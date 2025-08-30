<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Fake News Detector + Resume Screening — B.Tech Project</title>
  <meta name="description" content="Frontend demo: Fake news detection and resume screening AI. Drop into GitHub as index.html." />
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
  <style>
    :root{--bg:#071029;--card:#0b1530;--muted:#9fb0e6;--text:#e9f0ff;--accent:#6ea8ff}
    *{box-sizing:border-box}
    body{margin:0;font-family:Inter,system-ui,-apple-system,Segoe UI,Roboto,Arial;background:linear-gradient(180deg,#041025,#071733);color:var(--text);min-height:100vh}
    .wrap{max-width:1100px;margin:28px auto;padding:18px}
    header{display:flex;align-items:center;justify-content:space-between}
    .title{font-weight:800;font-size:20px}
    .sub{color:var(--muted);font-size:13px}
    .grid{display:grid;grid-template-columns:1fr 1fr;gap:16px;margin-top:18px}
    @media(max-width:980px){.grid{grid-template-columns:1fr}}
    .card{background:linear-gradient(180deg,#0b1530,#08173a);border:1px solid rgba(110,168,255,0.06);padding:16px;border-radius:12px}
    label{font-size:13px;color:var(--muted)}
    textarea,input,select{width:100%;padding:10px;border-radius:8px;border:1px solid rgba(255,255,255,0.04);background:transparent;color:var(--text);outline:none}
    .row{display:flex;gap:10px;margin-top:10px}
    .btn{background:linear-gradient(90deg,var(--accent),#9dd7ff);color:#03102b;padding:10px 12px;border-radius:10px;border:none;cursor:pointer;font-weight:700}
    .btn.ghost{background:transparent;border:1px solid rgba(255,255,255,0.04);color:var(--muted)}
    .messages{max-height:320px;overflow:auto;padding:8px;display:flex;flex-direction:column;gap:8px;margin-top:8px}
    .result{padding:12px;border-radius:10px;background:#071a33;border:1px solid rgba(255,255,255,0.03)}
    .mono{font-family:ui-monospace,Menlo,Consolas,monospace;color:#bcd6ff}
    footer{margin-top:18px;color:var(--muted);font-size:12px}
  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <div>
        <div class="title">NLP Suite — Fake News Detection & Resume Screening</div>
        <div class="sub">Frontend prototype for B.Tech (AI & DS) final project. Publish to GitHub Pages as index.html.</div>
      </div>
      <div class="mono">v1.0</div>
    </header>

    <div class="grid">
      <!-- Fake News -->
      <section class="card" id="fake-card">
        <h2>📰 Fake News Detection</h2>
        <p class="sub">Paste an article or URL (text only). Local demo uses keyword heuristics + readability signals. Swap to backend for real model (transformer).</p>

        <div style="margin-top:8px">
          <label for="article">Article text</label>
          <textarea id="article" rows="8" placeholder="Paste news article text here..."></textarea>
        </div>

        <div class="row">
          <button class="btn" id="btn-classify">Classify</button>
          <button class="btn ghost" id="btn-clear-article">Clear</button>
          <select id="fn-mode" style="width:220px">
            <option value="local">Local heuristic</option>
            <option value="api">Use /api/fakenews (POST)</option>
          </select>
        </div>

        <div style="margin-top:10px" id="fn-result" class="result">Result will appear here.</div>
      </section>

      <!-- Resume Screening -->
      <section class="card" id="resume-card">
        <h2>📄 Resume Screening</h2>
        <p class="sub">Paste job description and upload plain‑text resumes (.txt) or paste resumes. Local demo ranks resumes by keyword overlap. Backend endpoint expected: /api/resume/screen</p>

        <div style="margin-top:8px">
          <label for="jd">Job Description</label>
          <textarea id="jd" rows="5" placeholder="Paste the job description or role requirements here... e.g., 'Python, NLP, SQL, ML deployment' "></textarea>
        </div>

        <div style="margin-top:8px">
          <label for="res-files">Upload resume text files (.txt)</label>
          <input id="res-files" type="file" accept=".txt" multiple />
        </div>

        <div style="margin-top:8px">
          <label for="paste-resume">Or paste a resume</label>
          <textarea id="paste-resume" rows="4" placeholder="Name:...\nExperience:...\nSkills:... (optional)"></textarea>
        </div>

        <div class="row" style="margin-top:8px">
          <button class="btn" id="btn-screen">Screen Resumes</button>
          <button class="btn ghost" id="btn-export-scores">Export CSV</button>
          <select id="rs-mode" style="width:220px">
            <option value="local">Local overlap scorer</option>
            <option value="api">Use /api/resume/screen</option>
          </select>
        </div>

        <div style="margin-top:10px" id="rs-results" class="result">Screening results will appear here.</div>
      </section>
    </div>

    <section class="card" style="margin-top:18px">
      <h2>📜 Activity Log</h2>
      <div id="log" class="mono" style="white-space:pre-wrap;max-height:180px;overflow:auto;padding:8px"></div>
    </section>

    <footer>README inside this file. API contracts included. License: MIT.</footer>
  </div>

  <!--
  README (for GitHub)
  ===================
  Project: NLP Suite — Fake News Detection & Resume Screening
  - This single-file frontend demonstrates UI and local-mock logic for two NLP tasks.
  - For production, implement backend endpoints and replace local heuristics with trained models (transformers for fake-news; fine-tuned resume-ranker or BERT/SentenceTransformers + cosine similarity for resume ranking).

  API Contracts (suggested)
  1) POST /api/fakenews
     Body: { text: string }
     Response: { label: 'real'|'fake', score: float, explanations: [string] }

  2) POST /api/resume/screen
     Body: { jd: string, resumes: [{id, text}] }
     Response: { results: [{id, score, highlights:[string]}] }

  How to publish on GitHub Pages:
  - Create a new repo, add this file as index.html in the root, push to main, enable Pages from main branch (root). GitHub will provide a URL.

  Ethics & fairness:
  - Resume screening must be audited for bias. Do not use protected attributes (gender, ethnicity, age) in automated decisions.
  - Fake news models should include uncertainty, explainability, and avoid overconfident labels.
  -->

  <script>
    // ===== Utilities =====
    const $ = s=>document.querySelector(s);
    const log = m=>{ const el = $('#log'); el.textContent += `[${new Date().toLocaleTimeString()}] ${m}\n`; el.scrollTop = el.scrollHeight; };

    // ===== Fake News: local heuristic =====
    const FN_TRIGGER = ['clickbait','shocking','miracle','unbelievable','secret','never','won','free','conspiracy','hoax','fake','cure'];
    const FN_SOURCES = ['https://','http://','.com','.net','.org'];

    function fakeNewsHeuristic(text){
      const t = text.toLowerCase();
      let score=0; const reasons=[];
      FN_TRIGGER.forEach(w=>{ if(t.includes(w)) { score -= 1; reasons.push('Clickbait / sensational language: "'+w+'"'); } });
      // many uppercase words
      const caps = (text.match(/[A-Z]{3,}/g) || []).length; if(caps>2){ score -= 0.5; reasons.push('Excessive uppercase words'); }
      // too short / no source
      const hasSource = FN_SOURCES.some(s=>t.includes(s)); if(!hasSource){ score -= 0.5; reasons.push('No clear sources/links'); }
      // check quotes of celebrities without source
      if(t.split(' ').length < 30) { score -= 0.4; reasons.push('Very short article'); }
      // simple readability: many exclamation marks
      const ex = (text.match(/!/g)||[]).length; if(ex>2){ score -= 0.3; reasons.push('Excessive exclamation marks'); }
      // clamp
      const raw = score; const normalized = Math.max(-3, Math.min(3, raw));
      const probFake = Math.min(0.99, Math.max(0.01, 0.5 + normalized*0.12));
      const label = probFake>0.6? 'fake' : (probFake<0.4? 'real' : 'uncertain');
      return { label, score: probFake, reasons };
    }

    $('#btn-classify').addEventListener('click', async ()=>{
      const text = $('#article').value.trim(); if(!text){ alert('Paste article text first'); return; }
      const mode = $('#fn-mode').value;
      $('#fn-result').textContent = 'Classifying…'; log('FakeNews: classify requested');
      if(mode==='local'){
        await sleep(300);
        const r = fakeNewsHeuristic(text);
        $('#fn-result').innerHTML = `<strong>Label:</strong> ${r.label.toUpperCase()}<br/><strong>Score:</strong> ${r.score.toFixed(2)}<br/><strong>Reasons:</strong><ul>${r.reasons.map(x=>`<li>${x}</li>`).join('')}</ul>`;
        log('FakeNews: local result '+r.label);
      }else{
        try{
          const res = await fetch('/api/fakenews',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({text})});
          const j = await res.json(); $('#fn-result').textContent = JSON.stringify(j,null,2);
          log('FakeNews: API response');
        }catch(err){ $('#fn-result').textContent='(API error)'; log('FakeNews API error: '+err.message); }
      }
    });

    $('#btn-clear-article').addEventListener('click', ()=>{ $('#article').value=''; $('#fn-result').textContent='Result will appear here.'; });

    function sleep(ms){ return new Promise(r=>setTimeout(r,ms)); }

    // ===== Resume Screening: local overlap scorer =====
    async function readFilesAsText(files){ const arr = []; for(const f of files){ const txt = await f.text(); arr.push({name: f.name, text: txt}); } return arr; }

    function tokenize(s){ return s.toLowerCase().replace(/[^a-z0-9\s]/gi,' ').split(/\s+/).filter(Boolean); }

    function scoreResume(jdTokens, resumeText){ const rTokens = tokenize(resumeText); const set = new Set(rTokens); let overlap=0; const highlights=[]; jdTokens.forEach(t=>{ if(set.has(t)){ overlap++; highlights.push(t); } }); const score = overlap / Math.max(1, jdTokens.length); return { score: Number(score.toFixed(3)), highlights: Array.from(new Set(highlights)).slice(0,10) } }

    $('#btn-screen').addEventListener('click', async ()=>{
      const jd = $('#jd').value.trim(); if(!jd){ alert('Paste job description first'); return; }
      const mode = $('#rs-mode').value; const jdTokens = tokenize(jd);
      log('ResumeScreen: screening started');
      if(mode==='local'){
        const files = $('#res-files').files; const pasted = $('#paste-resume').value.trim(); let resumes = [];
        if(files && files.length>0){ resumes = resumes.concat(await readFilesAsText(files)); }
        if(pasted) resumes.push({name:'pasted_resume', text: pasted});
        if(resumes.length===0){ alert('Upload or paste at least one resume'); return; }
        const results = resumes.map(r=>{ const sc = scoreResume(jdTokens, r.text); return {id: r.name, score: sc.score, highlights: sc.highlights}; }).sort((a,b)=>b.score-a.score);
        $('#rs-results').innerHTML = `<strong>Ranked candidates:</strong><ol>${results.map(r=>`<li><strong>${r.id}</strong> — score: ${r.score}<br/>Highlights: ${r.highlights.join(', ')}</li>`).join('')}</ol>`;
        window.latestScreen = results; $('#btn-export-scores').disabled = false; log('ResumeScreen: local results ready');
      }else{
        try{
          // collect resumes
          const files = $('#res-files').files; const resumes = [];
          if(files && files.length>0){ const arr = await readFilesAsText(files); arr.forEach((a,i)=>resumes.push({id:a.name, text:a.text})); }
          if($('#paste-resume').value.trim()) resumes.push({id:'pasted', text: $('#paste-resume').value.trim()});
          const res = await fetch('/api/resume/screen',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({jd, resumes})});
          const j = await res.json(); $('#rs-results').textContent = JSON.stringify(j, null, 2); log('ResumeScreen: API response');
        }catch(err){ $('#rs-results').textContent='(API error)'; log('ResumeScreen API error: '+err.message); }
      }
    });

    $('#btn-export-scores').addEventListener('click', ()=>{
      const data = window.latestScreen; if(!data){ alert('No results to export'); return; }
      let csv = 'id,score,highlights\n'; data.forEach(r=>{ csv += `${r.id},${r.score},"${r.highlights.join('; ')}"\n`; });
      const blob = new Blob([csv],{type:'text/csv'}); const url = URL.createObjectURL(blob); const a=document.createElement('a'); a.href=url; a.download='resume_scores.csv'; a.click(); URL.revokeObjectURL(url); log('Resume scores exported');
    });

    // init
    log('NLP demo loaded — ready.');
  </script>
</body>
</html>
