---
session: s_b4730830
date: 2026-10-01
words: 1731
turns: 2
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-01 · Independent read-only review of Codex OAuth repair. Do not use tools or edit files. Report…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_b4730830` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Independent read-only review of Codex OAuth repair. Do not use tools or edit files. Report real correctness/security regressions and end with ACCEPT or BLOCK. Test mock credentials.scopes has since been set to SCOPES. Diff follows:
--- a/youtube_publish.py
+++ b/youtube_publish.py
@@ -58,6 +58,8 @@
     python ~/.claude/scripts/youtube_publish.py verify <videoId>
 
 Регресс: ~/.claude/scripts/_test_youtube_publish.py
+OAuth boundary: callback state is validated; credentials must resolve to exactly
+CHANNEL_ID before persistence and before every API client is returned.
 Скилл-дверь: ~/.claude/skills/youtube-publish/SKILL.md
 Канон: CLAUDE.md §9.13, §1.1 (подпись), §3.3 (раскрытие Майкрофта), §5.7 (shadow-first).
 """
@@ -994,6 +996,39 @@
     return creds if creds and creds.valid else None
 
 
+def require_target_channel(response: dict) -> None:
+    """Fail closed on an empty, mixed or wrong channel identity."""
+    items = response.get("items", [])
+    if len(items) != 1 or items[0].get("id") != CHANNEL_ID:
+        raise RuntimeError(f"OAuth channel is not exactly {CHANNEL_HANDLE} ({CHANNEL_ID})")
+
+
+def checked_youtube_service(creds):
+    from googleapiclient.discovery import build
+    yt = build("youtube", "v3", credentials=creds, cache_discovery=False)
+    require_target_channel(yt.channels().list(part="id", mine=True).execute())
+    return yt
+
+
+def parse_oauth_callback(path: str, expected_state: str) -> dict:
+    """Accept only one terminal result bound to this login attempt."""
+    from urllib.parse import urlparse, parse_qs
+    from hmac import compare_digest
+    parsed = urlparse(path)
+    q = parse_qs(parsed.query, keep_blank_values=True)
+    states = q.get("state", [])
+    if (parsed.path != "/" or len(states) != 1 or not expected_state
+            or not compare_digest(states[0].encode(), expected_state.encode())):
+        raise ValueError("Invalid OAuth callback state or path")
+    result = {key: q[key] for key in ("code", "error") if key in q}
+    if len(result) != 1:
+        raise ValueError("Expected exactly one OAuth result")
+    key, values = next(iter(result.items()))
+    if len(values) != 1 or not values[0]:
+        raise ValueError("Invalid OAuth result")
+    return {key: values[0]}
+
+
 def youtube_service():
     from googleapiclient.discovery import build  # noqa: PLC0415
     creds = _creds()
@@ -1003,7 +1038,7 @@
             f"  python {Path(__file__).name} auth login\n"
             f"токен ляжет в {TOKEN_FILE()}"
         )
-    return build("youtube", "v3", credentials=creds, cache_discovery=False)
+    return checked_youtube_service(creds)
 
 
 def cmd_auth(args) -> int:
@@ -1041,7 +1076,6 @@
     # строкой и сразу, а сервер ловит код сам — один клик вместо переписки.
     import threading  # noqa: PLC0415
     from http.server import BaseHTTPRequestHandler, HTTPServer  # noqa: PLC0415
-    from urllib.parse import urlparse, parse_qs  # noqa: PLC0415
     from google_auth_oauthlib.flow import InstalledAppFlow  # noqa: PLC0415
 
     cs = CLIENT_SECRET_FILE()
@@ -1053,15 +1087,22 @@
 
     class H(BaseHTTPRequestHandler):
         def do_GET(self):  # noqa: N802
-            q = parse_qs(urlparse(self.path).query)
-            box.update({k: v[0] for k, v in q.items()})
+            try:
+                result = parse_oauth_callback(self.path, _state)
+            except ValueError:
+                self.send_error(400, "Invalid OAuth callback")
+                return
+            if box:
+                self.send_error(409, "OAuth callback already received")
+                return
+            box.update(result)
             self.send_response(200)
             self.send_header("Content-Type", "text/html; charset=utf-8")
             self.end_headers()
             ok = "code" in box
             self.wfile.write(
-                ("<h2>" + ("Готово, можно закрыть вкладку." if ok
-                           else "Не получилось: " + box.get("error", "?")) + "</h2>")
+                ("<h2>" + ("Ответ получен. Проверка токена и канала ещё выполняется." if ok
+                           else "Вход отклонён. Подробности в терминале.") + "</h2>")
                 .encode("utf-8"))
 
         def log_message(self, *a):  # тишина в логе
@@ -1107,10 +1148,13 @@
     except Exception:
         pass
 
-    deadline = time.time() + wait_s
-    while "code" not in box and "error" not in box and time.time() < deadline:
-        time.sleep(1)
-    srv.shutdown()
+    deadline = time.monotonic() + wait_s
+    try:
+        while "code" not in box and "error" not in box and time.monotonic() < deadline:
+            time.sleep(1)
+    finally:
+        srv.shutdown()
+        srv.server_close()
 
     if "error" in box:
         print(f"❌ отказ на экране согласия: {box['error']}")
@@ -1121,7 +1165,12 @@
               "снова и раздавай ТОЛЬКО новую ссылку, старая молча вернёт invalid_grant.")
         return 1
 
-    flow.fetch_token(code=box["code"])
+    try:
+        flow.fetch_token(code=box["code"])
+        checked_youtube_service(flow.credentials)
+    except Exception as e:
+        print(f"❌ OAuth exchange/channel verification failed ({type(e).__name__}); token not saved")
+        return 1
     TOKEN_FILE().parent.mkdir(parents=True, exist_ok=True)
     TOKEN_FILE().write_text(flow.credentials.to_json(), encoding="utf-8")
     print(f"✅ токен сохранён: {TOKEN_FILE()}")
--- /dev/null
+++ b/_test_youtube_auth_boundary.py
@@ -0,0 +1,85 @@
+"""OAuth boundary tests: no real credentials, network or browser."""
+import unittest
+import argparse
+import tempfile
+from pathlib import Path
+from urllib.request import urlopen
+from urllib.error import HTTPError
+from unittest.mock import Mock, patch
+import youtube_publish as yp
+
+
+class AuthBoundary(unittest.TestCase):
+    def test_channel_empty_rejected(self):
+        with self.assertRaises(RuntimeError):
+            yp.require_target_channel({'items': []})
+
+    def test_channel_wrong_rejected(self):
+        with self.assertRaises(RuntimeError):
+            yp.require_target_channel({'items': [{'id': 'wrong'}]})
+
+    def test_channel_mixed_rejected(self):
+        with self.assertRaises(RuntimeError):
+            yp.require_target_channel({'items': [{'id': yp.CHANNEL_ID}, {'id': 'wrong'}]})
+
+    def test_target_allowed(self):
+        yp.require_target_channel({'items': [{'id': yp.CHANNEL_ID}]})
+
+    def test_service_blocks_wrong_channel(self):
+        service = Mock()
+        service.channels.return_value.list.return_value.execute.return_value = {'items': []}
+        with patch.object(yp, '_creds', return_value=Mock()), patch('googleapiclient.discovery.build', return_value=service):
+            with self.assertRaises(RuntimeError):
+                yp.youtube_service()
+
+    def test_callback_exact_state(self):
+        self.assertEqual(yp.parse_oauth_callback('/?state=expected&code=abc', 'expected'), {'code': 'abc'})
+
+    def test_callback_bad_inputs(self):
+        for path in ['/?code=abc', '/?state=wrong&code=abc', '/favicon.ico', '/?state=expected&code=a&code=b', '/?state=expected&code=a&error=no', '/?state=expected', '/?state=expected&state=wrong&code=a']:
+            with self.subTest(path=path), self.assertRaises(ValueError):
+                yp.parse_oauth_callback(path, 'expected')
+
+    def test_callback_error(self):
+        self.assertEqual(yp.parse_oauth_callback('/?state=expected&error=access_denied', 'expected'), {'error': 'access_denied'})
+
+    def login(self, channel_ok=True, exchange_ok=True):
+        from google_auth_oauthlib.flow import InstalledAppFlow
+        flow = Mock()
+        flow.authorization_url.return_value = ('https://example.invalid/not-opened', 'expected')
+        flow.credentials.to_json.return_value = '{"test":"new"}'
+        if not exchange_ok:
+            flow.fetch_token.side_effect = RuntimeError('do not print secrets')
+        service = Mock()
+        service.channels.return_value.list.return_value.execute.return_value = {
+            'items': [{'id': yp.CHANNEL_ID if channel_ok else 'wrong', 'snippet': {'title': 'test'}}]}
+        def browser(_):
+            with self.assertRaises(HTTPError) as error:
+                urlopen(flow.redirect_uri + '?state=wrong&code=bad', timeout=3)
+            self.assertEqual(error.exception.code, 400)
+            with urlopen(flow.redirect_uri + '?state=expected&code=good', timeout=3) as response:
+                self.assertEqual(response.status, 200)
+            with self.assertRaises(HTTPError) as error:
+                urlopen(flow.redirect_uri + '?state=expected&code=replay', timeout=3)
+            self.assertEqual(error.exception.code, 409)
+            return True
+        with tempfile.TemporaryDirectory() as directory:
+            token = Path(directory) / 'token.json'
+            token.write_text('old-token', encoding='utf-8')
+            with patch.object(yp, 'TOKEN_FILE', return_value=token), patch.object(yp, 'CLIENT_SECRET_FILE', return_value=token), patch.object(InstalledAppFlow, 'from_client_secrets_file', return_value=flow), patch('webbrowser.open', side_effect=browser), patch('googleapiclient.discovery.build', return_value=service), patch.object(yp, '_creds', return_value=flow.credentials), patch.dict(yp.os.environ, {'YT_OAUTH_PORT': '0', 'YT_OAUTH_WAIT': '3'}):
+                result = yp.cmd_auth(argparse.Namespace(action='login'))
+            flow.fetch_token.assert_called_once_with(code='good')
+            return result, token.read_text(encoding='utf-8')
+
+    def test_live_callback_wrong_channel_preserves_token(self):
+        self.assertEqual(self.login(channel_ok=False), (1, 'old-token'))
+
+    def test_live_callback_exchange_failure_preserves_token(self):
+        self.assertEqual(self.login(exchange_ok=False), (1, 'old-token'))
+
+    def test_live_callback_success(self):
+        self.assertEqual(self.login(), (0, '{"test":"new"}'))
+
+
+if __name__ == '__main__':
+    unittest.main()

---

**Claude:**

Read-only review, no tools used, judging the diff as shown.

## What the change gets right

- State is bound to the login attempt and compared with `compare_digest`; exactly one `state`, exactly one terminal result (`code` xor `error`), non-empty value, everything else in the query ignored. The old `box.update({k: v[0] for k, v in q.items()})` accepted anything any local process sent, including an injected `code`. That hole is closed.
- Replay/second callback returns 409 instead of silently overwriting `box`.
- No token is persisted until both the exchange and the channel identity check pass, and the on-disk token survives a failed login (proved by the two preserve-token tests).
- `time.monotonic()` for the deadline (immune to clock steps), `shutdown()` + `server_close()` in `finally` (socket released even if the wait raises).
- Browser HTML no longer echoes `box["error"]`, and `send_error` only ever gets constant strings, so nothing attacker-controlled reaches the response body.
- `len(items) != 1` rejecting a mixed/multi-channel response is the right fail-closed reading of `mine=True`, and the tests pin it.

## Findings

**1. Scope sufficiency for `channels.list(mine=True)`. Blocking if true, and the tests cannot see it.** `channels.list` needs one of `youtube`, `youtube.readonly`, `youtube.force-ssl`, or `youtubepartner`. `youtube.upload` alone is not sufficient and returns 403 `insufficientPermissions`. If `SCOPES` is upload-only, this diff fails closed on *everything*: every `youtube_service()` call raises, and `cmd_auth login` can never persist a token, so the tool locks itself out with no recovery path short of editing the code. Every test patches `googleapiclient.discovery.build` with a `Mock`, so the gate passes in CI under any scope set whatsoever. Confirm `SCOPES` contains a read-capable youtube scope, and do one real `auth login` before trusting this. Everything else below assumes that check passes.

**2. One transient error between `fetch_token` and the channel check costs a full re-login, and the diagnostic is thrown away.** The authorization code is single use (the file's own message says a reused link returns `invalid_grant`), so a 503 or DNS blip on `channels.list` discards credentials that were valid, and the operator has to start over with a brand new link. Worse, `except Exception` collapses "wrong channel" and "network down" and "bad scope" into one line that prints only `type(e).__name__`. The carefully worded `OAuth channel is not exactly @handle (ID)` message never reaches anyone, and it contains only public constants so printing it is safe. Suggested: catch `RuntimeError` separately and print `str(e)`; for transport errors either retry the identity check once or report them distinctly so a retry is not confused with an identity rejection.

**3. `parsed.path != "/"` hard-codes an assumption about `redirect_uri` that lives elsewhere.** The parser is correct for browser traffic today (browsers normalise an empty path to `/`), but the constraint is not derived from the redirect URI the flow actually registered. If `redirect_uri` ever gains a path, or a non-browser client sends `GET ?code=...` verbatim, every callback becomes 400, `box` stays empty, and the operator is handed the *wrong* diagnosis: the timeout branch tells them the link expired and to generate a new one, which will fail identically forever. Prefer `urlparse(flow.redirect_uri).path or "/"` as the expected path.

**4. Dead import.** `youtube_service()` still does `from googleapiclient.discovery import build` but no longer calls `build`; the import moved into `checked_youtube_service`. Remove it.

**5. The docstring claim is broader than the diff.** "before every API client is returned" is only enforced in `youtube_service()`. Worth grepping the file for any other `build(` or direct `_creds()` consumer; if one exists, the boundary statement in the module docstring is false and that path is the hole. I could not verify this from the diff alone.

**6. Minor test note.** `test_service_blocks_wrong_channel` patches `yp._creds` to a bare `Mock()`, so `creds` is truthy and the `if not creds` guard is bypassed by construction rather than by a realistic credential. Fine for intent, but combined with finding 1 the suite proves the *shape* of the gate and nothing about the API contract it depends on. One live run is the only thing that closes that gap.

Nothing here is an injected vulnerability or a logic inversion; the security posture is strictly better than before. Findings 1 is a pre-merge verification, 2 and 3 are robustness and diagnosability costs, 4 to 6 are cleanup.

**ACCEPT** (merge after confirming `SCOPES` admits `channels.list(mine=True)`; if it is upload-only, this flips to BLOCK).

🧒 Простыми словами: новая дверь проверяет, что вернувшийся ключ правда наш и что канал правда наш, и не сохраняет ключ, пока не проверит. Это хорошо. Но проверка канала просит у Google чуть больше прав, чем «просто загрузить видео», и в тестах Google ненастоящий, поэтому тесты этого не увидят. Надо один раз глазами посмотреть строку с правами и один раз войти по-настоящему. Ещё: если интернет мигнёт в самый момент проверки, вход придётся начинать заново, а на экране будет написано непонятное одно слово вместо причины.
