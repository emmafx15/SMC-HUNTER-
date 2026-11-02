<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>SMC HUNTERS - Trading Terminal Pro</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700&family=Inter:wght@400;700;900&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;margin:0;padding:0;font-family:Inter,sans-serif}
:root{--green:#00ff88;--bg:#050a0a;--card:#0f1e16;--border:#1a3a2a}
body{background:var(--bg);color:#fff;min-height:100vh}
.top{display:flex;justify-content:space-between;align-items:center;padding:14px 20px;background:rgba(10,18,15,0.95);border-bottom:1px solid var(--border);position:sticky;top:0;z-index:10;backdrop-filter:blur(12px)}
.logo{font-weight:900;letter-spacing:1px}.logo span{color:var(--green)}
.btn{padding:10px 18px;border-radius:12px;border:1px solid var(--border);background:var(--card);color:#fff;cursor:pointer;font-weight:700;font-size:13px}
.btn-green{background:var(--green);color:#000;box-shadow:0 0 20px #00ff8840;border-color:var(--green)}
.layout{display:grid;grid-template-columns:280px 1fr 320px;gap:14px;padding:14px;max-width:1600px;margin:0 auto}
.card{background:linear-gradient(180deg,rgba(15,30,22,0.9),rgba(10,20,15,0.9));border:1px solid var(--border);border-radius:18px;padding:16px}
.h{font-size:11px;letter-spacing:1.5px;color:#7aa88a;margin-bottom:12px;text-transform:uppercase}
.pair{padding:10px 12px;border-radius:10px;border:1px solid #222;background:rgba(255,255,255,0.03);margin:6px 0;display:flex;justify-content:space-between;align-items:center;cursor:pointer;font-size:13px}
.pair.active{border-color:var(--green);background:rgba(0,255,136,0.1);color:var(--green)}
.price{font-family:JetBrains Mono,monospace}
.bull{color:var(--green)}.bear{color:#ff4d4d}
.chart-wrap{height:520px;border-radius:18px;overflow:hidden;background:#000;border:1px solid var(--border)}
.a-card{background:var(--card);border:1px solid var(--border);border-radius:14px;padding:12px;margin:8px 0}
.score{float:right;background:rgba(0,255,136,0.15);border:1px solid var(--green);color:var(--green);padding:2px 8px;border-radius:20px;font-size:11px;font-weight:800}
.tag{display:inline-block;padding:3px 7px;border-radius:6px;font-size:10px;font-weight:700;margin:2px}
.ob{background:rgba(0,255,136,0.15);color:var(--green);border:1px solid var(--green)}
.fvg{background:rgba(255,170,0,0.15);color:#ffaa00}.liq{background:rgba(0,170,255,0.15);color:#00aaff}
.bos{background:rgba(255,68,170,0.15);color:#ff44aa}
input,select{width:100%;padding:12px;border-radius:10px;border:1px solid var(--border);background:#000;color:#fff;outline:none;margin-top:6px}
@media(max-width:1100px){.layout{grid-template-columns:1fr}.chart-wrap{height:400px}}
</style>
</head>
<body>
<div class="top">
<div class="logo">◎ SMC HUNTERS <span>A+ PREMIUM</span></div>
<div style="display:flex;gap:8px"><button class="btn" onclick="document.getElementById('market').scrollIntoView()">Markets</button><button class="btn btn-green">Live • Connected</button></div>
</div>

<div class="layout">
<div>
<div class="card">
<div class="h">Total Portfolio Value</div>
<div style="font-size:30px;font-weight:900">$128,462.94</div>
<div style="margin-top:8px;padding:6px 12px;border-radius:20px;background:rgba(0,255,136,0.12);border:1px solid var(--green);color:var(--green);font-size:12px;display:inline-block">+6.24% (+$7,542.10) • 24H</div>
<div class="h" style="margin-top:16px">Watchlist (click to load chart)</div>
<div id="watchlist"></div>
</div>
<div class="card" style="margin-top:14px">
<div class="h">A+ Setups Detected</div>
<div id="asetups"><div style="color:#666;font-size:12px;text-align:center;padding:10px">Select a pair to scan</div></div>
</div>
</div>

<div>
<div class="chart-wrap" id="tvchart"></div>
<div class="card" style="margin-top:14px;display:flex;gap:10px;justify-content:space-between;flex-wrap:wrap">
<div><div class="h">Selected Pair</div><div id="curPair" style="font-weight:900;font-size:20px">EURUSD</div><div id="curPrice" class="price" style="color:var(--green)">Loading...</div></div>
<div style="display:flex;gap:8px;align-items:center">
<button class="btn btn-green" style="padding:14px 28px;font-size:16px" onclick="trade('BUY')">▲ BUY</button>
<button class="btn" style="padding:14px 28px;font-size:16px;border-color:#ff4d4d;color:#ff4d4d" onclick="trade('SELL')">▼ SELL</button>
</div>
</div>
</div>

<div>
<div class="card" id="market">
<div class="h">Select Pairs (SMC will scan only these)</div>
<div style="max-height:300px;overflow-y:auto" id="pairList"></div>
<button class="btn btn-green" style="width:100%;margin-top:10px" onclick="runScan()">Scan <span id="cnt">0</span> Pairs for A+</button>
</div>
<div class="card" style="margin-top:14px">
<div class="h">Quick Trade</div>
<label style="font-size:11px;color:#888">Lot Size</label>
<select id="lots"><option>0.01</option><option selected>0.10</option><option>0.25</option><option>1.00</option></select>
<label style="font-size:11px;color:#888;margin-top:10px;display:block">Risk</label>
<input value="1% per trade" disabled>
<div style="margin-top:12px;font-size:11px;color:#666">Risk: LOW • Demo terminal. Connect broker API for real execution.</div>
</div>
</div>
</div>

<script src="https://s3.tradingview.com/tv.js"></script>
<script>
const PAIRS = [
 {s:"FX:EURUSD", n:"EURUSD", p:1.0842, c:0.18},
 {s:"FX:GBPUSD", n:"GBPUSD", p:1.2721, c:-0.12},
 {s:"FX:USDJPY", n:"USDJPY", p:149.82, c:0.45},
 {s:"FX:GBPJPY", n:"GBPJPY", p:190.45, c:0.31},
 {s:"OANDA:XAUUSD", n:"XAUUSD GOLD", p:2661.40, c:-0.42},
 {s:"OANDA:XAGUSD", n:"XAGUSD SILVER", p:31.20, c:1.1},
 {s:"BINANCE:BTCUSD", n:"BTCUSD", p:67204, c:4.89},
 {s:"BINANCE:ETHUSD", n:"ETHUSD", p:3450, c:3.2},
 {s:"BINANCE:SOLUSD", n:"SOLUSD", p:142.5, c:5.1},
 {s:"NASDAQ:AAPL", n:"AAPL", p:225.12, c:1.2},
 {s:"NASDAQ:TSLA", n:"TSLA", p:248.5, c:-0.8},
 {s:"NASDAQ:NVDA", n:"NVDA", p:142.85, c:3.12},
];
let selected = new Set(["FX:EURUSD","BINANCE:BTCUSD","OANDA:XAUUSD","NASDAQ:NVDA"]);
let current = PAIRS[0];
function render(){
 let w=document.getElementById('watchlist'); w.innerHTML='';
 PAIRS.filter(x=>selected.has(x.s)).forEach(p=>{
   let up=p.c>=0;
   w.innerHTML+=`<div class="pair ${current.s===p.s?'active':''}" onclick="loadPair('${p.s}')"><span>${p.n}</span><span class="price ${up?'bull':'bear'}">${p.p} ${up?'▲':'▼'}${Math.abs(p.c)}%</span></div>`;
 });
 let l=document.getElementById('pairList'); l.innerHTML='';
 PAIRS.forEach(p=>{
   let on=selected.has(p.s);
   l.innerHTML+=`<div class="pair ${on?'active':''}" onclick="toggle('${p.s}')"><span>${p.n}</span><span>${on?'✓':'+'}</span></div>`;
 });
 document.getElementById('cnt').innerText=selected.size;
}
function toggle(s){
 if(selected.has(s)){ if(selected.size>1) selected.delete(s);} else { if(selected.size<15) selected.add(s); }
 render();
}
function loadPair(sym){
 current = PAIRS.find(x=>x.s===sym);
 document.getElementById('curPair').innerText=current.n;
 document.getElementById('curPrice').innerText=current.p;
 document.getElementById('tvchart').innerHTML='';
 new TradingView.widget({
  "autosize":true, "symbol":sym, "interval":"60", "timezone":"Etc/UTC",
  "theme":"dark", "style":"1", "locale":"en", "toolbar_bg":"#000",
  "enable_publishing":false, "hide_top_toolbar":false, "save_image":false,
  "container_id":"tvchart"
 });
 render(); runScanOne(current);
}
function runScan(){
 render();
 document.getElementById('asetups').innerHTML='<div style="text-align:center;color:#00ff88;padding:10px">🔍 Scanning '+selected.size+' pairs for A+...</div>';
 setTimeout(()=>{
   document.getElementById('asetups').innerHTML='';
   PAIRS.filter(p=>selected.has(p.s)).forEach(p=>addSetup(p));
 },800);
}
function runScanOne(p){
 document.getElementById('asetups').innerHTML='<div style="text-align:center;color:#00ff88;padding:10px">Scanning '+p.n+'...</div>';
 setTimeout(()=>{ document.getElementById('asetups').innerHTML=''; addSetup(p); },600);
}
function addSetup(p){
 let ob=Math.random()>0.25, fvg=Math.random()>0.35, liq=Math.random()>0.2, bos=Math.random()>0.3, htf=Math.random()>0.5;
 let score=(ob?25:0)+(fvg?25:0)+(liq?20:0)+(bos?20:0)+(htf?10:0);
 let isA=score>=75;
 let entry=(p.p*(1+(Math.random()*0.002-0.001))).toFixed(2), sl=(entry*0.992).toFixed(2), tp=(entry*1.015).toFixed(2);
 let html=`<div class="a-card"><span class="score">${score}% ${isA?'A+':''}</span><b>${p.n}</b> ${isA?'<span class="tag ob">A+ SETUP</span>':'<span class="tag" style="background:#333;color:#888">B Setup</span>'}
 <div style="margin-top:6px">${ob?'<span class="tag ob">✓ OB</span>':''}${fvg?'<span class="tag fvg">✓ FVG</span>':''}${liq?'<span class="tag liq">✓ LIQ</span>':''}${bos?'<span class="tag bos">✓ BOS</span>':''}</div>
 <div style="margin-top:8px;font-size:11px;line-height:1.5">${isA?`Entry ${entry} | SL ${sl} | TP ${tp}<br><button class="btn btn-green" style="width:100%;margin-top:6px;padding:8px" onclick="alert('Taking ${p.n} A+')">TAKE A+ TRADE →</button>`:`Score ${score}% - Wait for A+`}</div></div>`;
 document.getElementById('asetups').innerHTML+=html;
}
function trade(side){ alert(side+' '+current.n+' Lot:'+document.getElementById('lots').value+'\nDemo mode - connect MT5/Binance API for live execution'); }
render(); loadPair(current.s);
</script>
</body>
</html>
