---
layout: page
title: Nettó vagyon kalkulátor
permalink: /net-worth
---

<h1 class="page-title">{{ page.title | escape }}</h1>

<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
<script defer src="https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.min.js"></script>

<style>
body{background:#f8f9fa;color:#212529;font-family:system-ui,-apple-system,Segoe UI,Roboto,Inter,Arial}
.container-lg{max-width:1400px}
input[type=number]{width:100%;padding:6px 8px;border:1px solid #ced4da;border-radius:6px}
.table th,.table td{vertical-align:middle}
.table input[disabled]{background:#eee}
.chart-wrap{height:420px}
.result strong{font-size:1.25rem}
.mono{font-variant-numeric: tabular-nums}
</style>

<div class="container py-4">
  <div class="d-flex justify-content-between align-items-center mb-4">
     <p>Ez a kalkulátor megmutatja, hogy a 2024 végi adatok alapján mennyi nettó vagyonod van a magyar háztartásokhoz képest. A percentilisek (a teljes lakosság 100 egyenlő részre bontva) a Magyar Nemzeti Bank (MNB) 2023-as adatai alapján készültek, és módosítva lettek a 2023 és 2024 közötti becsült vagyonnövekedés figyelembevételével. A számítás tartalmazza az elsődleges lakóingatlan értékét is, ezért azt mindenképpen vedd bele. A számítás forintban történik (400 Ft-os euró-forint árfolyamot figyelembe véve).</p>
  </div>

  <table class="table table-bordered bg-white" id="nw-table">
    <thead class="table-light">
      <tr>
        <th style="width:15%">Kategóriák</th>
        <th>Vagyonelemek</th>
        <th class="text-end" style="width:15%">Piaci ár (Ft)</th>
        <th class="text-end" style="width:15%">Hitel összege (Ft)</th>
        <th class="text-end" style="width:15%">Nettó érték</th>
        <th style="width:4%"></th>
      </tr>
    </thead>
    <tbody id="rows">
      <tr class="table-secondary"><td colspan="6">🏠 Ingatlanok</td></tr>
      <tr id="prop-anchor"></tr>
      <tr><td colspan="6"><button class="btn btn-outline-secondary" id="add-prop" type="button">➕ Ingatlan hozzáadása</button></td></tr>

      <tr class="table-secondary"><td colspan="6">📊 Befektetések</td></tr>
      <tr data-type="inv"><td>📦</td><td>Nyugdíjpénztár</td>
        <td><input type="number" data-field="value" value="0"></td><td><input type="number" data-field="debt" value="0" disabled></td>
        <td class="text-end mono" data-cell="net">Ft 0</td><td></td></tr>
      <tr data-type="inv"><td>🏛️</td><td>Állampapírok</td>
        <td><input type="number" data-field="value" value="0"></td><td><input type="number" data-field="debt" value="0" disabled></td>
        <td class="text-end mono" data-cell="net">Ft 0</td><td></td></tr>
      <tr data-type="inv"><td>🧾</td><td>Tartós befektetési számla</td>
        <td><input type="number" data-field="value" value="0"></td><td><input type="number" data-field="debt" value="0" disabled></td>
        <td class="text-end mono" data-cell="net">Ft 0</td><td></td></tr>
      <tr data-type="inv"><td>📈</td><td>Egyéb befektetések</td>
        <td><input type="number" data-field="value" value="0"></td><td><input type="number" data-field="debt" value="0" disabled></td>
        <td class="text-end mono" data-cell="net">Ft 0</td><td></td></tr>

      <tr class="table-secondary"><td colspan="6">💶 Egyéb vagyontárgyak</td></tr>
      <tr data-type="asset"><td>🚗</td><td>Autó- és egyéb vagyontárgyak</td>
        <td><input type="number" data-field="value" value="0"></td><td><input type="number" data-field="debt" value="0" disabled></td>
        <td class="text-end mono" data-cell="net">Ft 0</td><td></td></tr>

      <tr class="table-secondary"><td colspan="6">➖ Hitelek</td></tr>
      <tr data-type="liab"><td>💳</td><td>Egyéb hitelek</td>
        <td><input type="number" data-field="value" value="0" disabled></td>
        <td><input type="number" data-field="debt" value="0"></td>
        <td class="text-end mono" data-cell="net">Ft 0</td><td></td></tr>

      <tr class="fw-bold table-light">
        <td colspan="2">Total</td>
        <td class="text-end" id="sum-value">Ft 0</td>
        <td class="text-end" id="sum-debt">Ft 0</td>
        <td class="text-end" id="sum-net">Ft 0</td>
        <td></td>
      </tr>
    </tbody>
  </table>

  <div class="result mb-3">
    <strong>Nettó vagyon:</strong> <span id="nw-ft">Ft 0</span>
    <span class="badge text-bg-primary" id="pct-chip">Percentilis: –</span>
  </div>

  <div class="chart-wrap"><canvas id="percentileChart"></canvas></div>
  <div id="pct-text" class="mt-2 small text-muted">Az értékek automatikusan frissülnek, ha új adatot adsz meg.</div>
</div>

<script>
(function(){
  // === Percentile thresholds in Ft (descending, 100 -> 1) ===
  const PCT_THRESHOLDS = [
    1264000000, 399120400, 300722800, 240403200, 209129200, 182232400, 164804800, 147616000, 135679600, 132774800,
    124792000, 119045200, 113298000, 107551200, 101804000, 99341200, 95892800, 92444800, 88996400, 85548400,
    82100000, 78652000, 75203600, 71755600, 68307200, 66008400, 64202400, 62396000, 60590000, 58783600,
    56977600, 55171200, 53365200, 51558800, 49752800, 49260000, 47946400, 46632800, 45319200, 44005600,
    42692000, 41378400, 40064800, 38751200, 37437600, 36846400, 35926800, 35007600, 34088000, 33168400,
    32248800, 31329200, 30410000, 29490400, 28570800, 28242400, 27421600, 26600400, 25779600, 24958400,
    24137600, 23316400, 22495600, 21674400, 20853600, 20525200, 19704000, 18883200, 18062000, 17241200,
    16420000, 15599200, 14778000, 13957200, 13136000, 12643600, 11986800, 11330000, 10673200, 10016400,
    9359600, 8702800, 8046000, 7389200, 6732400, 6486000, 5911200, 5336400, 4762000, 4187200,
    3612400, 3037600, 2463200, 1888400, 1313600, 1050800, 788000, 525600, 262800, 0
  ];

  const LABELS = Array.from({length:100},(_,i)=>String(100-i)); // 100 -> 1
  const CHART_BARS = [...PCT_THRESHOLDS].reverse(); // index 0 is 1st percentile, etc.

  const CURRENCY = "Ft";
  const LOCALE = "hu-HU";

  function fmtFt(n){
    return `${CURRENCY} ${Number(n||0).toLocaleString(LOCALE)}`;
  }

  let chart;

  function initChart(){
    const canvas = document.getElementById("percentileChart");
    if(!canvas || !window.Chart) return;
    const ctx = canvas.getContext('2d');

    chart = new Chart(ctx,{
      type:"bar",
      data:{
        labels: LABELS,
        datasets:[{
          data: CHART_BARS,
          backgroundColor: "#cfd8dc",
          borderWidth: 0
        }]
      },
      options:{
        responsive:true,
        maintainAspectRatio:false,
        plugins:{
          legend:{display:false},
          tooltip:{
            callbacks:{
              title: items => items && items[0] ? ("Percentile "+items[0].label) : "",
              label:  item  => "Threshold " + fmtFt(item.raw)
            }
          }
        },
        scales:{
          x:{grid:{display:false},ticks:{autoSkip:true,maxRotation:0}},
          y:{
            beginAtZero:true,
            suggestedMax: 1500000000,          // 1.5B Ft top
            max: 1500000000,
            ticks:{
              stepSize: 100000000,             // 100M gridlines
              callback: (v) => (v/1e6)+"M"     // 100M, 200M, ... 1500M
            }
          }
        }
      }
    });
  }

  function highlight(p){
    if(!chart) return;
    const idx = 100 - p; // bar index (0-based from left)
    const colors = new Array(100).fill("#cfd8dc");
    if (idx>=0 && idx<colors.length) colors[idx] = "#0d6efd";
    chart.data.datasets[0].backgroundColor = colors;
    chart.update();
  }

  function addProperty(){
    const anchor=document.getElementById("prop-anchor");
    const tr=document.createElement("tr"); tr.dataset.type="prop";
    tr.innerHTML=`<td>🏠</td><td>Ingatlan</td>
      <td><input type="number" data-field="value" value="0"></td>
      <td><input type="number" data-field="debt" value="0"></td>
      <td class="text-end mono" data-cell="net">Ft 0</td>
      <td><button class="btn btn-sm btn-outline-danger" type="button">✖</button></td>`;
    anchor.parentNode.insertBefore(tr,anchor);
  }

  function compute(){
    let sumV=0,sumD=0,sumN=0;
    document.querySelectorAll("#rows tr[data-type]").forEach(r=>{
      const t=r.dataset.type;
      const v=+r.querySelector('[data-field="value"]')?.value||0;
      const d=+r.querySelector('[data-field="debt"]')?.value||0;
      let n=0;
      if(t==="prop") n=v-d;
      else if(t==="inv"||t==="asset") n=v;
      else if(t==="liab") n=-d;
      sumV+=v; sumD+=d; sumN+=n;
      r.querySelector('[data-cell="net"]').textContent = fmtFt(n);
    });

    document.getElementById("sum-value").textContent = fmtFt(sumV);
    document.getElementById("sum-debt").textContent  = fmtFt(sumD);
    document.getElementById("sum-net").textContent   = fmtFt(sumN);
    document.getElementById("nw-ft").textContent     = fmtFt(sumN);

    // percentile (1..100), thresholds are descending from 100->1
    let pct=100;
    for(let i=0;i<PCT_THRESHOLDS.length;i++){
      if(sumN>=PCT_THRESHOLDS[i]){ pct=i+1; break; }
    }

    document.getElementById("pct-chip").textContent = "Top "+pct+"%";
    document.getElementById("pct-text").textContent =
      `A nettó becsült vagyonod ${fmtFt(sumN)}, amivel a háztartások ${100-pct}%-ánál vagyonosabb vagy (Top ${pct}%).`;

    highlight(pct);
  }

  // Init
  if (document.readyState === "complete" || document.readyState === "interactive") {
    initChart(); addProperty(); compute();
  } else {
    document.addEventListener("DOMContentLoaded", ()=>{ initChart(); addProperty(); compute(); });
  }

  // Events
  document.body.addEventListener("input",e=>{ if(e.target.matches("input")) compute(); });
  document.addEventListener("click",e=>{
    if(e.target.id==="add-prop"){ addProperty(); }
    if(e.target.tagName==="BUTTON" && e.target.closest("tr")?.dataset.type==="prop"){
      e.target.closest("tr").remove(); compute();
    }
  });
})();
</script>
