---
session: s_338d3a02
date: 2026-10-02
words: 1236
turns: 1
tools: ""
license: CC-BY-4.0
dataset: https://huggingface.co/datasets/TonyDzi/agent-sessions
---

# 2026-10-02 · Independent code review, read-only. Return ACCEPT or BLOCK for bounded shadow automation…

_Full working session of an LLM coding agent, scrubbed by rule (names kept as stable pseudonyms; surnames, e-mails, phones, street addresses and ages replaced by [ФАМИЛИЯ], [EMAIL], [ТЕЛЕФОН], [АДРЕС], [ВОЗРАСТ]; hosts and keys replaced). Row `s_338d3a02` of the [dataset](https://huggingface.co/datasets/TonyDzi/agent-sessions)._

**User:**

Independent code review, read-only. Return ACCEPT or BLOCK for bounded shadow automation. Find concrete correctness/privacy/dedup/budget/deadline/coverage bugs. Do not edit or send anything. Scope: public metadata, local outputs only; 1 USD reservation cap, not vendor hard cap; stop 30 October; partial data explicitly unknown. No tools needed, full source follows. SHA256 23d7cbfafb3432c3bd9516151a6d99faef1ba214410a131aecc735e661a71baa

"""Public-input JEV shadow analyst. Independent outputs only; see adjacent passport."""
from __future__ import annotations
import argparse, base64, calendar, hashlib, json, math, os, re, sqlite3, subprocess, time
from itertools import zip_longest
from contextlib import contextmanager, closing
from datetime import datetime, date, timezone, timedelta
from pathlib import Path
from urllib.parse import urlsplit

HOME=Path.home()/'.claude'
MODEL='jev-1.13-20260917'
END=date(2026,10,30)
RESERVE=0.001
SOURCES={'research':('tonydzi/deep-research','research/'), 'content':('tonydzi/the-journey','artifacts/writings/')}
PROMPTS={
 'jobs':{'gig_labor':'Posting is piecework AI rating, annotation or outsourced gig labor.', 'student_required':'Posting explicitly requires current student enrollment. Internship alone is NOT sufficient.', 'software_product_ops':'Role involves software engineering, product, operations or partnerships.', 'multiple_roles':'Title combines several separate job advertisements.', 'insufficient_evidence':'Title/company/location alone are insufficient to determine actual eligibility.'},
 'threads':{'needs_response':'A recent comment asks tonydzi a question or requests action with no later answer from tonydzi.', 'actionable_request':'A concrete unresolved request, correction or next step exists.', 'insufficient_evidence':'Excerpt is insufficient to establish who owes a response.'},
 'research':{'answers_question':'Material substantively answers the research question stated in its heading/introduction.', 'is_plan_only':'Material is a plan or refusal instead of substantive findings.', 'unsupported_claims':'Material makes factual claims without supporting evidence or sources in the supplied text.', 'insufficient_evidence':'Available excerpt is insufficient to assess research quality.'},
 'content':{'generic_text':'Article relies on generic assertions instead of concrete examples.', 'repetition':'Article repeats substantially the same point without adding information.', 'unsupported_claims':'Article presents strong factual claims without evidence in the supplied text.', 'insufficient_evidence':'Available excerpt is insufficient to assess quality.'}}
QUESTIONS={ch:{k:{'type':'noul','instructions':v} for k,v in qs.items()} for ch,qs in PROMPTS.items()}

def packed(x): return json.dumps(x,ensure_ascii=False,sort_keys=True)
def now():
    utc=datetime.now(timezone.utc)
    def last_sunday(month):
        d=datetime(utc.year,month,calendar.monthrange(utc.year,month)[1],1,tzinfo=timezone.utc)
        return d-timedelta(days=(d.weekday()+1)%7)
    return utc.astimezone(timezone(timedelta(hours=int(last_sunday(3)<=utc<last_sunday(10)))))
def gh(args):
    r=subprocess.run(['gh',*args],capture_output=True,text=True,encoding='utf-8',timeout=25)
    if r.returncode: raise RuntimeError('github_read_failed')
    return json.loads(r.stdout)
def public(repo,reader=gh):
    if reader(['repo','view',repo,'--json','visibility']).get('visibility')!='PUBLIC':
        raise PermissionError('repository_not_verified_public')
def public_job(url):
    try:
        u=urlsplit(url); host=(u.hostname or '').lower()
        return u.scheme=='https' and not u.username and not u.password and not u.query and any(host==h or host.endswith('.'+h) for h in ('greenhouse.io','lever.co','ashbyhq.com','myworkdayjobs.com','smartrecruiters.com','jobs.workable.com'))
    except ValueError: return False
def inventory(db,config,states):
    out=[]; skipped=0
    if db.exists():
        with closing(sqlite3.connect(db.resolve().as_uri()+'?mode=ro',uri=True)) as c:
            for url,company,title,location in c.execute("SELECT url,company,title,location FROM ats_jobs WHERE status='new' ORDER BY last_seen DESC,url"):
                if not title or not public_job(url or ''): skipped+=1; continue
                out.append({'channel':'jobs','key':url,'state':packed({'company':(company or '')[:200],'title':title[:500],'location':(location or '')[:200]})})
    if config.exists():
        for p in json.loads(config.read_text(encoding='utf-8-sig')).get('prs',[]):
            repo=p.get('repo',''); n=p.get('number')
            if not re.fullmatch(r'[A-Za-z0-9_.-]+/[A-Za-z0-9_.-]+',repo) or not isinstance(n,int): skipped+=1; continue
            f=states/(repo.replace('/','-')+'-'+str(n)+'.json')
            try: s=json.loads(f.read_text(encoding='utf-8-sig'))
            except (ValueError,OSError): skipped+=1; continue
            if s.get('state','').lower()!='open' or s.get('kind')=='discussion': skipped+=1; continue
            out.append({'channel':'threads','key':repo+'#'+str(n),'repo':repo,'number':n})
    return out,skipped
def public_corpus(reader=gh):
    out=[]; errors=0
    for channel,(repo,prefix) in SOURCES.items():
        try:
            public(repo,reader)
            tree=reader(['api',f'repos/{repo}/git/trees/main?recursive=1'])
            if tree.get('truncated'): raise ValueError('truncated_tree')
            for x in sorted(tree.get('tree',[]),key=lambda x:x['path'],reverse=True):
                if x['type']=='blob' and x['path'].startswith(prefix) and x['path'].endswith('.md') and x.get('size',0)<=100000:
                    out.append({'channel':channel,'key':repo+'/'+x['path'],'repo':repo,'sha':x['sha'],'corpus':'public_historical_replay'})
        except Exception: errors+=1
    return out,errors
def hydrate(obj,reader=gh):
    if obj['channel']=='jobs': return obj['state']
    repo=obj['repo']; public(repo,reader)
    if obj['channel'] in SOURCES:
        x=reader(['api',f'repos/{repo}/git/blobs/{obj["sha"]}'])
        return base64.b64decode(x['content'],validate=False).decode('utf-8')
    n=obj['number']; issue=reader(['api',f'repos/{repo}/issues/{n}'])
    count=issue.get('comments',0)
    if count>100: raise ValueError('thread_too_large_for_bounded_read')
    comments=reader(['api',f'repos/{repo}/issues/{n}/comments?per_page=100'])
    return packed({'title':issue.get('title','')[:1000],'body':(issue.get('body') or '')[:6000], 'state':issue.get('state'), 'truncated':len(comments)>20,
        'title_truncated':len(issue.get('title',''))>1000,'body_truncated':len(issue.get('body') or '')>6000,
        'comments_omitted':max(0,len(comments)-20),'comment_bodies_truncated':sum(len(x.get('body') or '')>1000 for x in comments[-20:]),
        'comments':[{'user':x.get('user',{}).get('login'),'body':(x.get('body') or '')[:1000]} for x in comments[-20:]]})
@contextmanager
def locked(root):
    root.mkdir(parents=True,exist_ok=True); path=root/'run.lock'
    f=path.open('a+b'); f.seek(0)
    if path.stat().st_size==0: f.write(b'0'); f.flush()
    f.seek(0)
    try:
        if os.name=='nt':
            import msvcrt
            msvcrt.locking(f.fileno(),msvcrt.LK_NBLCK,1)
        else:
            import fcntl
            fcntl.flock(f,fcntl.LOCK_EX|fcntl.LOCK_NB)
        yield
    finally: f.close()
def connect(root):
    c=sqlite3.connect(root/'ledger.sqlite')
    c.execute('CREATE TABLE IF NOT EXISTS decisions (digest TEXT PRIMARY KEY, channel TEXT, object_key TEXT, ts TEXT, status TEXT, reserved REAL, model TEXT, input TEXT, answers TEXT, judgment TEXT, error TEXT, cost_usd REAL)')
    c.execute('CREATE TABLE IF NOT EXISTS runs (ts TEXT,counters TEXT)'); c.commit(); return c
def transport(state,questions,channel):
    import jev_ask
    old_log=jev_ask._log; old_tries=jev_ask.MAX_TRIES
    def safe_log(**row): row.pop('detail',None); old_log(**row)
    jev_ask._log=safe_log; jev_ask.MAX_TRIES=1; os.environ['JEV_ACTOR']='codex'
    try: return jev_ask.ask(state,questions,model=MODEL,rail='openrouter',timeout=25,caller='analyst-'+channel)
    finally: jev_ask._log=old_log; jev_ask.MAX_TRIES=old_tries
def valid(answers,questions):
    return isinstance(answers,dict) and set(answers)==set(questions) and all(isinstance(v,dict) and type(v.get('noul')) in (float,int) and math.isfinite(v['noul']) and 0<=v['noul']<=1 for v in answers.values())
def classify(report):
    counts=report['channels'].values()
    total=lambda key:sum(x[key] for x in counts)
    errors=total('errors')+report.get('source_errors',0)
    if errors: return ('PARTIAL' if total('reviewed') else 'ERROR',1)
    if total('budget_blocked'): return ('BUDGET_EXHAUSTED',3)
    if total('reviewed'): return ('OK',0)
    if total('eligible') and total('deduplicated')==total('eligible'): return ('NO_NEW',0)
    return ('NO_INPUT' if not total('eligible') else 'INCOMPLETE',2)
def run(objects,root,limit=20,budget=1.0,today=None,ask=transport,hydrate_fn=hydrate,skipped=0,source_errors=0,source_availability=None):
    get_day=lambda: today or now().date()
    counters={ch:{'eligible':sum(o['channel']==ch for o in objects),'reviewed':0,'errors':0,'skipped':0,'deduplicated':0,'budget_blocked':0,'unjudged':0} for ch in QUESTIONS}
    if get_day()>=END: return {'stopped':'evaluation_date_reached','channels':counters}
    with locked(root),closing(connect(root)) as c:
        used=c.execute('SELECT COALESCE(SUM(reserved),0) FROM decisions').fetchone()[0]
        attempts={}; fetches={}; started=time.monotonic()
        run_n=c.execute('SELECT count(*) FROM runs').fetchone()[0]
        groups=[]
        for channel in QUESTIONS:
            group=[o for o in objects if o['channel']==channel]
            offset=(run_n*20)%len(group) if group else 0
            groups.append(group[offset:]+group[:offset])
        reordered=[item for batch in zip_longest(*groups) for item in batch if item is not None]
        for obj in reordered:
            ch=obj['channel']; stats=counters[ch]
            if get_day()>=END or time.monotonic()-started>120: stats['skipped']+=1; continue
            if attempts.get(ch,0)>=limit or fetches.get(ch,0)>=20: stats['skipped']+=1; continue
            try:
                if ch!='jobs': fetches[ch]=fetches.get(ch,0)+1
                raw=hydrate_fn(obj)
                state=packed({'source':obj['key'],'provenance':'public_ats_metadata' if ch=='jobs' else 'live_public_github',
                              'corpus':obj.get('corpus','current_source'),'excerpt_truncated':len(raw)>28000,'text':raw[:28000]})
            except Exception: stats['errors']+=1; continue
            digest=hashlib.sha256(packed(['analyst-v1',MODEL,ch,obj['key'],state,QUESTIONS[ch]]).encode()).hexdigest()
            if c.execute('SELECT 1 FROM decisions WHERE digest=?',(digest,)).fetchone(): stats['deduplicated']+=1; continue
            if get_day()>=END: stats['skipped']+=1; continue
            if used+RESERVE>budget+1e-9: stats['budget_blocked']+=1; continue
            attempts[ch]=attempts.get(ch,0)+1
            c.execute('INSERT INTO decisions VALUES (?,?,?,?,?,?,?,?,?,?,?,?)',(digest,ch,obj['key'],now().isoformat(),'reserved',RESERVE,MODEL,state,None,'unknown',None,None)); c.commit(); used+=RESERVE
            try:
                result=ask(state,QUESTIONS[ch],ch); answers=result.get('answers')
                if not valid(answers,QUESTIONS[ch]): raise ValueError('invalid_answers')
                cost=result.get('usage',{}).get('cost')
                charge=max(RESERVE,float(cost)) if type(cost) in (int,float) and math.isfinite(cost) and cost>=0 else RESERVE
                used+=charge-RESERVE
                c.execute('UPDATE decisions SET status=?,reserved=?,model=?,answers=?,cost_usd=? WHERE digest=?',('reviewed',charge,result.get('model') or MODEL,packed(answers),cost if type(cost) in (int,float) and math.isfinite(cost) and cost>=0 else None,digest))
                stats['reviewed']+=1; stats['unjudged']+=1
            except Exception as e:
                c.execute('UPDATE decisions SET status=?,error=? WHERE digest=?',('error',type(e).__name__,digest)); stats['errors']+=1
            c.commit()
        report={'ts':now().isoformat(),'channels':counters,'inventory_skipped':skipped,'reserved_usd':used,'accuracy':'unknown: independent judgments required', 'corpus_mode':'research/content historical public replay, not live production decisions'}
        report['source_errors']=source_errors
        report['source_availability']=source_availability or {'scope':'provided inventory only; wider source coverage unknown'}
        report['status'],report['exit_code']=classify(report)
        report['cumulative']=[dict(zip(('channel','status','n'),r)) for r in c.execute('SELECT channel,status,count(*) FROM decisions GROUP BY channel,status')]
        c.execute('INSERT INTO runs VALUES (?,?)',(now().isoformat(),packed(report))); c.commit()
        with (root/'events.jsonl').open('a',encoding='utf-8') as f: f.write(packed({'ts':now().isoformat(),'node':os.environ.get('COMPUTERNAME','unknown'),'actor':'codex','event':'analyst-shadow','outcome':report})+'\n')
        temporary=root/'report.tmp'; temporary.write_text(packed(report),encoding='utf-8'); os.replace(temporary,root/'report.json')
    return report
def main():
    p=argparse.ArgumentParser(description=__doc__); mode=p.add_mutually_exclusive_group(required=True)
    mode.add_argument('--dry',action='store_true'); mode.add_argument('--run',action='store_true'); mode.add_argument('--report',action='store_true')
    p.add_argument('--limit',type=int,default=20); p.add_argument('--budget-usd',type=float,default=1)
    p.add_argument('--db',type=Path,default=Path('D:/Vault/_imports/jobs-watch/jobs.db')); p.add_argument('--config',type=Path,default=HOME/'pr_watch.json'); p.add_argument('--states',type=Path,default=HOME/'pr_watch_state'); p.add_argument('--out',type=Path,default=HOME/'jev_analyst')
    a=p.parse_args()
    if not 1<=a.limit<=100 or not 0<a.budget_usd<=1: p.error('limit 1..100; lifetime reservation budget 0..1 USD')
    if a.report:
        if not (a.out/'report.json').exists(): print(packed({'status':'NO_REPORT'})); return 2
        report=json.loads((a.out/'report.json').read_text(encoding='utf-8')); print(packed(report)); return report.get('exit_code',2)
    if a.run and now().date()>=END: print(packed({'stopped':'evaluation_date_reached'})); return
    availability={'jobs_db':a.db.is_file(),'thread_config':a.config.is_file(),'thread_states':a.states.is_dir(), 'remote_corpus':'not_checked'}
    missing=sum(not v for v in list(availability.values())[:3])
    try: objects,skipped=inventory(a.db,a.config,a.states)
    except (OSError,ValueError,sqlite3.Error):
        print(packed({'status':'SOURCE_ERROR','source_availability':availability})); return 1
    if a.dry:
        print(packed({'status':'SOURCE_MISSING' if missing else 'INVENTORY_ONLY','source_availability':availability,'inventory':{ch:sum(o['channel']==ch for o in objects) for ch in QUESTIONS},'skipped':skipped,'network_calls':0,'unknown':'public corpus inventory and thread privacy require live gh read'})); return 2 if missing else 0
    corpus,errors=public_corpus(); objects+=corpus
    availability['remote_corpus']='checked; failures='+str(errors)
    report=run(objects,a.out,a.limit,a.budget_usd,skipped=skipped,source_errors=errors+missing,source_availability=availability)
    print(packed(report)); return report.get('exit_code',2)
if __name__=='__main__': raise SystemExit(main())


TESTS
"""Offline tests: temporary databases only, fake network and model."""
import hashlib
import base64
import json
from pathlib import Path
import sqlite3
import tempfile
import unittest
import subprocess
import sys
from contextlib import closing
import jev_analyst_shadow as m

def fake(state,questions,channel):
    return {'model':m.MODEL,'answers':{k:{'noul':0.3} for k in questions},'usage':{'cost':0.00001}}

class Tests(unittest.TestCase):
    def setUp(self):
        self.tmp=tempfile.TemporaryDirectory(); self.addCleanup(self.tmp.cleanup)
        self.root=Path(self.tmp.name)/'out'
        self.objects=[{'channel':'jobs','key':str(i),'state':'job '+str(i)} for i in range(3)]
    def run_it(self,**kw): return m.run(self.objects,self.root,today=m.date(2026,10,2),ask=kw.pop('ask',fake),**kw)
    def test_dedup_and_budget(self):
        a=self.run_it(budget=.002); self.assertEqual(a['channels']['jobs']['reviewed'],2)
        b=self.run_it(budget=.002); self.assertEqual(b['channels']['jobs']['deduplicated'],2); self.assertEqual(b['channels']['jobs']['reviewed'],0)
        with closing(sqlite3.connect(self.root/'ledger.sqlite')) as c:
            self.assertAlmostEqual(c.execute('select sum(reserved) from decisions').fetchone()[0],.002)
            self.assertAlmostEqual(c.execute('select sum(cost_usd) from decisions').fetchone()[0],.00002)
    def test_failure_reserved_no_secret_logged(self):
        def bad(*args): raise TimeoutError('SECRET_TOKEN_123')
        a=self.run_it(ask=bad,limit=1)
        self.assertEqual(a['channels']['jobs']['errors'],1)
        self.assertNotIn('SECRET_TOKEN_123',(self.root/'events.jsonl').read_text())
        b=self.run_it(limit=1); self.assertEqual(b['channels']['jobs']['reviewed'],1)
    def test_schema_validation(self):
        for value in (float('nan'),1.1,True):
            self.assertFalse(m.valid({'x':{'noul':value}},{'x':{}}))
        self.assertFalse(m.valid({'x':{'noul':.3},'extra':{}},{'x':{}}))
    def test_end_date_no_outputs(self):
        r=m.run(self.objects,self.root,today=m.END,ask=fake)
        self.assertIn('stopped',r); self.assertFalse(self.root.exists())
    def test_exclusive_lock(self):
        with m.locked(self.root):
            with self.assertRaises(OSError): self.run_it()
        with m.locked(self.root): pass
    def test_private_repo_denied_before_reading_body(self):
        calls=[]
        def reader(args): calls.append(args); return {'visibility':'PRIVATE'}
        with self.assertRaises(PermissionError): m.hydrate({'channel':'threads','repo':'x/y','number':1},reader)
        self.assertEqual(len(calls),1)
    def test_source_database_unchanged(self):
        db=Path(self.tmp.name)/'jobs.db'
        with closing(sqlite3.connect(db)) as c:
            c.execute('create table ats_jobs(url,company,title,location,status,last_seen)')
            c.execute('insert into ats_jobs values (?,?,?,?,?,?)',('https://jobs.lever.co/example/id','Example','Engineer','US','new','2026-10-02'))
            c.commit()
        before=hashlib.sha256(db.read_bytes()).hexdigest()
        objects,_=m.inventory(db,Path(self.tmp.name)/'missing',Path(self.tmp.name))
        m.run(objects,self.root,today=m.date(2026,10,2),ask=fake)
        self.assertEqual(hashlib.sha256(db.read_bytes()).hexdigest(),before)
    def test_secret_url_denied(self):
        self.assertFalse(m.public_job('https://jobs.lever.co/example?token=secret'))
        self.assertFalse(m.public_job('https://jobs.lever.co.evil.test/x'))
    def test_crash_releases_os_lock(self):
        code="import sys,os; sys.path.insert(0,sys.argv[1]); import jev_analyst_shadow as m; from pathlib import Path; lock=m.locked(Path(sys.argv[2])); lock.__enter__(); os._exit(0)"
        subprocess.run([sys.executable,'-c',code,str(Path(m.__file__).parent),str(self.root)],check=True)
        with m.locked(self.root): pass
    def test_multiple_runs_feed_unseen(self):
        objects=[{'channel':'jobs','key':str(i),'state':'job '+str(i)} for i in range(45)]
        for _ in range(3):
            r=m.run(objects,self.root,limit=2,today=m.date(2026,10,2),ask=fake)
            self.assertEqual(r['channels']['jobs']['reviewed'],2)
        with closing(sqlite3.connect(self.root/'ledger.sqlite')) as c:
            self.assertEqual(c.execute('select count(*) from decisions').fetchone()[0],6)
    def test_expiry_during_hydration_no_paid_call(self):
        from unittest.mock import patch
        days=iter([m.datetime(2026,10,29),m.datetime(2026,10,29),m.datetime(2026,10,30)])
        calls=[]
        with patch.object(m,'now',side_effect=lambda:next(days,m.datetime(2026,10,30))):
            m.run(self.objects,self.root,ask=lambda *a:calls.append(a))
        self.assertEqual(calls,[])
    def test_corpus_truncation_recorded_at_single_boundary(self):
        obj={'channel':'research','key':'public/doc.md','repo':'tonydzi/deep-research','sha':'abc'}
        def reader(args):
            return {'visibility':'PUBLIC'} if args[0]=='repo' else {'content':base64.b64encode(b'x'*35000).decode()}
        raw=m.hydrate(obj,reader)
        self.assertEqual(len(raw),35000)
        m.run([obj],self.root,today=m.date(2026,10,2),ask=fake,hydrate_fn=lambda o:raw)
        with closing(sqlite3.connect(self.root/'ledger.sqlite')) as c:
            payload=json.loads(c.execute('select input from decisions').fetchone()[0])
        self.assertTrue(payload['excerpt_truncated']); self.assertEqual(len(payload['text']),28000)
    def test_thread_truncation_flags(self):
        def reader(args):
            if args[0]=='repo': return {'visibility':'PUBLIC'}
            if '/comments?' in args[-1]: return [{'body':'x'*1200,'user':{'login':'public'}}]*22
            return {'body':'x'*7000,'title':'y'*1100,'comments':22}
        data=json.loads(m.hydrate({'channel':'threads','repo':'public/repo','number':1},reader))
        self.assertTrue(data['body_truncated']); self.assertTrue(data['title_truncated'])
        self.assertEqual(data['comments_omitted'],2); self.assertEqual(data['comment_bodies_truncated'],20)
    def test_no_input_and_all_errors_not_green(self):
        r=m.run([],self.root,today=m.date(2026,10,2),ask=fake)
        self.assertEqual((r['status'],r['exit_code']),('NO_INPUT',2))
        def bad(*a): raise TimeoutError()
        r=self.run_it(ask=bad)
        self.assertEqual((r['status'],r['exit_code']),('ERROR',1))
    def test_dedup_is_no_new_not_no_input(self):
        self.run_it(); r=self.run_it()
        self.assertEqual((r['status'],r['exit_code']),('NO_NEW',0))
    def test_missing_source_is_partial_despite_success(self):
        r=self.run_it(source_errors=1,source_availability={'thread_config':False})
        self.assertEqual((r['status'],r['exit_code']),('PARTIAL',1))

if __name__=='__main__': unittest.main(verbosity=2)
