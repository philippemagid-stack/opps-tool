# opps-tool<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;500;600&family=IBM+Plex+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
  :root{--ground:#E8EBEE;--card:#FFFFFF;--ink:#16202B;--muted:#6C7784;--hair:#D3D8DD;--petrol:#1F6F78;--petrol-soft:#E4EFF0;--flag:#8A3324;--sans:'IBM Plex Sans',system-ui,-apple-system,sans-serif;--mono:'IBM Plex Mono',ui-monospace,monospace}
  *{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
  .ops-root{font-family:var(--sans);color:var(--ink);background:var(--ground);padding:20px 16px 28px;border-radius:4px;max-width:620px;margin:0 auto;line-height:1.45}
  .ops-title{font-family:var(--mono);font-size:11px;font-weight:600;letter-spacing:.16em;text-transform:uppercase;color:var(--muted);margin:0}
  .ops-date{font-family:var(--mono);font-size:11px;letter-spacing:.08em;color:var(--muted);margin-top:4px}
  .head-row{display:flex;justify-content:space-between;align-items:flex-start;gap:12px;margin-bottom:14px}
  /* Signature: neglect gauge, not an accumulation score */
  .gauge{background:var(--card);border:1px solid var(--hair);border-radius:3px;padding:4px 16px;margin-bottom:10px}
  .grow{display:flex;align-items:center;gap:12px;padding:11px 0;border-bottom:1px solid var(--hair)}
  .grow:last-child{border-bottom:none}
  .gname{font-family:var(--mono);font-size:10px;letter-spacing:.14em;text-transform:uppercase;color:var(--muted);width:96px;flex-shrink:0}
  .gbar{flex:1;height:6px;background:var(--hair);border-radius:1px;overflow:hidden}
  .gfill{height:100%;background:var(--petrol)}
  .gfill.warn{background:var(--flag)}
  .gval{font-family:var(--mono);font-size:11px;font-weight:600;width:62px;text-align:right;flex-shrink:0}
  .gval.warn{color:var(--flag)}
  .strip{display:flex;justify-content:space-between;align-items:center;gap:10px;font-family:var(--mono);font-size:10px;letter-spacing:.1em;text-transform:uppercase;color:var(--muted);padding:0 0 14px;border-bottom:1px solid var(--hair);margin-bottom:16px;flex-wrap:wrap}
  .strip b{color:var(--ink);font-weight:600}
  .strip b.low{color:var(--flag)}
  .toggles{display:flex;gap:6px}
  .rule{background:var(--petrol-soft);border:1px solid var(--petrol);border-radius:3px;padding:12px 14px;margin-bottom:14px;font-size:14px;line-height:1.4}
  .rule-k{display:block;font-family:var(--mono);font-size:9px;letter-spacing:.16em;text-transform:uppercase;color:var(--petrol);margin-bottom:5px;font-weight:600}
  .ops-card{background:var(--card);border:1px solid var(--hair);border-radius:3px;padding:16px;margin-bottom:10px}
  .ops-card.alert{border-left:3px solid var(--flag)}
  .eyebrow{font-family:var(--mono);font-size:10px;letter-spacing:.16em;text-transform:uppercase;color:var(--muted);margin-bottom:10px}
  .eyebrow.flag{color:var(--flag)}
  .prompt{font-size:17px;font-weight:500;margin:0 0 14px}
  .btn-row{display:flex;gap:8px;flex-wrap:wrap}
  button{font-family:var(--sans);font-size:15px;font-weight:600;color:var(--ink);background:var(--card);border:1px solid var(--ink);border-radius:3px;padding:15px 18px;cursor:pointer;flex:1 1 130px;min-height:52px;transition:background .12s ease}
  button:hover{background:var(--petrol-soft)}
  button:focus-visible{outline:2px solid var(--petrol);outline-offset:2px}
  button.primary{background:var(--ink);color:#fff}
  button.primary:hover{background:var(--petrol);border-color:var(--petrol)}
  button.quiet{border-color:var(--hair);color:var(--muted);font-weight:500}
  .toggle{font-family:var(--mono);font-size:10px;letter-spacing:.08em;text-transform:uppercase;background:none;border:1px solid var(--hair);color:var(--muted);padding:5px 8px;min-height:0;flex:0 0 auto;font-weight:500;border-radius:2px}
  .toggle.on{border-color:var(--petrol);color:var(--petrol);background:var(--petrol-soft)}
  .option{display:flex;align-items:flex-start;gap:14px;width:100%;text-align:left;background:var(--card);border:1px solid var(--hair);border-radius:3px;padding:16px;margin-bottom:8px;font-size:16px;font-weight:400;min-height:0}
  .option:hover{border-color:var(--petrol);background:var(--petrol-soft)}
  .tag{font-family:var(--mono);font-size:12px;font-weight:600;color:var(--petrol);border:1px solid var(--petrol);border-radius:2px;padding:1px 6px;flex-shrink:0;margin-top:2px}
  .tag.sig{background:var(--petrol);color:#fff}
  .focus-text{font-size:20px;font-weight:600;letter-spacing:-.01em;margin:0 0 4px}
  .note{font-size:14px;color:var(--muted);margin:10px 0 0}
  input[type="text"],input[type="date"]{font-family:var(--sans);font-size:16px;width:100%;padding:14px;border:1px solid var(--hair);border-radius:3px;margin-bottom:10px;color:var(--ink)}
  input:focus{outline:2px solid var(--petrol);outline-offset:-1px;border-color:var(--petrol)}
  summary{font-family:var(--mono);font-size:10px;letter-spacing:.14em;text-transform:uppercase;color:var(--muted);cursor:pointer;padding:8px 0}
  details{margin-top:6px}
  .log-line{font-family:var(--mono);font-size:12px;color:var(--muted);padding:7px 0;border-bottom:1px solid var(--hair);display:flex;justify-content:space-between;gap:12px}
  .log-line.used{text-decoration:line-through;opacity:.5}
  .log-line b.no{color:var(--flag)}
  .reset{font-family:var(--mono);font-size:10px;letter-spacing:.1em;color:var(--muted);background:none;border:none;padding:10px 0;min-height:0;flex:0 0 auto;font-weight:400;text-decoration:underline;text-transform:uppercase}
  .reset:hover{background:none;color:var(--ink)}
  @media (prefers-reduced-motion:reduce){*{transition:none!important}}
</style>
<div class="ops-root" id="root"><div class="ops-card"><div class="eyebrow">Loading</div></div></div>
<script>
const P_HOME=[[1,'Be home when you said you would be. To the minute.'],[1,'Phone in another room for the first 15 minutes you are together.'],[1,'Sit with her for five minutes with nothing in your hands.'],[1,'Zero phone checks at dinner tonight.'],[1,'Give her the first hour after work, not the leftovers.'],[1,'Say yes to the next small thing she asks. No negotiating it.'],[1,'Laptop shut and away before she walks in.'],[2,'Phone off and in a drawer from 6pm until morning. Off, not silent.'],[2,'No laptop in the house tonight. Leave it in the car.'],[2,'Decline the evening call outright. Not rescheduled. Declined.'],[2,'Give her the whole of Saturday morning. Nothing booked around it.'],[2,'Take Thursday off. Drive her in, collect her, no conditions.'],[2,'Come back from the trip a day early. Do not announce it as a sacrifice.']];
const P_AWAY=[[1,'Call at the time you said. To the minute.'],[1,'Message when you land or finish, before she has to ask.'],[1,'Tell her what time you will call tomorrow. Then do it.'],[1,'Video call with nothing else open on your screen.'],[2,'Clear an evening on the road entirely. No calls, no dinner, just her.'],[2,'Move a meeting so you are free when she actually is.']];
const R_LIST=[[1,'Ask about something she told you last week. Use the detail, not the gist.'],[1,'Ask how the thing she was dreading actually turned out.'],[1,'Repeat back what she said before you respond. Once.'],[1,'Say one specific thing you noticed about her today. Out loud, once. Do not expand.'],[1,'Ask about a person she mentioned, by name.'],[1,'Ask what she wants this weekend, then do that thing.'],[2,'Whole conversation about her work. Zero solutions. Questions only, start to finish.'],[2,'Ask about the boss situation, then say nothing but questions for ten minutes.'],[2,'Before you respond to any problem tonight, ask which she wants. Listen or help.'],[2,'Sit through the full story without reaching for the fix. Ask what she needs from you at the end.']];
const B_LIST=[[1,'Do not take a call from your ex while you are with her. Return it later.'],[1,'Tell her about a co-parenting decision before you make it, not after.'],[1,'Batch ex-related replies into one window today.'],[1,'Tell her what is happening with the ex before she has to ask.'],[1,'Do not let an ex-related issue become tonight\'s conversation.'],[2,'Say no to an ex-related request with Galuh in the room. Let her see it happen.'],[2,'Set a contact window with your ex, tell Galuh what it is, hold it all week.'],[2,'Bring her into the next co-parenting conversation that affects the household.'],[2,'Make the next Pablo decision with her, not near her.']];
const B_PABLO=[[1,'Ask her what she wants out of this week with Pablo. Before you plan it.'],[1,'Include her in one decision about Pablo before you decide it.'],[2,'Book one full evening this week that is only her, inside the Pablo week.'],[2,'Let her choose how the weekend with Pablo runs. Then run it that way.']];
const RECOVER=['One question about her day. That is all.','Be home on time. Nothing else.','Phone away for ten minutes tonight.','Say one true specific sentence. Do not expand on it.','Make her a drink. Say nothing about yesterday.'];
const THU_PREP=[{c:'R',w:1,t:'Ask her what she needs for tomorrow. Write the answer down.'},{c:'P',w:2,t:'Clear tomorrow evening completely. No calls after 5. Tell her it is clear.'},{c:'P',w:2,t:'Offer the lift for tomorrow now, before she has to ask.'}];
const THU_DAY=[{c:'P',w:2,t:'Drive her in. Offered, not requested. No conditions.'},{c:'R',w:1,t:'Message before the meeting with her boss. Specific, not generic.'},{c:'P',w:2,t:'Be free and unreachable to work at the end of her day.'}];

const KEY='ops-state-v5';
const blank={streak:0,today:null,lastAudit:null,recent:[],frictions:[],signals:[],asks:[],dropped:[],history:[],away:false,pablo:false};
let S={...blank},view='home',offered=[],heavy=false;
const el=document.getElementById('root');
const today=()=>new Date().toLocaleDateString('en-CA');
const dow=()=>new Date().getDay();
const esc=s=>String(s).replace(/[<>&"]/g,c=>({'<':'&lt;','>':'&gt;','&':'&amp;','"':'&quot;'}[c]));
const daysAgo=n=>{const d=new Date();d.setDate(d.getDate()-n);return d.toLocaleDateString('en-CA');};
const gap=a=>Math.round((new Date(today())-new Date(a))/864e5);

async function load(){try{const r=await window.storage.get(KEY,false);if(r&&r.value)S={...blank,...JSON.parse(r.value)};}catch(e){}
  if(S.today&&S.today.date!==today())S.today=null;render();}
async function save(){try{await window.storage.set(KEY,JSON.stringify(S),false);}catch(e){console.error(e);}}

function recovering(){const y=daysAgo(1);const h=S.history.find(x=>x.date===y);return h&&h.status==='missed';}
function lastServed(c){const h=S.history.filter(x=>x.status==='done'&&x.c===c);return h.length?gap(h[h.length-1].date):null;}

function heavyThisWeek(){const c=daysAgo(7);return S.history.filter(h=>h.date>=c&&h.status==='done'&&h.w===2).length;}
function pickThree(heavy){
  if(recovering())return RECOVER.slice(0,3).map(t=>({c:'P',w:1,t:t}));
  if(dow()===3)return THU_PREP.slice();
  if(dow()===4)return THU_DAY.slice();
  const pool=arr=>{let p=arr.filter(x=>x[0]===(heavy?2:1)&&!S.recent.includes(x[1]));
    if(!p.length)p=arr.filter(x=>x[0]===(heavy?2:1));
    if(!p.length)p=arr;
    return {w:p[0][0],t:p[Math.floor(Math.random()*p.length)][1]};};
  const out=[];
  const openDrop=S.dropped.filter(d=>!d.used);
  if(!heavy&&openDrop.length&&Math.random()<0.5){const d=openDrop[openDrop.length-1];out.push({c:'P',w:1,t:'She stopped asking for this. Offer it, on her terms: '+d.text,drop:d.text});}
  else {const x=pool(S.away?P_AWAY:P_HOME);out.push({c:'P',w:x.w,t:x.t});}
  const due=S.signals.filter(s=>!s.used&&(!s.resurface||s.resurface<=today()));
  if(!heavy&&due.length&&Math.random()<0.8){const g=due[due.length-1];out.push({c:'R',w:1,t:'Bring this back to her: '+g.text,sig:g.text});}
  else {const x=pool(R_LIST);out.push({c:'R',w:x.w,t:x.t});}
  const x=pool(S.pablo?B_PABLO.concat(B_LIST):B_LIST);out.push({c:'B',w:x.w,t:x.t});
  return out;
}
const CHEERS=['Set. Small and done beats big and discussed.','Locked. One thing, plainly. That is the whole game.','Set. Nothing else needs to happen today.','Locked. Do it once. Do not add to it.'];

function gaugeRow(name,key){
  const d=lastServed(key);
  const warn=d===null||d>7;
  const pct=d===null?0:Math.max(6,100-Math.min(d,14)/14*100);
  return '<div class="grow"><span class="gname">'+name+'</span><span class="gbar"><span class="gfill'+(warn?' warn':'')+'" style="width:'+pct+'%"></span></span><span class="gval'+(warn?' warn':'')+'">'+(d===null?'never':d===0?'today':d+'d ago')+'</span></div>';
}

function render(){
  const d=new Date().toLocaleDateString('en-AU',{weekday:'short',day:'numeric',month:'short'});
  const a14=S.asks.filter(x=>x.date>=daysAgo(14));
  const yes=a14.filter(x=>x.answer==='yes').length;
  const isThu=dow()===4,isWed=dow()===3,rec=recovering(),hv=heavyThisWeek();
  let body='';

  if(view==='home'){
    let banner='';
    if(rec)banner='<div class="ops-card alert"><div class="eyebrow flag">Recovery day</div><p class="prompt" style="margin:0">Yesterday missed. Today goes smaller, not bigger. Do not overcorrect.</p></div>';
    else if(isWed)banner='<div class="ops-card alert"><div class="eyebrow flag">Standing protocol / Wednesday</div><p class="prompt" style="margin:0">Tomorrow is the hard day. Tonight is prep, not recovery.</p></div>';
    else if(isThu)banner='<div class="ops-card alert"><div class="eyebrow flag">Standing protocol / Thursday</div><p class="prompt" style="margin:0">Offer before she asks. Do not make her negotiate for it.</p></div>';

    if(S.today&&S.today.status==='set'){
      body=banner+'<div class="ops-card"><div class="eyebrow">Active focus / '+S.today.c+'</div><p class="focus-text">'+esc(S.today.t)+'</p><p class="note">One thing. Adding more is overcompensating.</p></div><div class="btn-row"><button class="primary" data-go="audit">Audit tonight</button></div><div class="btn-row" style="margin-top:8px"><button class="quiet" data-go="signal">Signal</button><button class="quiet" data-go="ask">Log an ask</button><button class="quiet" data-go="drop">Stopped asking</button></div>';
    }else if(S.today&&(S.today.status==='done'||S.today.status==='missed')){
      const done=S.today.status==='done';
      body=banner+'<div class="ops-card"><div class="eyebrow">Closed</div><p class="focus-text">'+(done?'Logged.':'Friction logged.')+'</p><p class="note">'+(done?'Back tomorrow. Nothing more today.':'Tomorrow goes smaller. One miss is not the pattern.')+'</p></div><div class="btn-row"><button class="quiet" data-go="signal">Signal</button><button class="quiet" data-go="ask">Log an ask</button><button class="quiet" data-go="drop">Stopped asking</button></div>';
    }else{
      body=banner+'<div class="ops-card"><div class="eyebrow">No focus set</div><p class="prompt">Pick today\'s single action.</p><div class="btn-row"><button class="primary" data-go="morning">Morning</button><button data-go="audit">Audit</button></div><div class="btn-row" style="margin-top:8px"><button class="quiet" data-go="signal">Signal</button><button class="quiet" data-go="ask">Log an ask</button><button class="quiet" data-go="drop">Stopped asking</button></div></div>';
    }
  }
  if(view==='morning'){
    if(!offered.length)offered=pickThree(heavy);
    const fixed=isWed||isThu||rec;
    body='<div class="eyebrow" style="margin-left:2px">'+(rec?'Recovery set. Smallest available.':fixed?'Standing protocol':'Choose one')+'</div>'+offered.map((a,i)=>'<button class="option" data-pick="'+i+'"><span class="tag'+(a.sig||a.drop?' sig':'')+'">'+a.c+(a.w===2?'\u2009\u25cf':'')+'</span><span>'+esc(a.t)+'</span></button>').join('')+'<div class="btn-row"><button class="quiet" data-go="home">Back</button>'+(fixed?'':'<button class="quiet" data-reroll="1">Different three</button><button class="quiet" data-heavy="1">'+(heavy?'Go lighter':'Go heavier')+'</button>')+'</div>'+(heavy&&hv>=3?'<p class="note" style="padding:0 2px">Four or more heavy actions in a week is usually overcompensation, not progress.</p>':'');
  }
  if(view==='set')body='<div class="ops-card"><div class="eyebrow">Focus set / '+S.today.c+'</div><p class="focus-text">'+esc(S.today.t)+'</p><p class="note">'+esc(S.cheer||CHEERS[0])+'</p></div><div class="btn-row"><button class="quiet" data-go="home">Close</button></div>';
  if(view==='audit')body='<div class="ops-card"><div class="eyebrow">Audit</div><p class="prompt">Did you execute today\'s micro-action?</p><div class="btn-row"><button class="primary" data-audit="yes">Yes</button><button data-audit="no">No</button></div></div><div class="btn-row"><button class="quiet" data-go="home">Back</button></div>';
  if(view==='friction')body='<div class="ops-card"><div class="eyebrow">Audit</div><p class="prompt">What was the friction point? Five words or less.</p><input type="text" id="inp" maxlength="60" placeholder="e.g. work ran over again" autocomplete="off"><div class="btn-row"><button class="primary" data-friction="1">Log and close</button></div></div>';
  if(view==='signal')body='<div class="ops-card"><div class="eyebrow">Signal</div><p class="prompt">Something she said or wanted. A few words.</p><input type="text" id="inp" maxlength="70" placeholder="e.g. dreading the review on the 8th" autocomplete="off"><p class="eyebrow" style="margin:4px 0 6px">Bring it back on</p><input type="date" id="rsf"><div class="btn-row"><button class="primary" data-signal="1">Save</button><button class="quiet" data-go="home">Back</button></div><p class="note">On that date it becomes your R option. Recall as a queue, not as a hope.</p></div>';
  if(view==='ask')body='<div class="ops-card"><div class="eyebrow flag">Direct ask</div><p class="prompt">She asked you for something. What was it?</p><input type="text" id="inp" maxlength="70" placeholder="e.g. lift to work in the rain" autocomplete="off"><div class="btn-row"><button class="primary" data-ask="yes">I said yes</button><button data-ask="no">I said no</button></div><div class="btn-row" style="margin-top:8px"><button class="quiet" data-go="home">Back</button></div><p class="note">She does not ask for much. This log is the one that counts.</p></div>';
  if(view==='drop')body='<div class="ops-card"><div class="eyebrow flag">Stopped asking</div><p class="prompt">Something she used to ask for and no longer does.</p><input type="text" id="inp" maxlength="70" placeholder="e.g. a bike ride at her tempo" autocomplete="off"><div class="btn-row"><button class="primary" data-drop="1">Save</button><button class="quiet" data-go="home">Back</button></div><p class="note">A withdrawn request is louder than a repeated one. These come back as offers, on her terms.</p></div>';

  const openSig=S.signals.filter(s=>!s.used);
  const sigHtml=S.signals.length?'<details><summary>Recall queue ('+openSig.length+' open)</summary>'+S.signals.slice(-12).reverse().map(s=>'<div class="log-line'+(s.used?' used':'')+'"><span>'+esc(s.text)+'</span><span>'+esc((s.resurface||s.date).slice(5))+'</span></div>').join('')+'</details>':'';
  const dropHtml=S.dropped.length?'<details><summary>Stopped asking ('+S.dropped.filter(x=>!x.used).length+' open)</summary>'+S.dropped.slice(-10).reverse().map(x=>'<div class="log-line'+(x.used?' used':'')+'"><span>'+esc(x.text)+'</span><span>'+esc(x.date.slice(5))+'</span></div>').join('')+'</details>':'';
  const askHtml=S.asks.length?'<details><summary>Ask log ('+yes+'/'+a14.length+' yes, 14 days)</summary>'+S.asks.slice(-12).reverse().map(x=>'<div class="log-line"><span>'+esc(x.text)+'</span><b class="'+(x.answer==='no'?'no':'')+'">'+x.answer.toUpperCase()+'</b></div>').join('')+'</details>':'';
  const frHtml=S.frictions.length?'<details><summary>Friction log ('+S.frictions.length+')</summary>'+S.frictions.slice(-8).reverse().map(f=>'<div class="log-line"><span>'+esc(f.text)+'</span><span>'+esc(f.date.slice(5))+'</span></div>').join('')+'</details>':'';

  el.innerHTML='<div class="head-row"><div><p class="ops-title">Daily Ops</p><div class="ops-date">'+d.toUpperCase()+'</div></div><div class="toggles"><button class="toggle'+(S.pablo?' on':'')+'" data-pablo="1">Pablo week</button><button class="toggle'+(S.away?' on':'')+'" data-away="1">Away</button></div></div>'+
  '<div class="gauge">'+gaugeRow('Presence','P')+gaugeRow('Recall','R')+gaugeRow('Boundary','B')+'</div>'+
  '<div class="strip"><span>Last served. Longer bar is better.</span><span>Asks <b'+(a14.length&&yes/a14.length<0.7?' class="low"':'')+'>'+yes+'/'+a14.length+'</b></span><span>Heavy 7d <b'+(hv>3?' class="low"':'')+'>'+hv+'</b></span></div>'+'<div class="rule"><span class="rule-k">Standing rule</span>Before you respond to a problem of hers, ask which she wants. Listening or help. Do not guess.</div>'+
  body+sigHtml+dropHtml+askHtml+frHtml+'<div class="btn-row"><button class="reset" data-reset="1">Clear all data</button></div>';
  const inp=document.getElementById('inp');if(inp)inp.focus();
}

function closeDay(status,c,w){S.history=S.history.filter(h=>h.date!==today());S.history.push({date:today(),status:status,c:c||null,w:w||1});S.history=S.history.slice(-150);S.lastAudit=today();}

el.addEventListener('click',async e=>{
  const b=e.target.closest('button');if(!b)return;
  if(b.dataset.away){S.away=!S.away;render();return save();}
  if(b.dataset.pablo){S.pablo=!S.pablo;render();return save();}
  if(b.dataset.go){view=b.dataset.go;if(view==='morning'){offered=[];heavy=false;}return render();}
  if(b.dataset.reroll){offered=pickThree(heavy);return render();}
  if(b.dataset.heavy){heavy=!heavy;offered=pickThree(heavy);return render();}
  if(b.dataset.pick!==undefined){const a=offered[+b.dataset.pick];
    S.today={date:today(),c:a.c,w:a.w||1,t:a.t,status:'set',sig:a.sig||null,drop:a.drop||null};
    S.recent=[...S.recent,a.t].slice(-12);S.cheer=CHEERS[Math.floor(Math.random()*CHEERS.length)];
    view='set';render();return save();}
  if(b.dataset.audit==='yes'){
    if(S.lastAudit!==today())S.streak+=1;
    if(S.today&&S.today.sig){const i=S.signals.findIndex(s=>s.text===S.today.sig);if(i>-1)S.signals[i].used=true;}
    if(S.today&&S.today.drop){const i=S.dropped.findIndex(s=>s.text===S.today.drop);if(i>-1)S.dropped[i].used=true;}
    closeDay('done',S.today?S.today.c:null,S.today?S.today.w:1);
    if(S.today)S.today.status='done';else S.today={date:today(),status:'done'};
    view='home';render();return save();}
  if(b.dataset.audit==='no'){view='friction';return render();}
  if(b.dataset.friction){const v=(document.getElementById('inp').value||'not recorded').trim();
    S.frictions.push({date:today(),text:v.slice(0,60)});S.streak=0;
    closeDay('missed',S.today?S.today.c:null,S.today?S.today.w:1);
    if(S.today)S.today.status='missed';else S.today={date:today(),status:'missed'};
    view='home';render();return save();}
  if(b.dataset.signal){const v=(document.getElementById('inp').value||'').trim();if(!v){document.getElementById('inp').focus();return;}
    S.signals.push({date:today(),text:v.slice(0,70),resurface:document.getElementById('rsf').value||'',used:false});
    S.signals=S.signals.slice(-40);view='home';render();return save();}
  if(b.dataset.drop){const v=(document.getElementById('inp').value||'').trim();if(!v){document.getElementById('inp').focus();return;}
    S.dropped.push({date:today(),text:v.slice(0,70),used:false});S.dropped=S.dropped.slice(-25);
    view='home';render();return save();}
  if(b.dataset.ask){const v=(document.getElementById('inp').value||'unrecorded').trim();
    S.asks.push({date:today(),text:v.slice(0,70),answer:b.dataset.ask});S.asks=S.asks.slice(-60);
    view='home';render();return save();}
  if(b.dataset.reset){S={...blank};view='home';render();return save();}
});
el.addEventListener('keydown',e=>{if(e.key==='Enter'&&e.target.id==='inp'){const btn=el.querySelector('[data-friction],[data-signal],[data-drop]');if(btn)btn.click();}});
load();
</script>
