---
layout: page
title: Nettó vagyon és vagyonadó kalkulátor
permalink: /net-worth-test
---

<h1 class="page-title">{{ page.title | escape }}</h1>

<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
<script defer src="https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.min.js"></script>

<style>
body{
  background:#f8f9fa;
  color:#212529;
  font-family:system-ui,-apple-system,Segoe UI,Roboto,Inter,Arial;
}

.container-lg{
  max-width:1400px;
}

input[type=number]{
  width:100%;
  padding:6px 8px;
  border:1px solid #ced4da;
  border-radius:6px;
}

.table th,
.table td{
  vertical-align:middle;
}

.table input[disabled]{
  background:#eee;
}

.chart-wrap{
  height:420px;
}

.result strong{
  font-size:1.25rem;
}

.mono{
  font-variant-numeric:tabular-nums;
}


/* === Calculator visual refresh === */

.calculator-shell{
  background:linear-gradient(135deg,#eef6ff 0%,#f8fbff 100%);
  border:1px solid #d7e9ff;
  border-radius:22px;
  padding:24px;
  box-shadow:0 14px 36px rgba(13,110,253,.08);
}

.calculator-kicker{
  font-size:.75rem;
  font-weight:800;
  letter-spacing:.1em;
  text-transform:uppercase;
  color:#0d6efd;
  margin-bottom:6px;
}


/* === Net worth table === */

#nw-table{
  border-radius:16px;
  overflow:hidden;
  box-shadow:0 8px 22px rgba(15,23,42,.06);
  border-color:#e3eaf2;
}

#nw-table thead th{
  background:#f1f5f9!important;
  color:#475569;
  font-size:.78rem;
  text-transform:uppercase;
  letter-spacing:.03em;
}

#nw-table .table-secondary td{
  background:#eaf2fb!important;
  color:#23415f;
  font-weight:800;
  border-top:8px solid #fff;
}


/* Positive / asset inputs */

#nw-table input[data-field=value]:not(:disabled){
  background:#eaf4ff!important;
  border:2px solid #90c2ff!important;
  font-weight:700;
}


/* Debt inputs */

#nw-table input[data-field=debt]:not(:disabled){
  background:#fff1f1!important;
  border:2px solid #f0a2a2!important;
  font-weight:700;
}


/* Active input */

#nw-table input:not(:disabled):focus{
  background:#fff7d6!important;
  border-color:#e0a800!important;
  box-shadow:0 0 0 3px rgba(224,168,0,.14)!important;
  outline:0;
}


/* Disabled inputs */

#nw-table input:disabled{
  background:#f1f3f5!important;
  border-color:#e2e5e8!important;
  color:#a0a6ad;
}


/* === Main result card === */

.net-result-card{
  display:flex;
  align-items:center;
  justify-content:space-between;
  gap:32px;

  background:linear-gradient(135deg,#0d6efd,#0756c9);
  color:#fff;

  border-radius:18px;
  padding:24px 28px;
  margin:22px 0;

  box-shadow:0 12px 28px rgba(13,110,253,.2);
}


/* Left side: net worth result */

.net-result-card > div{
  flex:1 1 auto;
  min-width:0;
}

.net-result-card .result-label{
  font-size:.78rem;
  font-weight:800;
  letter-spacing:.08em;
  text-transform:uppercase;
  opacity:.82;
  margin-bottom:5px;
}

.net-result-card #nw-ft{
  display:block;
  font-size:clamp(1.8rem,3.2vw,2.4rem);
  font-weight:800;
  line-height:1.15;
  white-space:nowrap;
}


/* Right side: percentile */

