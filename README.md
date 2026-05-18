<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Verificador de Contratos — Portalia Desarrollos Inteligentes</title>
<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --gold:#FFB548;--gold-d:#e8a030;--gold-lt:#fff3dc;--gold-glow:rgba(255,181,72,0.15);--gold-tr:rgba(255,181,72,0.1);
  --gray:#58595B;--gray-d:#3e3f41;--gray-l:#8a8b8d;
  --bg:#f2f2f0;--surface:#fff;--surface2:#f8f8f6;--surface3:#f0f0ee;
  --border:#e0e0dc;--border2:#ccccca;
  --text:#222;--text2:#58595B;--text3:#8a8b8d;
  --err:#d64545;--err-bg:#fff0f0;--err-b:#ffd0d0;
  --warn:#c47c00;--warn-bg:#fff8e6;--warn-b:#ffe0a0;
  --ok:#1f8a5e;--ok-bg:#edfaf4;--ok-b:#a8e6cc;
  --r:12px;--rs:8px;--rxs:5px;
}
*{-webkit-font-smoothing:antialiased}
body{font-family:'Montserrat',sans-serif;background:var(--bg);color:var(--text);min-height:100vh}
::-webkit-scrollbar{width:5px}::-webkit-scrollbar-track{background:transparent}::-webkit-scrollbar-thumb{background:var(--border2);border-radius:10px}

