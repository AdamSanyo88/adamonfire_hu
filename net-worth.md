---
layout: page
title: Nettó vagyon kalkulátor
permalink: /net-worth
---

<h1 class="page-title">{{ page.title | escape }}</h1>

<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.min.js"></script>
  <style>
    body { background:#f8f9fa; color:#212529; }
    .card { margin-bottom: 20px; }
    .result { font-weight: 600; font-size: 1.1rem; white-space: pre-line; }
    .bg-orange { background-color: #ffe5b4; }
    .bg-green { background-color: #d4edda; }
    .bg-blue { background-color: #d1ecf1; }
    .bg-red { background-color: #f8d7da; }
    .bg-lightblue { background-color: #b3e5fc; }
    .chart-wrap { height: 360px; }
    .muted { opacity: .85; }
    /* Prevent underline on navigation icons/links */
    a, a:hover, a:focus, a:active { text-decoration: none !important; }
  </style>
</head>
<body>
  <div class="container py-4">
    <div class="d-flex justify-content-between align-items-center mb-4">
	  <p>Ez a kalkulátor megmutatja, hogy a 2024 végi adatok alapján mennyi nettó vagyonod van a magyar háztartásokhoz képest. A percentilisek (a teljes lakosság 100 egyenlő részre bontva) a Magyar Nemzeti Bank (MNB) 2023-as adatai alapján készültek, és módosítva lettek a 2023 és 2024 közötti becsült vagyonnövekedés figyelembevételével. A számítás tartalmazza az elsődleges lakóingatlan értékét is, ezért azt mindenképpen vedd bele. A számítás forintban történik (400 Ft-os euró-forint árfolyamot figyelembe véve).</p>
    </div>

    <div class="row">
      <div class="col-lg-6">
        <div class="card bg-orange">
          <div class="card-body">
            <h4 class="h5">🏠 Ingatlanvagyon</h4>
            <label for="propertyCount" class="form-label">Lakóingatlanok száma (maximum 5)</label>
            <input type="number" class="form-control" id="propertyCount" min="0" max="5" value="0" onchange="generatePropertyInputs()"/>
            <div id="propertyInputs"></div>
            <div class="mt-3"><strong>Összes ingatlanvagyon:</strong> <span id="realEstateTotal">0 Ft</span></div>
          </div>
        </div>

        <div class="card bg-green">
          <div class="card-body">
            <h4 class="h5">📊 Befektetések</h4>
            <label class="form-label">Nyugdíjpénztári számla</label>
            <input type="number" class="form-control" id="privatePension" value="0"/>
            <label class="form-label mt-2">Állampapír</label>
            <input type="number" class="form-control" id="govBonds" value="0"/>
            <label class="form-label mt-2">TBSZ számlák egyenlege</label>
            <input type="number" class="form-control" id="taxInvestments" value="0"/>
            <label class="form-label mt-2">Egyéb befektetések egyenlege</label>
            <input type="number" class="form-control" id="otherInvestments" value="0"/>
            <div class="mt-3"><strong>Összes befektetett vagyon:</strong> <span id="investmentTotal">0 Ft</span></div>
          </div>
        </div>

        <div class="card bg-blue">
          <div class="card-body">
            <h4 class="h5">💶 Egyéb vagyontárgyak</h4>
            <label class="form-label">Autó és egyéb vagyontárgyak</label>
            <input type="number" class="form-control" id="otherAssets" value="0"/>
            <div class="mt-3"><strong>Össze egyéb vagyontárgy:</strong> <span id="otherAssetsTotal">0 Ft</span></div>
          </div>
        </div>

        <div class="card bg-red">
          <div class="card-body">
            <h4 class="h5">➖ Hitelek</h4>
            <label class="form-label">Egyéb hitelek </label>
            <input type="number" class="form-control" id="otherLiabilities" value="0"/>
            <div class="mt-3"><strong>Összes hitel:</strong> <span id="liabilitiesTotal">0 Ft</span></div>
          </div>
        </div>
      </div>

      <div class="col-lg-6">
        <div class="card bg-lightblue">
          <div class="card-body">
            <h4 class="h5">📈 Results</h4>
            <button class="btn btn-primary mb-3" id="calcBtn">Számold ki a vagyonom</button>
            <div id="result" class="result mb-3">Kattints a “Számold ki a vagyonom” gombra, hogy lásd, hányadik percentilisbe tartozol.</div>

            <div class="small muted mb-1">Percentilisek (100 → 1)</div>
            <div class="chart-wrap">
              <canvas id="percentileChart" aria-label="Percentile chart" role="img"></canvas>
            </div>
            <div class="small mt-2" id="percentileSummary">A percentilisedet a kék oszlop jelöli.</div>
          </div>
        </div>
      </div>
    </div>
  </div>

<script>
/**
 * Percentile thresholds:
 * index 0 => Top 1%, index 99 => Top 100% (bottom)
 * Values are the minimum net worth for that percentile.
 */
const PCT_THRESHOLDS = [
  1264000000, 399120400, 300722800, 240403200, 209129200, 182232400, 164804800, 147616000, 135679600, 132774800
124792000, 119045200, 113298000, 107551200, 101804000, 99341200, 95892800, 92444800, 88996400, 85548400
82100000, 78652000, 75203600, 71755600, 68307200, 66008400, 64202400, 62396000, 60590000, 58783600
56977600, 55171200, 53365200, 51558800, 49752800, 49260000, 47946400, 46632800, 45319200, 44005600
42692000, 41378400, 40064800, 38751200, 37437600, 36846400, 35926800, 35007600, 34088000, 33168400
32248800, 31329200, 30410000, 29490400, 28570800, 28242400, 27421600, 26600400, 25779600, 24958400
24137600, 23316400, 22495600, 21674400, 20853600, 20525200, 19704000, 18883200, 18062000, 17241200
16420000, 15599200, 14778000, 13957200, 13136000, 12643600, 11986800, 11330000, 10673200, 10016400
9359600, 8702800, 8046000, 7389200, 6732400, 6486000, 5911200, 5336400, 4762000, 4187200
3612400, 3037600, 2463200, 1888400, 1313600, 1050800, 788000, 525600, 262800, 0
];

// Static chart data (labels 100 → 1, values aligned)
const CHART_LABELS = Array.from({ length: 100 }, (_, i) => String(100 - i));
const CHART_DATA   = [...PCT_THRESHOLDS].reverse();

let percentileChart = null;

// Create the chart ONCE so it's always visible; no destroy/recreate later
function initChartStatic() {
  const canvas = document.getElementById("percentileChart");
  if (!canvas) return;
  const ctx = canvas.getContext("2d");
  if (!ctx) return;

  const baseColors = new Array(100).fill("#b9c2cf"); // grey everywhere initially

  percentileChart = new Chart(ctx, {
    type: "bar",
    data: {
      labels: CHART_LABELS,
      datasets: [{
        data: CHART_DATA,
        backgroundColor: baseColors,
        borderWidth: 0
      }]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      plugins: {
        legend: { display: false },
        tooltip: {
          callbacks: {
            title: (items) => `Percentile: ${items[0].label}`,
            label:  (item)  => `Threshold: $Ft{Number(item.raw).toLocaleString()}`
          }
        }
      },
      scales: {
        x: { grid: { display: false }, ticks: { maxRotation: 0, autoSkip: true } },
        y: { beginAtZero: true, ticks: { callback: (v) => `$Ft{v.toLocaleString()}` } }
      }
    }
  });
}

// Only update bar colors to highlight the clicked percentile
function highlightPercentile(percentile) {
  if (!percentileChart) return;

  // Map percentile p (1..100) to bar index (100..1 -> 0..99)
  const p = Math.max(1, Math.min(100, percentile));
  const highlightIndex = 100 - p;

  const colors = new Array(100).fill("#b9c2cf");
  colors[highlightIndex] = "#0d6efd";

  percentileChart.data.datasets[0].backgroundColor = colors;
  percentileChart.update();
}

function generatePropertyInputs() {
  const count = parseInt(document.getElementById("propertyCount").value) || 0;
  const container = document.getElementById("propertyInputs");
  container.innerHTML = "";
  for (let i = 0; i < count; i++) {
    const div = document.createElement("div");
    div.classList.add("mb-3");
    div.innerHTML = `
      <h5 class="h6 mt-3">Lakás/ház ${i + 1}</h5>
      <label class="form-label">Lakás/ház értéke</label>
      <input type="number" class="form-control" id="propertyValue${i}" value="0"/>
      <label class="form-label mt-2">Fennálló tőketartozás / hitel</label>
      <input type="number" class="form-control" id="propertyMortgage${i}" value="0"/>
    `;
    container.appendChild(div);
  }
}

function calculateNetWorthAndPercentile() {
  const count = parseInt(document.getElementById("propertyCount").value) || 0;
  let realEstateTotal = 0;
  for (let i = 0; i < count; i++) {
    const v = parseFloat(document.getElementById(`propertyValue${i}`)?.value) || 0;
    const m = parseFloat(document.getElementById(`propertyMortgage${i}`)?.value) || 0;
    realEstateTotal += (v - m);
  }

  const investments =
    (parseFloat(document.getElementById("privatePension").value) || 0) +
    (parseFloat(document.getElementById("govBonds").value) || 0) +
    (parseFloat(document.getElementById("taxInvestments").value) || 0) +
    (parseFloat(document.getElementById("otherInvestments").value) || 0);

  const otherAssets = parseFloat(document.getElementById("otherAssets").value) || 0;
  const liabilities = parseFloat(document.getElementById("otherLiabilities").value) || 0;

  const netWorth = realEstateTotal + investments + otherAssets - liabilities;

  document.getElementById("realEstateTotal").innerText = `$Ft{realEstateTotal.toLocaleString()}`;
  document.getElementById("investmentTotal").innerText = `$Ft{investments.toLocaleString()}`;
  document.getElementById("otherAssetsTotal").innerText = `$Ft{otherAssets.toLocaleString()}`;
  document.getElementById("liabilitiesTotal").innerText = `$Ft{liabilities.toLocaleString()}`;

  // Find percentile: first threshold that netWorth >= threshold
  let percentile = 100;
  for (let i = 0; i < PCT_THRESHOLDS.length; i++) {
    if (netWorth >= PCT_THRESHOLDS[i]) { percentile = i + 1; break; }
  }

  return { netWorth, percentile };
}

document.addEventListener("DOMContentLoaded", () => {
  // Static chart is visible immediately
  initChartStatic();

  // Only highlight on click; keep your original math for "above"
  document.getElementById("calcBtn").addEventListener("click", () => {
    const { netWorth, percentile } = calculateNetWorthAndPercentile();
    const above = Math.max(0, Math.min(100, 100 - percentile)); // unchanged

    document.getElementById("result").textContent =
      `Becsült nettó vagyon: $Ft{netWorth.toLocaleString()}\nBecsült vagyoni percentilis: Top ${percentile}%`;

    document.getElementById("percentileSummary").textContent =
      `Gazdagabb vagy az emberek ${above}%-ánál (Top ${percentile}%).`;

    highlightPercentile(percentile);
  });
});
</script>
</body>
</html>