.net-result-card #pct-chip{
  flex:0 0 auto;

  display:inline-flex;
  align-items:center;
  justify-content:center;

  min-width:130px;

  font-size:1rem;
  font-weight:800;
  line-height:1.2;
  white-space:nowrap;

  padding:.75rem 1.1rem;

  background:#fff!important;
  color:#0d6efd!important;

  border-radius:999px;

  box-shadow:0 4px 12px rgba(0,0,0,.12);
}


  /* A meglévő táblázatba illesztett, kompakt cégadatok */
  .business-input-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(145px,1fr));gap:9px;}
  .business-input-grid label{font-size:.78rem;font-weight:600;color:#475569;}
  .business-input-grid input{display:block;margin-top:4px;font-size:.9rem;}
  #nw-table input[data-business]:focus{background:#fff7d6!important;border-color:#e0a800!important;outline:0;}
  .wealth-tax-result{border:1px solid #d7e9ff;border-radius:12px;background:#fff;padding:14px 20px;margin:-8px 0 22px;display:flex;align-items:center;justify-content:space-between;gap:12px;flex-wrap:wrap;}
  .wealth-tax-result strong{font-size:1.3rem;color:#0756c9;}

/* === Chart === */

.chart-card{
  background:#fff;
  border:1px solid #e3eaf2;
  border-radius:16px;
  padding:18px;
  box-shadow:0 8px 22px rgba(15,23,42,.06);
}


/* === Mobile === */

@media(max-width:768px){

  .calculator-shell{
    padding:14px;
  }

  .net-result-card{
    flex-direction:column;
    align-items:flex-start;
    gap:16px;
    padding:20px;
  }

  .net-result-card #nw-ft{
    font-size:1.7rem;
    white-space:normal;
  }

  .net-result-card #pct-chip{
    align-self:flex-start;
    min-width:auto;
  }

}
</style>

<div class="container py-4">
<div class="calculator-shell">
  <div class="calculator-kicker">Nettó vagyon és vagyonadó kalkulátor</div>
  <div class="d-flex justify-content-between align-items-center mb-4">
     <p>Ez a kalkulátor megmutatja, hogy az MNB adatai alapján mennyi nettó vagyonod van a magyar háztartásokhoz képest. A percentilisek (a teljes lakosság 100 egyenlő részre bontva) a Magyar Nemzeti Bank (MNB) 2014, 2017, 2020, és 2023-as adatai alapján készültek, és módosítva lettek a 2023 és 2026 közötti becsült vagyonnövekedéssel. A számítás tartalmazza az elsődleges lakóingatlan értékét és a 2027-ben bevezetendő vagyonadó számítása alapján a cégértéket is, ezért ezeket mindenképpen vedd bele. A számítás forintban történik. A lenti grafikában több időszak vagyoni szintjeit is megnézheted, és ahhoz hasonlíthatod a vagyonod szintjét (de értelemszerűen a 2026-os táblázat tükrözi a jelenlegi vagyoni szinteket).</p>
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

      <tr class="table-secondary"><td colspan="6">🏢 Céges részesedés (nem tőzsdei társaság), 500 millió Ft-os tőkéig</td></tr>
      <tr data-type="business">
        <td>🏢</td>
        <td>
          <div class="fw-semibold mb-2">Cégértékelés a 2027-ben bevezetendő vagyonadó alapján</div>
          <div class="business-input-grid">
            <label>Saját tőke (Ft)<input type="number" data-business="equity" min="0" max="500000000" step="1" value="0"></label>
            <label>2024 adózott eredmény (Ft)<input type="number" data-business="profit2024" step="1" value="0"></label>
            <label>2025 adózott eredmény (Ft)<input type="number" data-business="profit2025" step="1" value="0"></label>
            <label>2026 adózott eredmény (Ft)<input type="number" data-business="profit2026" step="1" value="0"></label>
            <label>Tulajdoni hányad (%)<input type="number" data-business="ownership" min="0" max="100" step="0.01" value="100"></label>
          </div>
          <div id="business-detail" class="small text-muted mt-2">Számított hozamérték: Ft 0</div>
          <div class="small text-muted mt-1">500 millió Ft vagy magasabb saját tőke esetén a rejtett tartalékok miatt a kalkuláció nem alkalmazható. A 33–50% közötti kisebbségi részesedésre 25%, 33% alatt 30% értékcsökkentés érvényesül. Holdingtársaságokra eltérő szabály vonatkozik.</div>
        </td>
        <td><input type="number" data-field="value" value="0" disabled aria-label="Számított cégérték"></td>
        <td><input type="number" data-field="debt" value="0" disabled></td>
        <td class="text-end mono" data-cell="net">Ft 0</td>
        <td></td>
      </tr>

      <tr class="table-secondary"><td colspan="6">📊 Befektetések</td></tr>
      <tr data-type="inv"><td>📦</td><td>Nyugdíjpénztár</td>
        <td><input type="number" data-field="value" value="0"></td>
        <td><input type="number" data-field="debt" value="0" disabled></td>
        <td class="text-end mono" data-cell="net">Ft 0</td>
        <td></td>
      </tr>
      <tr data-type="inv"><td>🏛️</td><td>Állampapírok</td>
        <td><input type="number" data-field="value" value="0"></td>
        <td><input type="number" data-field="debt" value="0" disabled></td>
        <td class="text-end mono" data-cell="net">Ft 0</td>
        <td></td>
      </tr>
      <tr data-type="inv"><td>🧾</td><td>Tartós befektetési számla</td>
        <td><input type="number" data-field="value" value="0"></td>
        <td><input type="number" data-field="debt" value="0" disabled></td>
        <td class="text-end mono" data-cell="net">Ft 0</td>
        <td></td>
      </tr>
      <tr data-type="inv"><td>📈</td><td>Egyéb befektetések</td>
        <td><input type="number" data-field="value" value="0"></td>
        <td><input type="number" data-field="debt" value="0" disabled></td>
        <td class="text-end mono" data-cell="net">Ft 0</td>
        <td></td>
      </tr>

      <tr class="table-secondary"><td colspan="6">💶 Egyéb vagyontárgyak</td></tr>
      <tr data-type="asset"><td>🚗</td><td>Autó- és egyéb vagyontárgyak</td>
        <td><input type="number" data-field="value" value="0"></td>
        <td><input type="number" data-field="debt" value="0" disabled></td>
        <td class="text-end mono" data-cell="net">Ft 0</td>
        <td></td>
      </tr>

      <tr class="table-secondary"><td colspan="6">➖ Hitelek</td></tr>
      <tr data-type="liab"><td>💳</td><td>Egyéb hitelek</td>
        <td><input type="number" data-field="value" value="0" disabled></td>
        <td><input type="number" data-field="debt" value="0"></td>
        <td class="text-end mono" data-cell="net">Ft 0</td>
        <td></td>
      </tr>

      <tr class="fw-bold table-light">
        <td colspan="2">Total</td>
        <td class="text-end" id="sum-value">Ft 0</td>
        <td class="text-end" id="sum-debt">Ft 0</td>
        <td class="text-end" id="sum-net">Ft 0</td>
        <td></td>
      </tr>
    </tbody>
  </table>

  <div class="net-result-card">
    <div><div class="result-label">Becsült nettó vagyon</div><span id="nw-ft">Ft 0</span></div>
    <span class="badge" id="pct-chip">Percentilis: –</span>
  </div>

  <div class="wealth-tax-result" role="status" aria-live="polite">
    <div><div class="fw-semibold">Fizetendő vagyonadó 2027-ben</div><div class="small text-muted">Becsült összeg a 2026. december 31-i nettó vagyon alapján, kedvezmények nélkül</div></div>
    <strong class="mono" id="wealth-tax">Ft 0</strong>
  </div>

  <!-- Skála év választó -->
  <div class="d-flex align-items-center gap-2 mb-1">
    <label for="scale-year" class="form-label mb-0 small text-muted">
      Skála éve a grafikonhoz:
    </label>
    <select id="scale-year" class="form-select form-select-sm" style="width:auto">
      <option value="2014">2014</option>
      <option value="2017">2017</option>
      <option value="2020">2020</option>
      <option value="2023">2023</option>
      <option value="2025" selected>2025</option>
    </select>
  </div>

  <div class="chart-card"><div class="chart-wrap"><canvas id="percentileChart"></canvas></div>
  <div id="pct-text" class="mt-2 small text-muted">Az értékek automatikusan frissülnek, ha új adatot adsz meg.</div></div>
</div>
</div>

<script>
(function(){
  // === Percentilis küszöbök Ft-ban (1..100; 1 = leggazdagabb, 100 = legszegényebb) ===
  const PCT_DATA = {
    "2014": [
      428491000, 125133000, 89270000, 72937000, 63705000, 55200000, 49602000, 45677000, 41848000, 40127000,
      37656700, 35362300, 33207700, 31184300, 29284300, 27500000, 26445400, 25431300, 24456100, 23518200,
      22616400, 21749100, 20915000, 20113000, 19341700, 18600000, 17972900, 17367000, 16781500, 16215800,
      15669100, 15140800, 14630400, 14137100, 13660500, 13200000, 12825700, 12462000, 12108600, 11765200,
      11431500, 11107400, 10792400, 10486300, 10188900, 9900000, 9628900, 9365300, 9108800, 8859400,
      8616800, 8380900, 8151400, 7928200, 7711100, 7500000, 7257600, 7023100, 6796100, 6576500,
      6364000, 6158300, 5959300, 5766700, 5580300, 5400000, 5155900, 4922800, 4700200, 4487700,
      4284900, 4091100, 3906200, 3729600, 3561000, 3400000, 3153100, 2924200, 2711900, 2515000,
      2332400, 2163000, 2006000, 1860300, 1725300, 1600000, 1212600, 919000, 696400, 527800,
      400000, 303100, 229700, 174100, 132000, 100000, 70000, 40000, 20000, 0
    ],
    "2017": [
      647184000, 191334000, 137200000, 104003000, 83914000, 73398000, 64335000, 58422000, 55636000, 49800000,
      47286800, 44900400, 42634500, 40482900, 38439900, 36500000, 35059200, 33675400, 32346100, 31069300,
      29842900, 28664900, 27533500, 26446600, 25402700, 24400000, 23708100, 23035700, 22382500, 21747700,
      21131000, 20531800, 19949500, 19383800, 18834100, 18300000, 17829000, 17370200, 16923200, 16487600,
      16063300, 15649900, 15247200, 14854800, 14472500, 14100000, 13703400, 13317900, 12943300, 12579200,
      12225400, 11881500, 11547300, 11222500, 10906800, 10600000, 10266500, 9943600, 9630800, 9327800,
      9034400, 8750200, 8474900, 8208300, 7950100, 7700000, 7374600, 7063000, 6764500, 6478600,
      6204800, 5942600, 5691500, 5451000, 5220600, 5000000, 4605900, 4242900, 3908500, 3600400,
      3316600, 3055200, 2814400, 2592600, 2388200, 2200000, 1855200, 1564400, 1319200, 1112400,
      938100, 791100, 667100, 562500, 474300, 400000, 300000, 200000, 100000, 0
    ],
    "2020": [
      767230000, 309962000, 222265000, 168485000, 135942000, 118905000, 104223000, 94645000, 90130000, 80591000,
      77453000, 74152900, 70993500, 67968600, 65072600, 62300000, 59834100, 57465800, 55191200, 53006600,
      50908500, 48893500, 46958200, 45099600, 43314400, 41600000, 40302200, 39044800, 37826700, 36646500,
      35503200, 34395600, 33322500, 32282900, 31275700, 30300000, 29450400, 28624700, 27822100, 27042000,
      26283800, 25546900, 24830600, 24134400, 23457700, 22800000, 22192000, 21600200, 21024200, 20463500,
      19917800, 19386700, 18869700, 18366500, 17876700, 17400000, 16860700, 16338000, 15831600, 15340900,
      14865400, 14404600, 13958100, 13525500, 13106200, 12700000, 12126400, 11578700, 11055800, 10556500,
      10079700, 9624400, 9189800, 8774700, 8378400, 8000000, 7482700, 6998900, 6546300, 6123000,
      5727100, 5356800, 5010400, 4686500, 4383400, 4100000, 3481900, 2957000, 2511200, 2132600,
      1811100, 1538000, 1306200, 1109200, 942000, 800000, 600000, 390000, 180000, 0
    ],
    "2023": [
      1183230000, 478028000, 342780000, 259840000, 209652000, 183377000, 160735000, 145963000, 139001000, 124290000, 119449000, 114360000, 109487000, 104822000, 100356000, 96080000, 92277000, 88624000, 85117000, 81747000, 79121000, 75990000, 72982000, 70093000, 67319000, 64654000, 62637000, 60683000, 58790000, 56955000, 56092000, 54342000, 52647000, 51004000, 49413000, 47872000, 46529000, 45225000, 43957000, 42724000, 41785000, 40614000, 39475000, 38368000, 37292000, 36247000, 35280000, 34339000, 33424000, 32532000, 31439000, 30601000, 29785000, 28991000, 28218000, 27465000, 26614000, 25789000, 24989000, 24215000, 23690000, 22956000, 22244000, 21555000, 20886000, 20239000, 19325000, 18452000, 17619000, 16823000, 16456000, 15712000, 15003000, 14325000, 13678000, 13060000, 12216000, 11426000, 10687000, 9996000, 8591000, 8035000, 7516000, 7030000, 6575000, 6150000, 5223000, 4436000, 3767000, 3199000, 2717000, 2307000, 1959000, 1664000, 1413000, 1200000, 900000, 585000, 270000, 0
    ],
   "2026": [
  1881340000, 734730000, 526850000, 399370000, 322230000,
  281850000, 247050000, 224340000, 213640000, 196300000,
  188660000, 180620000, 172920000, 165560000, 158500000,
  151750000, 145740000, 139970000, 134430000, 129110000,
  124960000, 120020000, 115270000, 110710000, 106320000,
  102120000, 98930000, 95840000, 92850000, 89960000,
  89190000, 86400000, 83710000, 81100000, 78570000,
  76120000, 73980000, 71910000, 69890000, 67930000,
  66440000, 64580000, 62770000, 61010000, 59300000,
  57630000, 56100000, 54600000, 53140000, 51730000,
  49990000, 48660000, 47360000, 46100000, 44870000,
  43670000, 42320000, 41000000, 39730000, 38500000,
  37670000, 36500000, 35370000, 34270000, 33210000,
  32180000, 30730000, 29340000, 28010000, 26750000,
  26170000, 24980000, 23850000, 22780000, 21750000,
  19380000, 18130000, 16960000, 15860000, 14830000,
  12750000, 11920000, 11150000, 10430000, 9760000,
  9130000, 7750000, 6580000, 5590000, 4750000,
  4030000, 3420000, 2910000, 2470000, 2100000,
  1780000, 1340000, 870000, 400000, 0
]
  };

  const LABELS = Array.from({length:100},(_,i)=>String(100-i)); // 100 -> 1
  const CURRENCY = "Ft";
  const LOCALE = "hu-HU";

  function fmtFt(n){
    return `${CURRENCY} ${Number(n||0).toLocaleString(LOCALE)}`;
  }

  // Alapértelmezett év: 2025
  let currentYear = "2025";
  let PCT_THRESHOLDS = PCT_DATA[currentYear].slice();

  let chart;

  function getChartBars(){
    // PCT_THRESHOLDS: 1..100 (gazdag->szegény), grafikonon: 1..100 (szegény->gazdag)
    return [...PCT_THRESHOLDS].reverse();
  }

  function initChart(){
    const canvas = document.getElementById("percentileChart");
    if(!canvas || !window.Chart || !PCT_THRESHOLDS.length) return;
    const ctx = canvas.getContext('2d');

    chart = new Chart(ctx,{
      type:"bar",
      data:{
        labels: LABELS,
        datasets:[{
          data: getChartBars(),
          backgroundColor: new Array(100).fill("#cfd8dc"),
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
              title: items => items && items[0] ? ("Percentilis "+items[0].label) : "",
              label:  item  => "Medián vagyon " + fmtFt(item.raw)
            }
          }
        },
        scales:{
          x:{grid:{display:false},ticks:{autoSkip:true,maxRotation:0}},
          y:{
            beginAtZero:true,
            suggestedMax: 2000000000,   // fix: 2,0 Mrd
            max: 2000000000,
            ticks:{
              stepSize: 100000000,      // fix: 100M lépték
              callback: (v) => (v/1e6)+"M"
            }
          }
        }
      }
    });
  }

  function updateChartScale(year){
    if(!PCT_DATA[year] || !PCT_DATA[year].length || !chart) return;
    currentYear = year;
    PCT_THRESHOLDS = PCT_DATA[year].slice();

    chart.data.datasets[0].data = getChartBars();

    // Y-skála fix marad: 0–1.8Mrd, 100M lépés
    chart.options.scales.y.max = 1800000000;
    chart.options.scales.y.suggestedMax = 1800000000;
    chart.options.scales.y.ticks.stepSize = 100000000;

    chart.data.datasets[0].backgroundColor = new Array(100).fill("#cfd8dc");
    chart.update();

    compute(); // új skálához újraszámoljuk a percentilist
  }

  function highlight(p){
    if(!chart) return;
    const idx = 100 - p; // 1-es percentilis a jobb szél
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

  function businessValue(){
    const row=document.querySelector('#rows tr[data-type="business"]');
    if(!row) return 0;
    const number=(field)=>{
      const value=Number(row.querySelector(`[data-business="${field}"]`).value);
      return Number.isFinite(value) ? value : 0;
    };
    // Minden adat Ft-ban értendő, nincs ezerforintos átváltás.
    const equity=Math.max(0,Math.min(499999999,number('equity')));
    const ownership=Math.max(0,Math.min(100,number('ownership')));
    const average=(number('profit2024')+number('profit2025')+number('profit2026'))/3;
    const yieldValue=Math.max(0,average)/0.15;
    const fullCompanyValue=(equity+2*yieldValue)/3;
    const discount=ownership<33 ? 0.30 : ownership<50 ? 0.25 : 0;
    // A végső részesedésérték legalább nulla, a kijelzés és az összesítés egyezik.
    const value=Math.max(0,Math.round(fullCompanyValue*ownership/100*(1-discount)));
    row.querySelector('[data-field="value"]').value=value;
    document.getElementById('business-detail').textContent=
      `Saját tőke: ${fmtFt(equity)} · Átlagos adózott eredmény: ${fmtFt(average)} · `+
      `Hozamérték: ${fmtFt(yieldValue)} · Teljes cégérték: ${fmtFt(Math.round(fullCompanyValue))} · `+
      `Tulajdoni hányad: ${ownership}% · Kisebbségi értékcsökkentés: ${discount*100}% · `+
      `Számított részesedésérték: ${fmtFt(value)}`;
    return value;
  }

  function compute(){
    let sumV=0,sumD=0,sumN=0;
    const computedBusinessValue=businessValue();
    document.querySelectorAll("#rows tr[data-type]").forEach(r=>{
      const t=r.dataset.type;
      const v=t==="business" ? computedBusinessValue : (+r.querySelector('[data-field="value"]')?.value||0);
      const d=+r.querySelector('[data-field="debt"]')?.value||0;
      let n=0;
      if(t==="prop") n=v-d;
      else if(t==="inv"||t==="asset"||t==="business") n=v;
      else if(t==="liab") n=-d;
      sumV+=v; sumD+=d; sumN+=n;
      r.querySelector('[data-cell="net"]').textContent = fmtFt(n);
    });

    document.getElementById("sum-value").textContent = fmtFt(sumV);
    document.getElementById("sum-debt").textContent  = fmtFt(sumD);
    document.getElementById("sum-net").textContent   = fmtFt(sumN);
    document.getElementById("nw-ft").textContent     = fmtFt(sumN);
    const tax=Math.max(0,Math.min(sumN,100000000000)-1000000000)*0.01
      +Math.max(0,sumN-100000000000)*0.015;
    document.getElementById("wealth-tax").textContent = fmtFt(Math.round(tax));

    if (!PCT_THRESHOLDS.length){
      document.getElementById("pct-chip").textContent = "Percentilis: –";
      document.getElementById("pct-text").textContent = "Hiányzó percentilis adatok.";
      return;
    }

    // Percentilis (1..100) az aktuális év skáláján
    let pct=100;
    for(let i=0;i<PCT_THRESHOLDS.length;i++){
      if(sumN>=PCT_THRESHOLDS[i]){ pct=i+1; break; }
    }

    document.getElementById("pct-chip").textContent = "Top "+pct+"% ("+currentYear+")";
    document.getElementById("pct-text").textContent =
      `A nettó becsült vagyonod ${fmtFt(sumN)}, amivel a háztartások ${100-pct}%-ánál vagyonosabb vagy (Top ${pct}%, ${currentYear}-es skála).`;

    highlight(pct);
  }

  function initAll(){
    addProperty();
    initChart();
    compute();
  }

  if (document.readyState === "complete" || document.readyState === "interactive") {
    initAll();
  } else {
    document.addEventListener("DOMContentLoaded", initAll);
  }

  // Események
  document.body.addEventListener("input",e=>{
    if(!e.target.matches("input")) return;
    if(e.target.matches('[data-business="equity"]') && Number(e.target.value)>=500000001) e.target.value="500000000";
    if(e.target.matches('[data-business="equity"]') && Number(e.target.value)<0) e.target.value="0";
    if(e.target.matches('[data-business="ownership"]') && Number(e.target.value)>100) e.target.value="100";
    if(e.target.matches('[data-business="ownership"]') && Number(e.target.value)<0) e.target.value="0";
    compute();
  });
  document.addEventListener("click",e=>{
    if(e.target.id==="add-prop"){ addProperty(); }
    if(e.target.tagName==="BUTTON" && e.target.closest("tr")?.dataset.type==="prop"){
      e.target.closest("tr").remove(); compute();
    }
  });

  document.addEventListener("change", e => {
    if (e.target && e.target.id === "scale-year") {
      updateChartScale(e.target.value);
    }
  });
})();
</script>