/* HEADER */
header{position:sticky;top:0;z-index:100;background:var(--gray);height:64px;display:flex;align-items:center;justify-content:space-between;padding:0 2rem;box-shadow:0 2px 12px rgba(0,0,0,.15)}
.logo{display:flex;align-items:center;gap:10px}
.logo-bars{display:flex;align-items:flex-end;gap:3px}
.bar{background:var(--gold);border-radius:1px 1px 0 0}
.b1{width:6px;height:10px}.b2{width:7px;height:16px}.b3{width:8px;height:22px}
.logo-txt{display:flex;flex-direction:column;line-height:1}
.logo-name{font-size:20px;font-weight:800;color:#fff;letter-spacing:.04em}
.logo-name span{color:var(--gold)}
.logo-sub{font-size:7px;font-weight:700;color:var(--gold);letter-spacing:.18em;text-transform:uppercase;margin-top:2px}
.logo-since{font-size:7px;font-weight:600;color:rgba(255,255,255,.4);letter-spacing:.1em;text-transform:uppercase;margin-top:1px}
.hbadge{font-size:10px;font-weight:800;background:var(--gold);color:var(--gray);padding:4px 12px;border-radius:20px;letter-spacing:.05em}

/* MAIN */
main{max-width:1300px;margin:0 auto;padding:2rem 1.5rem}

/* HERO */
.hero{background:var(--gray);border-radius:var(--r);padding:1.75rem 2rem;margin-bottom:1.75rem;display:flex;align-items:center;justify-content:space-between;gap:1rem;overflow:hidden;position:relative}
.hero::after{content:'';position:absolute;right:-30px;top:-30px;width:180px;height:180px;background:var(--gold);opacity:.05;border-radius:50%}
.hero-eyebrow{font-size:10px;font-weight:700;color:var(--gold);letter-spacing:.2em;text-transform:uppercase;margin-bottom:8px;display:flex;align-items:center;gap:8px}
.hero-eyebrow::before{content:'';width:16px;height:2px;background:var(--gold);border-radius:2px}
.hero-title{font-size:26px;font-weight:800;color:#fff;letter-spacing:-.01em;margin-bottom:6px}
.hero-title span{color:var(--gold)}
.hero-desc{font-size:12px;color:rgba(255,255,255,.5);line-height:1.7;max-width:440px}
.hero-stats{display:flex;gap:2rem;flex-shrink:0}
.hstat-val{font-size:24px;font-weight:800;color:var(--gold);text-align:center}
.hstat-lbl{font-size:9px;font-weight:700;color:rgba(255,255,255,.4);letter-spacing:.08em;text-transform:uppercase;text-align:center;margin-top:2px}

/* API BOX */
.apibox{background:var(--surface);border:1px solid var(--border);border-left:4px solid var(--gold);border-radius:var(--r);padding:1rem 1.5rem;margin-bottom:1.5rem;display:flex;align-items:center;gap:1.5rem;flex-wrap:wrap}
.api-lbl{font-size:12px;font-weight:700;color:var(--text2);white-space:nowrap;display:flex;align-items:center;gap:6px}
.api-row{display:flex;gap:8px;flex:1;min-width:200px}
.api-input{flex:1;padding:9px 12px;background:var(--surface2);border:1.5px solid var(--border);border-radius:var(--rs);font-family:'Montserrat',monospace;font-size:11.5px;color:var(--text);outline:none;transition:border-color .2s}
.api-input:focus{border-color:var(--gold)}
.api-input::placeholder{color:var(--text3)}
.api-note{font-size:11px;color:var(--text3);font-weight:500;white-space:nowrap}

/* GRID */
.grid2{display:grid;grid-template-columns:1fr 1fr;gap:1.5rem;margin-bottom:1.5rem}
@media(max-width:900px){.grid2,.results-grid{grid-template-columns:1fr!important}header{padding:0 1rem}main{padding:1.25rem 1rem}.hero{flex-direction:column}.hero-stats{gap:1.5rem}}

/* PANEL */
.panel{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);overflow:hidden;display:flex;flex-direction:column;box-shadow:0 1px 4px rgba(0,0,0,.04)}
.panel-hdr{background:var(--gray);padding:.85rem 1.25rem;display:flex;align-items:center;justify-content:space-between}
.panel-ttl{font-size:12px;font-weight:700;color:#fff;letter-spacing:.06em;text-transform:uppercase;display:flex;align-items:center;gap:7px}
.panel-ttl::before{content:'';width:8px;height:8px;background:var(--gold);border-radius:2px;flex-shrink:0}
.panel-count{font-size:11px;font-weight:600;color:rgba(255,255,255,.4)}
.panel-body{padding:1.25rem;flex:1;overflow-y:auto}

/* DROP ZONE */
.dz{border:2px dashed var(--border2);border-radius:var(--rs);padding:1.75rem 1rem;text-align:center;cursor:pointer;transition:all .2s;position:relative;background:var(--surface2)}
.dz:hover,.dz.over{border-color:var(--gold);background:var(--gold-tr)}
.dz input[type=file]{position:absolute;inset:0;opacity:0;cursor:pointer;width:100%;height:100%}
.dz-icon{font-size:24px;margin-bottom:6px;display:block}
.dz-text{font-size:13px;font-weight:700;color:var(--text2);margin-bottom:3px}
.dz-hint{font-size:11px;color:var(--text3)}
.file-list{margin-top:10px;display:flex;flex-direction:column;gap:5px}
.fitem{display:flex;align-items:center;gap:8px;background:var(--surface2);border:1px solid var(--border);border-radius:var(--rxs);padding:7px 10px;font-size:11.5px}
.fdot{width:7px;height:7px;border-radius:50%;flex-shrink:0;transition:all .3s}
.fdot.ready{background:var(--ok);box-shadow:0 0 5px rgba(31,138,94,.4)}
.fdot.loading{background:var(--gold);animation:blink .8s infinite}
@keyframes blink{0%,100%{opacity:1}50%{opacity:.2}}
.fname{flex:1;font-weight:600;color:var(--text2);white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.fsize{color:var(--text3);font-size:11px;flex-shrink:0}
.frm{background:none;border:none;cursor:pointer;color:var(--text3);font-size:16px;padding:0 2px;line-height:1;transition:color .15s}
.frm:hover{color:var(--err)}

/* PASTE BTN */
.paste-btn{width:100%;margin-bottom:1rem;padding:10px 14px;background:var(--gold-lt);border:1.5px solid var(--gold);border-radius:var(--rs);font-family:'Montserrat',sans-serif;font-size:11px;font-weight:800;color:var(--gray);cursor:pointer;transition:all .2s;display:flex;align-items:center;justify-content:center;gap:8px;letter-spacing:.04em;text-transform:uppercase}
.paste-btn:hover{background:var(--gold);transform:translateY(-1px);box-shadow:0 4px 12px var(--gold-glow)}

/* FORM */
.cform{max-height:450px;overflow-y:auto;padding-right:2px}
.cform::-webkit-scrollbar-thumb{background:var(--border2)}
.fsect{font-size:10px;font-weight:800;text-transform:uppercase;letter-spacing:.12em;color:var(--gold-d);margin-bottom:10px;padding-bottom:6px;border-bottom:2px solid var(--gold-lt)}
.fgrid{display:grid;grid-template-columns:1fr 1fr;gap:7px;margin-bottom:14px}
.ff{display:flex;flex-direction:column;gap:3px}
.ff.full{grid-column:1/-1}
.ff label{font-size:10px;font-weight:700;color:var(--text3);text-transform:uppercase;letter-spacing:.07em}
.ff input,.ff select{padding:8px 10px;background:var(--surface2);border:1.5px solid var(--border);border-radius:var(--rxs);font-family:'Montserrat',sans-serif;font-size:12px;font-weight:500;color:var(--text);outline:none;width:100%;transition:border-color .15s;-webkit-appearance:none}
.ff input:focus,.ff select:focus{border-color:var(--gold)}
.ff input::placeholder{color:var(--text3);font-weight:400}
.ff input.filled{border-color:var(--ok);background:var(--ok-bg);animation:flash .5s ease}
@keyframes flash{0%{background:#d4fae8}100%{background:var(--ok-bg)}}

/* ANALYZE BTN */
.analyze-btn{width:100%;padding:15px;margin-bottom:2rem;background:var(--gold);color:var(--gray);border:none;border-radius:var(--rs);font-family:'Montserrat',sans-serif;font-size:13px;font-weight:800;letter-spacing:.07em;text-transform:uppercase;cursor:pointer;transition:all .25s;display:flex;align-items:center;justify-content:center;gap:10px;box-shadow:0 4px 16px var(--gold-glow)}
.analyze-btn:hover:not(:disabled){background:var(--gold-d);transform:translateY(-2px);box-shadow:0 8px 24px rgba(255,181,72,.3)}
.analyze-btn:disabled{opacity:.35;cursor:not-allowed;transform:none;box-shadow:none}

/* LOADING */
.loading{display:none;background:var(--surface);border:1px solid var(--border);border-top:4px solid var(--gold);border-radius:var(--r);padding:2.5rem 2rem;text-align:center;margin-bottom:2rem}
.loading.active{display:block}
.spinner{width:42px;height:42px;border:3px solid var(--gold-lt);border-top-color:var(--gold);border-radius:50%;animation:spin .8s linear infinite;margin:0 auto 1rem}
@keyframes spin{to{transform:rotate(360deg)}}
.load-title{font-size:15px;font-weight:800;color:var(--gray);margin-bottom:4px}
.load-sub{font-size:12px;color:var(--text3);font-weight:500;margin-bottom:1.5rem}
.load-steps{display:flex;justify-content:center;gap:2rem;flex-wrap:wrap}
.lstep{display:flex;align-items:center;gap:6px;font-size:10px;font-weight:700;color:var(--text3);text-transform:uppercase;letter-spacing:.07em}
.sdot{width:8px;height:8px;border-radius:50%;background:var(--border2);transition:all .3s;flex-shrink:0}
.sdot.active{background:var(--gold);box-shadow:0 0 8px var(--gold-glow);animation:pulse .9s infinite}
.sdot.done{background:var(--ok)}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.35}}

/* RESULTS */
#results{display:none}
#results.show{display:block;animation:fadeUp .35s ease}
@keyframes fadeUp{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:translateY(0)}}
.sum-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:1rem;margin-bottom:1.5rem}
.scard{background:var(--surface);border:1px solid var(--border);border-top:4px solid var(--border);border-radius:var(--r);padding:1.1rem 1.25rem;box-shadow:0 1px 4px rgba(0,0,0,.04)}
.scard.s-gold{border-top-color:var(--gold)}.scard.s-err{border-top-color:var(--err)}.scard.s-warn{border-top-color:var(--warn)}.scard.s-ok{border-top-color:var(--ok)}
.scard-lbl{font-size:10px;font-weight:700;color:var(--text3);text-transform:uppercase;letter-spacing:.1em;margin-bottom:7px}
.scard-val{font-size:30px;font-weight:800;color:var(--gray);line-height:1}
.scard-val.gold{color:var(--gold-d)}.scard-val.red{color:var(--err)}.scard-val.amber{color:var(--warn)}.scard-val.green{color:var(--ok)}
.scard-val sup{font-size:13px;color:var(--text3);font-weight:500}
.act-row{display:flex;gap:10px;flex-wrap:wrap;margin-bottom:1.5rem}
.results-grid{display:grid;grid-template-columns:1fr 1fr;gap:1.5rem}
.rpanel{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);overflow:hidden;display:flex;flex-direction:column}
.rpanel-hdr{display:flex;align-items:center;justify-content:space-between;padding:.8rem 1.25rem;background:var(--gray)}
.rpanel-ttl{font-size:11px;font-weight:700;color:#fff;letter-spacing:.07em;text-transform:uppercase;display:flex;align-items:center;gap:7px}
.rpanel-ttl::before{content:'';width:8px;height:8px;background:var(--gold);border-radius:2px;flex-shrink:0}
.rbadge{font-size:10px;font-weight:800;padding:3px 10px;border-radius:20px;letter-spacing:.04em;text-transform:uppercase}
.rb-blue{background:rgba(255,181,72,.15);color:var(--gold-d);border:1px solid rgba(255,181,72,.3)}
.rb-err{background:var(--err-bg);color:var(--err);border:1px solid var(--err-b)}
.rb-ok{background:var(--ok-bg);color:var(--ok);border:1px solid var(--ok-b)}
.tab-bar{display:flex;background:var(--surface3);border-bottom:1px solid var(--border);padding:0 1.25rem}
.tab-btn{background:none;border:none;border-bottom:2px solid transparent;padding:8px 12px;margin-bottom:-1px;font-family:'Montserrat',sans-serif;font-size:10px;font-weight:700;color:var(--text3);cursor:pointer;transition:all .15s;letter-spacing:.07em;text-transform:uppercase}
.tab-btn.active{color:var(--gold-d);border-bottom-color:var(--gold)}
.tab-c{display:none}.tab-c.active{display:block}
.pbody{padding:1.25rem;max-height:500px;overflow-y:auto;flex:1}
.pbody::-webkit-scrollbar-thumb{background:var(--border2)}
.ctext{font-family:'Montserrat',monospace;font-size:11px;line-height:1.9;color:var(--text2);white-space:pre-wrap;word-break:break-word;font-weight:400}
.herr{background:var(--err-bg);border-bottom:2px solid var(--err);color:var(--err);border-radius:3px;padding:0 3px;font-weight:600;cursor:pointer}
.hwarn{background:var(--warn-bg);border-bottom:2px solid var(--warn);color:var(--warn);border-radius:3px;padding:0 3px;font-weight:600;font-style:italic;cursor:pointer}
.hok{background:var(--ok-bg);border-bottom:2px solid var(--ok);color:var(--ok);border-radius:3px;padding:0 3px;font-weight:600}
.legend{display:flex;gap:1rem;flex-wrap:wrap;padding:9px 1.25rem;border-top:1px solid var(--border);background:var(--surface2)}
.li{display:flex;align-items:center;gap:5px;font-size:10px;font-weight:700;color:var(--text3);letter-spacing:.06em;text-transform:uppercase}
.ld{width:10px;height:3px;border-radius:2px}
.frow{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:12px}
.fpill{padding:5px 11px;border-radius:20px;font-family:'Montserrat',sans-serif;font-size:10px;font-weight:700;cursor:pointer;border:1.5px solid var(--border2);background:transparent;color:var(--text3);transition:all .15s;letter-spacing:.04em;text-transform:uppercase}
.fp-all{background:var(--gray);color:#fff;border-color:var(--gray)}
.fp-err{background:var(--err-bg);color:var(--err);border-color:var(--err-b)}
.fp-warn{background:var(--warn-bg);color:var(--warn);border-color:var(--warn-b)}
.fp-ok{background:var(--ok-bg);color:var(--ok);border-color:var(--ok-b)}
.issue{border:1px solid var(--border);border-left:3px solid var(--border2);border-radius:var(--rxs);padding:10px 12px;margin-bottom:7px;transition:transform .15s}
.issue:hover{transform:translateX(2px)}
.issue-err{border-color:var(--err-b);border-left-color:var(--err);background:var(--err-bg)}
.issue-warn{border-color:var(--warn-b);border-left-color:var(--warn);background:var(--warn-bg)}
.issue-ok{border-color:var(--ok-b);border-left-color:var(--ok);background:var(--ok-bg)}
.issue-ttl{font-size:12px;font-weight:700;color:var(--text);margin-bottom:4px}
.issue-det{font-size:11px;color:var(--text3);line-height:1.5;font-weight:500}
.found{color:var(--err);font-weight:700}.expected{color:var(--ok);font-weight:700}
.empty-st{text-align:center;padding:2.5rem 1rem;color:var(--text3);font-size:12px;font-weight:600;text-transform:uppercase;letter-spacing:.06em}

/* BTNS */
.btn-ghost{padding:9px 16px;background:var(--surface);border:1.5px solid var(--border2);border-radius:var(--rs);font-family:'Montserrat',sans-serif;font-size:11px;font-weight:700;color:var(--text2);cursor:pointer;transition:all .15s;display:flex;align-items:center;gap:6px;letter-spacing:.04em;text-transform:uppercase}
.btn-ghost:hover{border-color:var(--gold);color:var(--gray);background:var(--gold-lt)}
.btn-solid{padding:9px 16px;background:var(--gray);border:none;border-radius:var(--rs);font-family:'Montserrat',sans-serif;font-size:11px;font-weight:700;color:#fff;cursor:pointer;transition:all .15s;display:flex;align-items:center;gap:6px;letter-spacing:.04em;text-transform:uppercase}
.btn-solid:hover{background:var(--gray-d);transform:translateY(-1px)}

/* MODAL */
.modal-bg{display:none;position:fixed;inset:0;background:rgba(40,40,40,.65);z-index:9999;align-items:center;justify-content:center;padding:1rem}
.modal-bg.open{display:flex}
.modal-box{background:var(--surface);border:1px solid var(--border);border-top:4px solid var(--gold);border-radius:var(--r);width:100%;max-width:580px;box-shadow:0 20px 60px rgba(0,0,0,.2);animation:mIn .2s ease}
@keyframes mIn{from{opacity:0;transform:scale(.97) translateY(6px)}to{opacity:1;transform:scale(1) translateY(0)}}
.modal-hdr{display:flex;align-items:center;justify-content:space-between;padding:1rem 1.5rem;background:var(--gray)}
.modal-ttl{font-size:13px;font-weight:800;color:#fff;display:flex;align-items:center;gap:8px;letter-spacing:.04em;text-transform:uppercase}
.modal-ttl::before{content:'';width:8px;height:8px;background:var(--gold);border-radius:2px}
.modal-close{background:none;border:none;font-size:22px;cursor:pointer;color:rgba(255,255,255,.5);padding:2px 6px;border-radius:4px;line-height:1;transition:color .15s;font-family:sans-serif}
.modal-close:hover{color:#fff}
.modal-body{padding:1.5rem}
.modal-hint{font-size:12px;color:var(--text3);background:var(--gold-lt);border:1px solid rgba(255,181,72,.25);border-radius:var(--rxs);padding:11px 13px;margin-bottom:12px;line-height:1.6;font-weight:500}
.paste-area{width:100%;height:220px;padding:12px;background:var(--surface2);border:1.5px solid var(--border);border-radius:var(--rs);font-family:'Montserrat',sans-serif;font-size:13px;color:var(--text);resize:vertical;outline:none;line-height:1.7;font-weight:400;transition:border-color .15s;-webkit-user-select:text;user-select:text}
.paste-area:focus{border-color:var(--gold)}
.paste-area::placeholder{color:var(--text3)}
.modal-foot{display:flex;gap:10px;justify-content:flex-end;padding:1rem 1.5rem;border-top:1px solid var(--border);background:var(--surface2)}
.pind{display:none;align-items:center;gap:8px;font-size:11px;font-weight:700;color:var(--gray-d);padding:8px 12px;background:var(--gold-lt);border:1px solid rgba(255,181,72,.3);border-radius:var(--rxs);margin-top:10px;letter-spacing:.04em;text-transform:uppercase}
.pind.show{display:flex}
.mspin{width:14px;height:14px;border:2px solid rgba(255,181,72,.3);border-top-color:var(--gold);border-radius:50%;animation:spin .7s linear infinite;flex-shrink:0}

/* HIGHLIGHT ACTIVE */
.herr.active-hl,.hwarn.active-hl,.hok.active-hl{
  outline:3px solid var(--gold);
  outline-offset:2px;
  border-radius:4px;
  animation:hl-flash .5s ease;
}
@keyframes hl-flash{0%{box-shadow:0 0 0 6px var(--gold-glow)}100%{box-shadow:none}}

/* ISSUE CLICKABLE */
.issue{cursor:pointer}
.issue.active-issue{outline:2px solid var(--gold);outline-offset:2px}

/* TOOLTIP */
.tip{position:fixed;background:var(--gray);border:1px solid var(--gray-d);color:#fff;border-radius:8px;padding:9px 13px;font-size:12px;max-width:220px;z-index:99999;pointer-events:none;opacity:0;transition:opacity .15s;line-height:1.5;box-shadow:0 8px 24px rgba(0,0,0,.2)}
.tip.show{opacity:1}
.tip-lbl{font-size:10px;color:var(--gold);text-transform:uppercase;letter-spacing:.08em;margin-bottom:3px;font-weight:800}

/* TOAST */
.toast{position:fixed;top:74px;right:20px;background:var(--gray);border:1px solid var(--gray-d);color:#fff;padding:10px 16px;border-radius:10px;font-size:12px;font-weight:600;z-index:99998;transform:translateX(130%);transition:transform .3s cubic-bezier(.34,1.56,.64,1);box-shadow:0 8px 24px rgba(0,0,0,.15);max-width:300px}
.toast.show{transform:translateX(0)}

/* FOOTER */
footer{background:var(--gray);text-align:center;padding:1rem;margin-top:2.5rem}
.foot-logo{display:flex;align-items:center;justify-content:center;gap:7px;margin-bottom:3px}
.fbars{display:flex;align-items:flex-end;gap:2px}
.fb{background:var(--gold);border-radius:1px 1px 0 0}
.fb1{width:4px;height:7px}.fb2{width:5px;height:11px}.fb3{width:6px;height:15px}
.foot-name{font-size:12px;font-weight:800;color:#fff;letter-spacing:.06em;text-transform:uppercase}
.foot-name span{color:var(--gold)}
.foot-copy{font-size:10px;color:rgba(255,255,255,.3);letter-spacing:.06em;font-weight:500}
</style>
</head>
<body>

<header>
  <div class="logo">
    <div class="logo-bars"><div class="bar b1"></div><div class="bar b2"></div><div class="bar b3"></div></div>
    <div class="logo-txt">
      <div class="logo-name">PORTAL<span>I</span>A</div>
      <div class="logo-sub">Desarrollos Inteligentes</div>
      <div class="logo-since">Desde 2009</div>
    </div>
  </div>
  <span class="hbadge">⚡ IA Verificadora</span>
</header>

<main>
  <div class="hero">
    <div>
      <div class="hero-eyebrow">Herramienta Legal Inteligente</div>
      <h1 class="hero-title">Verificador de <span>Contratos</span></h1>
      <p class="hero-desc">Sube el contrato, captura los datos correctos del cliente y la IA detecta errores e inconsistencias automáticamente.</p>
    </div>
    <div class="hero-stats">
      <div><div class="hstat-val">IA</div><div class="hstat-lbl">Análisis</div></div>
      <div><div class="hstat-val">100%</div><div class="hstat-lbl">Preciso</div></div>
      <div><div class="hstat-val">PDF</div><div class="hstat-lbl">Soporte</div></div>
    </div>
  </div>

  <div class="apibox">
    <div class="api-lbl">🔑 Clave API Anthropic</div>
    <div class="api-row">
      <input type="password" id="apiKey" class="api-input" placeholder="sk-ant-api...">
      <button class="btn-solid" onclick="saveKey()">Guardar</button>
    </div>
    <div class="api-note">Solo en tu navegador · Nunca se comparte</div>
  </div>

  <div class="grid2">
    <!-- CONTRATO -->
    <div class="panel">
      <div class="panel-hdr">
        <div class="panel-ttl">Contrato del cliente</div>
        <span class="panel-count" id="fileCount">Sin archivos</span>
      </div>
      <div class="panel-body">
        <div class="dz" id="dz"
          ondragover="event.preventDefault();document.getElementById('dz').classList.add('over')"
          ondragleave="document.getElementById('dz').classList.remove('over')"
          ondrop="onDrop(event)">
          <input type="file" id="fileInput" accept=".pdf,.txt" multiple onchange="onFileChange(event)">
          <span class="dz-icon">📂</span>
          <div class="dz-text">Arrastra uno o más contratos aquí</div>
          <div class="dz-hint">PDF, TXT · Múltiples archivos · Máx. 10MB c/u</div>
        </div>
        <div class="file-list" id="fileList"></div>
      </div>
    </div>

    <!-- DATOS CLIENTE -->
    <div class="panel">
      <div class="panel-hdr">
        <div class="panel-ttl">Datos correctos del cliente</div>
      </div>
      <div class="panel-body">
        <button class="paste-btn" id="pasteBtn" type="button" onclick="openModal()">
          📋 &nbsp;Pegar datos — rellenar con IA automáticamente
        </button>
        <div class="cform">
          <div class="fsect">👤 Datos personales</div>
          <div class="fgrid">
            <div class="ff full"><label>NUI</label><input id="f_nui" placeholder="Número único de identificación" oninput="chkReady()"></div>
            <div class="ff full"><label>Nombre completo</label><input id="f_nombre" placeholder="Nombre(s) Apellido Paterno Apellido Materno" oninput="chkReady()"></div>
            <div class="ff"><label>Estado civil</label>
              <select id="f_estado_civil" onchange="chkReady()">
                <option value="">— Seleccionar —</option>
                <option>Soltero(a)</option><option>Casado(a)</option><option>Divorciado(a)</option><option>Viudo(a)</option><option>Unión libre</option>
              </select>
            </div>
            <div class="ff"><label>Régimen matrimonial</label>
              <select id="f_regimen" onchange="chkReady()">
                <option value="">— Seleccionar —</option>
                <option>Sociedad conyugal</option><option>Separación de bienes</option><option>N/A</option>
              </select>
            </div>
            <div class="ff"><label>Originario de</label><input id="f_origen" placeholder="Ciudad, Estado" oninput="chkReady()"></div>
            <div class="ff"><label>Ocupación</label><input id="f_ocupacion" placeholder="Ej. Empleada, Ingeniero..." oninput="chkReady()"></div>
            <div class="ff"><label>Correo electrónico</label><input id="f_correo" type="email" placeholder="ejemplo@correo.com" oninput="chkReady()"></div>
            <div class="ff"><label>Teléfono</label><input id="f_telefono" placeholder="10 dígitos" oninput="chkReady()"></div>
            <div class="ff"><label>CURP</label><input id="f_curp" placeholder="18 caracteres" style="text-transform:uppercase" oninput="chkReady()"></div>
            <div class="ff"><label>RFC</label><input id="f_rfc" placeholder="12 o 13 caracteres" style="text-transform:uppercase" oninput="chkReady()"></div>
            <div class="ff full"><label>Domicilio completo</label><input id="f_domicilio" placeholder="Calle, Número, Col., Ciudad, C.P." oninput="chkReady()"></div>
            <div class="ff full"><label>Beneficiario</label><input id="f_beneficiario" placeholder="Nombre completo del beneficiario" oninput="chkReady()"></div>
          </div>
          <div class="fsect">🎟️ Datos del ticket</div>
          <div class="fgrid">
            <div class="ff"><label>Cantidad de tickets</label><input id="f_tickets" type="number" placeholder="Ej. 5" oninput="chkReady()"></div>
            <div class="ff"><label>Valor por ticket</label><input id="f_valor_ticket" placeholder="Ej. $407,800" oninput="chkReady()"></div>
            <div class="ff"><label>Separación / Aportación inicial</label><input id="f_separacion" placeholder="Ej. $305,850" oninput="chkReady()"></div>
            <div class="ff"><label>Esquema de pago</label><input id="f_esquema" placeholder="Ej. Contado a 90 días" oninput="chkReady()"></div>
            <div class="ff"><label>Método de pago</label>
              <select id="f_metodo_pago" onchange="chkReady()">
                <option value="">— Seleccionar —</option>
                <option>Transferencia bancaria</option><option>Cheque</option><option>Efectivo</option><option>Tarjeta de crédito</option><option>Tarjeta de débito</option>
              </select>
            </div>
            <div class="ff"><label>Firma en Notaría (fecha)</label><input id="f_fecha_notaria" type="date" oninput="chkReady()"></div>
            <div class="ff full"><label>Fechas de pago para liquidar</label><input id="f_fechas_pago" placeholder="Ej. 27 mayo 2026, agosto 2026" oninput="chkReady()"></div>
            <div class="ff full"><label>Notaría</label><input id="f_notaria" placeholder="Ej. Notaría Pública Número 29" oninput="chkReady()"></div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <button class="analyze-btn" id="analyzeBtn" type="button" onclick="analyze()" disabled>
    🔍 &nbsp;Analizar contrato
  </button>

  <div class="loading" id="loading">
    <div class="spinner"></div>
    <div class="load-title">Analizando contrato...</div>
    <div class="load-sub">Comparando cada campo con inteligencia artificial</div>
    <div class="load-steps">
      <div class="lstep"><div class="sdot" id="s1"></div>Leyendo PDF</div>
      <div class="lstep"><div class="sdot" id="s2"></div>Procesando</div>
      <div class="lstep"><div class="sdot" id="s3"></div>Comparando</div>
      <div class="lstep"><div class="sdot" id="s4"></div>Reporte</div>
    </div>
  </div>

  <div id="results">
    <div class="sum-grid" id="sumCards"></div>
    <div class="act-row">
      <button class="btn-ghost" type="button" onclick="resetAll()">↩ Nueva verificación</button>
      <button class="btn-solid" type="button" onclick="exportReport()">⬇ Exportar reporte</button>
    </div>
    <div class="results-grid">
      <div class="rpanel">
        <div class="rpanel-hdr">
          <div class="rpanel-ttl">Contrato anotado</div>
          <div id="cBadge" class="rbadge rb-blue">–</div>
        </div>
        <div class="tab-bar">
          <button class="tab-btn active" type="button" onclick="switchTab('a')">Vista marcada</button>
          <button class="tab-btn" type="button" onclick="switchTab('o')">Original</button>
        </div>
        <div class="pbody">
          <div id="ta" class="tab-c active"><div class="ctext" id="annotated"></div></div>
          <div id="to" class="tab-c"><div class="ctext" id="original"></div></div>
        </div>
        <div class="legend">
          <div class="li"><div class="ld" style="background:var(--err)"></div>Incorrecto</div>
          <div class="li"><div class="ld" style="background:var(--warn)"></div>Faltante</div>
          <div class="li"><div class="ld" style="background:var(--ok)"></div>Correcto</div>
        </div>
      </div>
      <div class="rpanel">
        <div class="rpanel-hdr">
          <div class="rpanel-ttl">Hallazgos</div>
          <div id="iBadge" class="rbadge rb-err">–</div>
        </div>
        <div class="pbody">
          <div class="frow" id="filterRow"></div>
          <div id="issuesList"></div>
        </div>
      </div>
    </div>
  </div>
</main>

<footer>
  <div class="foot-logo">
    <div class="fbars"><div class="fb fb1"></div><div class="fb fb2"></div><div class="fb fb3"></div></div>
    <div class="foot-name">PORTAL<span>I</span>A</div>
  </div>
  <div class="foot-copy">Desarrollos Inteligentes · Desde 2009 · Verificador de Contratos</div>
</footer>

<!-- MODAL -->
<div class="modal-bg" id="modalBg">
  <div class="modal-box">
    <div class="modal-hdr">
      <div class="modal-ttl">Pegar datos del cliente</div>
      <button class="modal-close" type="button" onclick="closeModal()">&#x2715;</button>
    </div>
    <div class="modal-body">
      <div class="modal-hint">
        💡 Pega los datos en cualquier formato: lista, correo, texto libre, como los tengas. La IA los interpretará y rellenará el formulario automáticamente.
      </div>
      <textarea class="paste-area" id="pasteArea" placeholder="Ejemplo:&#10;NUI 12354007&#10;Nombre: Adriana Esquivel Mireles&#10;CURP: EUMA730522MCLSRD07&#10;RFC: EUMA730522B2A&#10;Estado civil: Casada&#10;Régimen: Sociedad conyugal&#10;Originario de: Coahuila&#10;Profesión: Empleada&#10;5 tickets a $407,800 c/u&#10;Beneficiario: Luis Fernando González&#10;Notaría 29"></textarea>
      <div class="pind" id="pind">
        <div class="mspin"></div>
        Interpretando con IA...
      </div>
    </div>
    <div class="modal-foot">
      <button class="btn-ghost" type="button" onclick="closeModal()">Cancelar</button>
      <button class="btn-solid" type="button" id="parseBtn" onclick="parsePaste()">✨ Rellenar formulario</button>
    </div>
  </div>
</div>

<div class="tip" id="tip"></div>
<div class="toast" id="toast"></div>

<script>
pdfjsLib.GlobalWorkerOptions.workerSrc='https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';

// ── STATE ──────────────────────────────────────────────────────────────────
const S={files:[],texts:[],key:localStorage.getItem('portalia_key')||'',result:null};
if(S.key)document.getElementById('apiKey').value=S.key;

const FIELDS=[
  {id:'f_nui',k:'nui',label:'NUI'},
  {id:'f_nombre',k:'nombre',label:'Nombre completo'},
  {id:'f_estado_civil',k:'estado_civil',label:'Estado civil'},
  {id:'f_regimen',k:'regimen',label:'Régimen matrimonial'},
  {id:'f_origen',k:'origen',label:'Originario de'},
  {id:'f_ocupacion',k:'ocupacion',label:'Ocupación'},
  {id:'f_correo',k:'correo',label:'Correo electrónico'},
  {id:'f_telefono',k:'telefono',label:'Teléfono'},
  {id:'f_curp',k:'curp',label:'CURP'},
  {id:'f_rfc',k:'rfc',label:'RFC'},
  {id:'f_domicilio',k:'domicilio',label:'Domicilio completo'},
  {id:'f_beneficiario',k:'beneficiario',label:'Beneficiario'},
  {id:'f_tickets',k:'tickets',label:'Cantidad de tickets'},
  {id:'f_valor_ticket',k:'valor_ticket',label:'Valor por ticket'},
  {id:'f_separacion',k:'separacion',label:'Aportación inicial'},
  {id:'f_esquema',k:'esquema',label:'Esquema de pago'},
  {id:'f_metodo_pago',k:'metodo_pago',label:'Método de pago'},
  {id:'f_fechas_pago',k:'fechas_pago',label:'Fechas de pago'},
  {id:'f_fecha_notaria',k:'fecha_notaria',label:'Fecha firma notaría'},
  {id:'f_notaria',k:'notaria',label:'Notaría'},
];

// ── HELPERS ────────────────────────────────────────────────────────────────
function toast(msg){const e=document.getElementById('toast');e.textContent=msg;e.classList.add('show');setTimeout(()=>e.classList.remove('show'),3000)}
function sleep(ms){return new Promise(r=>setTimeout(r,ms))}
function esc(s){return(s||'').replace(/'/g,"\\'").replace(/"/g,'&quot;')}
function getFormData(){return FIELDS.map(f=>({...f,value:(document.getElementById(f.id)||{}).value?.trim()||''}))}
function formHasData(){return getFormData().some(f=>f.value)}
function chkReady(){document.getElementById('analyzeBtn').disabled=!(S.files.length&&formHasData()&&S.key)}

// ── API KEY ────────────────────────────────────────────────────────────────
function saveKey(){const k=document.getElementById('apiKey').value.trim();if(!k)return;S.key=k;localStorage.setItem('portalia_key',k);toast('✅ Clave guardada');chkReady()}

// ── FILE HANDLING ──────────────────────────────────────────────────────────
function onDrop(e){e.preventDefault();document.getElementById('dz').classList.remove('over');Array.from(e.dataTransfer.files).forEach(addFile)}
function onFileChange(e){Array.from(e.target.files).forEach(addFile);e.target.value=''}

async function addFile(file){
  if(S.files.find(f=>f.name===file.name)){toast('⚠️ '+file.name+' ya fue agregado');return}
  const idx=S.files.length;
  S.files.push(file);S.texts.push('');
  renderFiles();
  try{
    if(file.name.toLowerCase().endsWith('.pdf')){
      const buf=await file.arrayBuffer();
      const pdf=await pdfjsLib.getDocument({data:buf}).promise;
      let txt='';
      for(let i=1;i<=pdf.numPages;i++){
        const pg=await pdf.getPage(i);
        const ct=await pg.getTextContent();
        const items=ct.items.filter(x=>x.str&&x.str.trim());
        // Sort by Y desc, X asc
        items.sort((a,b)=>{const yd=Math.round(b.transform[5])-Math.round(a.transform[5]);return yd!==0?yd:a.transform[4]-b.transform[4]});
        let lines=[],curY=null,curLine=[];
        for(const item of items){
          const y=Math.round(item.transform[5]);
          if(curY===null||Math.abs(y-curY)>4){if(curLine.length)lines.push(curLine);curLine=[{x:item.transform[4],str:item.str}];curY=y}
          else curLine.push({x:item.transform[4],str:item.str});
        }
        if(curLine.length)lines.push(curLine);
        txt+=lines.map(l=>l.sort((a,b)=>a.x-b.x).map(x=>x.str).join(' ')).join('\n')+'\n\n';
      }
      S.texts[idx]=txt.trim();
      toast('✅ '+file.name+' — '+pdf.numPages+' página(s)');
    }else{
      S.texts[idx]=await file.text();
      toast('✅ '+file.name+' cargado');
    }
  }catch(err){toast('❌ Error: '+err.message);S.texts[idx]=''}
  renderFiles();chkReady();
}

function removeFile(idx){S.files.splice(idx,1);S.texts.splice(idx,1);renderFiles();chkReady()}

function renderFiles(){
  const fc=document.getElementById('fileCount');
  fc.textContent=S.files.length?S.files.length+' archivo'+(S.files.length>1?'s':''):'Sin archivos';
  document.getElementById('fileList').innerHTML=S.files.map((f,i)=>{
    const sz=f.size<1048576?(f.size/1024).toFixed(1)+' KB':(f.size/1048576).toFixed(1)+' MB';
    return`<div class="fitem"><div class="fdot ${S.texts[i]?'ready':'loading'}"></div><span class="fname" title="${f.name}">${f.name}</span><span class="fsize">${sz}</span><button class="frm" type="button" onclick="removeFile(${i})">&#x2715;</button></div>`;
  }).join('')
}

// ── MODAL ──────────────────────────────────────────────────────────────────
function openModal(){
  const m=document.getElementById('modalBg');
  m.style.display='flex';
  m.classList.add('open');
  setTimeout(()=>{const ta=document.getElementById('pasteArea');if(ta)ta.focus()},200);
}

function closeModal(){
  const m=document.getElementById('modalBg');
  m.classList.remove('open');
  m.style.display='none';
  document.getElementById('pind').classList.remove('show');
}

document.getElementById('modalBg').addEventListener('click',function(e){if(e.target===this)closeModal()});
document.addEventListener('keydown',e=>{if(e.key==='Escape')closeModal()});

// ── PARSE PASTE ────────────────────────────────────────────────────────────
async function parsePaste(){
  const raw=document.getElementById('pasteArea').value.trim();
  if(!raw){toast('⚠️ Pega los datos primero');return}
  if(!S.key){toast('⚠️ Guarda tu clave API primero');return}
  document.getElementById('pind').classList.add('show');
  document.getElementById('parseBtn').disabled=true;

  const prompt=`Extrae los datos del siguiente texto y devuelve SOLO un JSON válido sin texto extra ni markdown.

TEXTO:
${raw}

JSON exacto (usa cadena vacía si no encuentras el dato):
{"nui":"","nombre":"","estado_civil":"","regimen":"","origen":"","ocupacion":"","correo":"","telefono":"","curp":"","rfc":"","domicilio":"","beneficiario":"","tickets":"","valor_ticket":"","separacion":"","esquema":"","metodo_pago":"","fechas_pago":"","fecha_notaria":"","notaria":""}

Notas:
- fecha_notaria en formato YYYY-MM-DD si la encuentras
- estado_civil: Soltero(a)|Casado(a)|Divorciado(a)|Viudo(a)|Unión libre
- regimen: Sociedad conyugal|Separación de bienes|N/A
- metodo_pago: Transferencia bancaria|Cheque|Efectivo|Tarjeta de crédito|Tarjeta de débito
- Si el texto dice "Profesión: EMPLEADA" → ocupacion="Empleada"
- Si el texto dice "BIENES MANCOMUNADOS" → regimen="Sociedad conyugal"`;

  try{
    const resp=await fetch('https://api.anthropic.com/v1/messages',{method:'POST',headers:{'Content-Type':'application/json','x-api-key':S.key,'anthropic-version':'2023-06-01','anthropic-dangerous-direct-browser-access':'true'},body:JSON.stringify({model:'claude-haiku-4-5-20251001',max_tokens:800,messages:[{role:'user',content:prompt}]})});
    if(!resp.ok){const e=await resp.json();throw new Error(e.error?.message||'Error API')}
    const data=await resp.json();
    const parsed=JSON.parse(data.content[0].text.replace(/```json|```/g,'').trim());
    const map={nui:'f_nui',nombre:'f_nombre',estado_civil:'f_estado_civil',regimen:'f_regimen',origen:'f_origen',ocupacion:'f_ocupacion',correo:'f_correo',telefono:'f_telefono',curp:'f_curp',rfc:'f_rfc',domicilio:'f_domicilio',beneficiario:'f_beneficiario',tickets:'f_tickets',valor_ticket:'f_valor_ticket',separacion:'f_separacion',esquema:'f_esquema',metodo_pago:'f_metodo_pago',fechas_pago:'f_fechas_pago',fecha_notaria:'f_fecha_notaria',notaria:'f_notaria'};
    let filled=0;
    Object.entries(map).forEach(([k,id])=>{
      const el=document.getElementById(id);const val=parsed[k]||'';
      if(el&&val){el.value=val;el.classList.add('filled');setTimeout(()=>el.classList.remove('filled'),2000);filled++}
    });
    closeModal();chkReady();toast('✅ '+filled+' campos rellenados');
  }catch(err){toast('❌ '+err.message)}
  finally{document.getElementById('pind').classList.remove('show');document.getElementById('parseBtn').disabled=false}
}

// ── LOADING STEPS ──────────────────────────────────────────────────────────
function setStep(n){['s1','s2','s3','s4'].forEach((id,i)=>{const e=document.getElementById(id);e.className='sdot'+(i<n-1?' done':i===n-1?' active':'')})}

// ── ANALYZE ────────────────────────────────────────────────────────────────
async function analyze(){
  if(!S.key){toast('⚠️ Guarda tu clave API');return}
  document.getElementById('loading').classList.add('active');
  document.getElementById('results').classList.remove('show');
  document.getElementById('analyzeBtn').disabled=true;
  setStep(1);await sleep(400);setStep(2);await sleep(300);

  const fd=getFormData();
  const filled=fd.filter(f=>f.value).map(f=>f.label+': '+f.value).join('\n');
  const empty=fd.filter(f=>!f.value).map(f=>f.label).join(', ');
  const combined=S.texts.map((t,i)=>'=== '+S.files[i]?.name+' ===\n'+t).join('\n\n');
  const cText=combined.slice(0,12000);

  setStep(3);

  const prompt=`Eres el sistema de verificación de contratos de PORTALIA DESARROLLOS INTELIGENTES. Compara los DATOS DEL CLIENTE con el CONTRATO y devuelve SOLO JSON sin texto extra.

ESTRUCTURA DE LOS CONTRATOS DE PORTALIA:
El contrato principal (CMPI) usa este formato en la sección DECLARACIONES:
  1.- Llamarse como queda escrito [NOMBRE]
  2.- Nacionalidad: [VALOR]
  3.- Originario de: [CIUDAD/ESTADO]
  4.- Fecha de nacimiento: [FECHA]
  5.- Estado civil: [VALOR] ([RÉGIMEN])
     "CASADA (BIENES MANCOMUNADOS)" = Estado civil Casado(a) + Régimen Sociedad conyugal
     "SOLTERO/A" = Estado civil Soltero(a)
  6.- Profesión: [VALOR]  ← equivale al campo Ocupación
  7.- RFC: [VALOR]
  8.- CURP: [VALOR]
  9.- Con domicilio: [DIRECCIÓN]

El ANEXO A tiene tabla DATOS GENERALES con: MANDANTE, RFC, CURP, DOMICILIO, TICKETS DE INVERSIÓN, INVERSIÓN TOTAL, PLAZO, BENEFICIARIOS.

DATOS CORRECTOS DEL CLIENTE:
${filled}
${empty?'NO evaluar estos campos: '+empty:''}

CONTRATO:
${cText}

EQUIVALENCIAS OBLIGATORIAS (siempre son CORRECTO):
- BIENES MANCOMUNADOS = Sociedad conyugal
- SEPARACION DE BIENES = Separación de bienes
- CASADA/CASADO = Casado(a)
- SOLTERA/SOLTERO = Soltero(a)
- Profesión = Ocupación (el valor que sigue es la ocupación del cliente)
- Originario de = lugar de origen

REGLAS:
1. Ignora mayúsculas, minúsculas y acentos
2. Busca cada dato en TODO el contrato (CMPI, ANEXO A, ANEXO B, ANEXO C)
3. "correcto" si el dato aparece en el contrato aunque sea con variación menor de formato
4. "error" SOLO si el valor en el contrato es claramente DIFERENTE al dato del cliente
5. "faltante" SOLO si el dato fue proporcionado Y después de buscar exhaustivamente NO aparece en ninguna parte
6. NUNCA marques faltante campos no proporcionados por el usuario

JSON exacto:
{"resumen":{"errores":0,"faltantes":0,"correctos":0,"puntaje":0},"hallazgos":[{"tipo":"error","campo":"","valorContrato":"","valorCorrecto":"","descripcion":""}],"contratoAnotado":""}

contratoAnotado: texto COMPLETO del contrato con [ERROR:fragmento], [FALTANTE:campo], [OK:fragmento]
puntaje: 0-100`;

  try{
    const resp=await fetch('https://api.anthropic.com/v1/messages',{method:'POST',headers:{'Content-Type':'application/json','x-api-key':S.key,'anthropic-version':'2023-06-01','anthropic-dangerous-direct-browser-access':'true'},body:JSON.stringify({model:'claude-sonnet-4-5',max_tokens:8000,temperature:0,messages:[{role:'user',content:prompt}]})});
    if(!resp.ok){const e=await resp.json();throw new Error(e.error?.message||'Error API')}
    const data=await resp.json();
    const clean=data.content[0].text.replace(/```json|```/g,'').trim();
    S.result=JSON.parse(clean);
    setStep(4);await sleep(300);
    renderResults(S.result);
  }catch(err){toast('❌ '+err.message);document.getElementById('analyzeBtn').disabled=false}
  finally{document.getElementById('loading').classList.remove('active')}
}

// ── RENDER RESULTS ─────────────────────────────────────────────────────────
function renderResults(r){
  document.getElementById('results').classList.add('show');
  const sc=r.resumen.puntaje>=80?'green':r.resumen.puntaje>=50?'amber':'red';
  document.getElementById('sumCards').innerHTML=`
    <div class="scard s-gold"><div class="scard-lbl">Puntaje</div><div class="scard-val gold">${r.resumen.puntaje}<sup>/100</sup></div></div>
    <div class="scard s-err"><div class="scard-lbl">Errores</div><div class="scard-val red">${r.resumen.errores}</div></div>
    <div class="scard s-warn"><div class="scard-lbl">Faltantes</div><div class="scard-val amber">${r.resumen.faltantes}</div></div>
    <div class="scard s-ok"><div class="scard-lbl">Correctos</div><div class="scard-val green">${r.resumen.correctos}</div></div>`;
  const errs=r.hallazgos.filter(h=>h.tipo==='error').length;
  document.getElementById('cBadge').textContent=r.hallazgos.length+' campos';
  document.getElementById('iBadge').className='rbadge '+(errs>0?'rb-err':'rb-ok');
  document.getElementById('iBadge').textContent=errs+' error'+(errs!==1?'es':'');
  let annIdx={err:0,warn:0,ok:0};
  let ann=(r.contratoAnotado||S.texts.join('\n\n'))
    .replace(/\[ERROR:(.*?)\]/g,(_,t)=>{const i=annIdx.err++;return`<span class="herr" id="herr-${i}" data-hl="err-${i}" onmouseenter="showTip(event,'❌ Dato incorrecto','${esc(t)}')" onmouseleave="hideTip()">${t}</span>`})
    .replace(/\[FALTANTE:(.*?)\]/g,(_,t)=>{const i=annIdx.warn++;return`<span class="hwarn" id="hwarn-${i}" data-hl="warn-${i}" onmouseenter="showTip(event,'⚠️ Faltante','${esc(t)}')" onmouseleave="hideTip()">▲ ${t}</span>`})
    .replace(/\[OK:(.*?)\]/g,(_,t)=>{const i=annIdx.ok++;return`<span class="hok" id="hok-${i}" data-hl="ok-${i}">${t}</span>`});
  document.getElementById('annotated').innerHTML=ann;
  document.getElementById('original').textContent=S.texts.map((t,i)=>'=== '+S.files[i]?.name+' ===\n'+t).join('\n\n');
  window._H=r.hallazgos;
  renderFilters(r.hallazgos);
  renderIssues('all');
}

function renderFilters(h){
  const e=h.filter(x=>x.tipo==='error').length,w=h.filter(x=>x.tipo==='faltante').length,o=h.filter(x=>x.tipo==='correcto').length;
  document.getElementById('filterRow').innerHTML=`
    <button class="fpill fp-all" type="button" onclick="setFilter(this,'all')">Todos (${h.length})</button>
    <button class="fpill" type="button" onclick="setFilter(this,'error')">Errores (${e})</button>
    <button class="fpill" type="button" onclick="setFilter(this,'faltante')">Faltantes (${w})</button>
    <button class="fpill" type="button" onclick="setFilter(this,'correcto')">Correctos (${o})</button>`;
}

function setFilter(btn,type){
  document.querySelectorAll('.fpill').forEach(p=>p.className='fpill');
  btn.classList.add({'all':'fp-all','error':'fp-err','faltante':'fp-warn','correcto':'fp-ok'}[type]);
  renderIssues(type);
}

function renderIssues(filter){
  const h=window._H||[];
  const list=filter==='all'?h:h.filter(x=>x.tipo===filter);
  if(!list.length){document.getElementById('issuesList').innerHTML='<div class="empty-st">🎉 Sin hallazgos aquí</div>';return}
  // Track per-type counters to match span IDs
  const typeCounts={error:0,faltante:0,correcto:0};
  const allH=window._H||[];
  // Build a global index per type for the FULL hallazgos list (not just filtered)
  const globalIdx=allH.map(h=>{const t=h.tipo==='error'?'err':h.tipo==='faltante'?'warn':'ok';const i=typeCounts[h.tipo]||0;typeCounts[h.tipo]=(typeCounts[h.tipo]||0)+1;return{...h,hlId:`h${t==='err'?'err':t==='warn'?'warn':'ok'}-${i}`}});
  // Now render only the filtered ones but keep their hlId
  const filteredWithId=filter==='all'?globalIdx:globalIdx.filter(x=>x.tipo===filter);
  document.getElementById('issuesList').innerHTML=filteredWithId.map((h,listIdx)=>{
    const cls=h.tipo==='error'?'issue-err':h.tipo==='faltante'?'issue-warn':'issue-ok';
    const ico=h.tipo==='error'?'❌':h.tipo==='faltante'?'⚠️':'✅';
    return`<div class="issue ${cls}" onclick="jumpToHighlight('${h.hlId}',this)" title="Click para ver en el contrato">
      <div class="issue-ttl">${ico} ${h.campo}</div>
      ${h.tipo==='error'?`<div class="issue-det">Contrato: <span class="found">${h.valorContrato||'—'}</span> &nbsp;·&nbsp; Correcto: <span class="expected">${h.valorCorrecto||'—'}</span><br>${h.descripcion}</div>`:''}
      ${h.tipo==='faltante'?`<div class="issue-det">${h.descripcion}</div>`:''}
      ${h.tipo==='correcto'?`<div class="issue-det">✓ ${h.descripcion}</div>`:''}
    </div>`;
  }).join('')
}

// ── TOOLTIP ────────────────────────────────────────────────────────────────
function showTip(e,lbl,txt){const t=document.getElementById('tip');t.innerHTML=`<div class="tip-lbl">${lbl}</div>${txt}`;t.style.left=(e.clientX+12)+'px';t.style.top=(e.clientY-10)+'px';t.classList.add('show')}
function hideTip(){document.getElementById('tip').classList.remove('show')}

// ── TABS ───────────────────────────────────────────────────────────────────
function switchTab(id){
  document.querySelectorAll('.tab-btn').forEach((b,i)=>b.classList.toggle('active',(i===0&&id==='a')||(i===1&&id==='o')));
  document.getElementById('ta').classList.toggle('active',id==='a');
  document.getElementById('to').classList.toggle('active',id==='o');
}

// ── RESET ──────────────────────────────────────────────────────────────────
function resetAll(){
  S.files=[];S.texts=[];S.result=null;
  document.getElementById('fileList').innerHTML='';
  document.getElementById('fileInput').value='';
  document.getElementById('fileCount').textContent='Sin archivos';
  document.getElementById('results').classList.remove('show');
  document.getElementById('pasteArea').value='';
  FIELDS.forEach(f=>{const el=document.getElementById(f.id);if(el.tagName==='SELECT')el.selectedIndex=0;else el.value=''});
  chkReady();
}

// ── EXPORT ─────────────────────────────────────────────────────────────────
function exportReport(){
  if(!S.result)return;
  const r=S.result;
  const txt=['REPORTE DE VERIFICACIÓN DE CONTRATOS','Portalia Desarrollos Inteligentes · Desde 2009','='.repeat(55),'Fecha: '+new Date().toLocaleString('es-MX'),'Archivos: '+S.files.map(f=>f.name).join(', '),'','RESUMEN','-'.repeat(35),'Puntaje: '+r.resumen.puntaje+'/100','Errores: '+r.resumen.errores,'Faltantes: '+r.resumen.faltantes,'Correctos: '+r.resumen.correctos,'','HALLAZGOS','-'.repeat(35),...r.hallazgos.map(h=>'['+h.tipo.toUpperCase()+'] '+h.campo+'\n  Contrato: '+(h.valorContrato||'—')+'\n  Correcto: '+(h.valorCorrecto||'—')+'\n  Nota: '+h.descripcion+'\n')].join('\n');
  const a=document.createElement('a');a.href=URL.createObjectURL(new Blob([txt],{type:'text/plain;charset=utf-8'}));a.download='reporte_portalia_'+Date.now()+'.txt';a.click();
}

// ── JUMP TO HIGHLIGHT ─────────────────────────────────────────────────────
function jumpToHighlight(hlId, issueEl){
  // Switch to annotated tab
  switchTab('a');

  // Remove previous highlights
  document.querySelectorAll('.herr,.hwarn,.hok').forEach(el=>el.classList.remove('active-hl'));
  document.querySelectorAll('.issue').forEach(el=>el.classList.remove('active-issue'));

  // Find the span in the contract
  const span=document.getElementById(hlId);
  if(!span){
    // If not found by exact id, try partial match
    const allSpans=document.querySelectorAll('[id^="h"]');
    let found=false;
    allSpans.forEach(s=>{if(s.id===hlId&&!found){s.classList.add('active-hl');s.scrollIntoView({behavior:'smooth',block:'center'});found=true}});
    if(!found)toast('⚠️ No se encontró el fragmento en el contrato');
  } else {
    span.classList.add('active-hl');
    // Scroll the contract panel to the span
    const pbody=span.closest('.pbody');
    if(pbody){
      const spanTop=span.offsetTop;
      const pbodyHeight=pbody.clientHeight;
      pbody.scrollTo({top:spanTop-pbodyHeight/2,behavior:'smooth'});
    } else {
      span.scrollIntoView({behavior:'smooth',block:'center'});
    }
  }

  // Highlight the issue card
  if(issueEl)issueEl.classList.add('active-issue');

  // Remove highlights after 3 seconds
  setTimeout(()=>{
    document.querySelectorAll('.active-hl').forEach(el=>el.classList.remove('active-hl'));
    document.querySelectorAll('.active-issue').forEach(el=>el.classList.remove('active-issue'));
  },3000);
}

chkReady();
</script>
</body>
</html>
