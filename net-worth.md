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
    a, a:hover, a:focus, a:active { text-decoration: none !important; }
  </style>
</head>
<body>
  <div class="container py-4">
    <div class="d-flex justify-content-between align-items-center mb-4">
	  <p>Ez a kalkulátor megmutatja, hogy a 2024 végi adatok alapján mennyi nettó vagyonod van a magyar háztartásokhoz képest...</p>
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
            <h4 class="h5">📈 Összesítés</h4>
            <button class="btn btn-primary mb-3" id="calcBtn">Számold ki a vagyonom</button>
            <div id="result" class="result mb-3">Kattints a “Számold ki a vagyonom” gombra...</div>
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
// Sample PCT_THRESHOLDS array, required for percentile logic
const PCT_THRESHOLDS = Array.from({ length: 100 }, (_, i) => (i + 1) * 1000000);

const CHART_LABELS = Array.from({ length: 100 }, (_, i) => String(100 - i));
const CHART_DATA = [...PCT_THRESHOLDS].reverse();
let percentileChart = null;

function initChartStatic() {
  const ctx = document.getElementById("percentileChart").getContext("2d");
  const baseColors = new Array(100).fill("#b9c2cf");

  percentileChart = new Chart(ctx, {
    type: "bar",
    data: {
      labels: CHART_LABELS,
      datasets: [{ data: CHART_DATA, backgroundColor: baseColors, borderWidth: 0 }]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      plugins: {
        legend: { display: false },
        tooltip: {
          callbacks: {
            title: (items) => `Percentilis: ${items[0].label}`,
            label: (item) => `Küszöbérték: ${Number(item.raw).toLocaleString()} Ft`
          }
        }
      },
      scales: {
        x: { grid: { display: false }, ticks: { maxRotation: 0, autoSkip: true } },
        y: {
          beginAtZero: true,
          ticks: {
            stepSize: 20000000,
            callback: (v) => `${v / 1_000_000}M Ft`
          }
        }
      }
    }
  });
}

function highlightPercentile(percentile) {
  if (!percentileChart) return;
  const p = Math.max(1, Math.min(100, percentile));
  const idx = 100 - p;
  const colors = new Array(100).fill("#b9c2cf");
  colors[idx] = "#0d6efd";
  percentileChart.data.datasets[0].backgroundColor = colors;
  percentileChart.update();
}

function generatePropertyInputs() {
  const count = parseInt(document.getElementById("propertyCount").value) || 0;
  const container = document.getElementById("propertyInputs");
  container.innerHTML = "";
  for (let i = 0; i < count; i++) {
    container.innerHTML += `
      <div class="mb-3">
        <h5 class="h6 mt-3">Lakás/ház ${i + 1}</h5>
        <label class="form-label">Lakás/ház értéke</label>
        <input type="number" class="form-control" id="propertyValue${i}" value="0"/>
        <label class="form-label mt-2">Fennálló tőketartozás / hitel</label>
        <input type="number" class="form-control" id="propertyMortgage${i}" value="0"/>
      </div>
    `;
  }
}

function calculateNetWorthAndPercentile() {
  let realEstateTotal = 0;
  const count = parseInt(document.getElementById("propertyCount").value) || 0;
  for (let i = 0; i < count; i++) {
    const v = parseFloat(document.getElementById(`propertyValue${i}`)?.value) || 0;
    const m = parseFloat(document.getElementById(`propertyMortgage${i}`)?.value) || 0;
    realEstateTotal += (v - m);
  }
  const investments = ["privatePension", "govBonds", "taxInvestments", "otherInvestments"]
    .map(id => parseFloat(document.getElementById(id)?.value) || 0)
    .reduce((a, b) => a + b, 0);
  const otherAssets = parseFloat(document.getElementById("otherAssets").value) || 0;
  const liabilities = parseFloat(document.getElementById("otherLiabilities").value) || 0;
  const netWorth = realEstateTotal + investments + otherAssets - liabilities;

  document.getElementById("realEstateTotal").innerText = `${realEstateTotal.toLocaleString()} Ft`;
  document.getElementById("investmentTotal").innerText = `${investments.toLocaleString()} Ft`;
  document.getElementById("otherAssetsTotal").innerText = `${otherAssets.toLocaleString()} Ft`;
  document.getElementById("liabilitiesTotal").innerText = `${liabilities.toLocaleString()} Ft`;

  let percentile = 100;
  for (let i = 0; i < PCT_THRESHOLDS.length; i++) {
    if (netWorth >= PCT_THRESHOLDS[i]) { percentile = i + 1; break; }
  }
  return { netWorth, percentile };
}

document.addEventListener("DOMContentLoaded", () => {
  initChartStatic();
  const calcBtn = document.getElementById("calcBtn");
  if (calcBtn) {
    calcBtn.addEventListener("click", () => {
      const { netWorth, percentile } = calculateNetWorthAndPercentile();
      const above = Math.max(0, Math.min(100, 100 - percentile));

      document.getElementById("result").textContent =
        `Becsült nettó vagyon: ${netWorth.toLocaleString()} Ft\nBecsült vagyoni percentilis: Top ${percentile}%`;

      document.getElementById("percentileSummary").textContent =
        `Gazdagabb vagy az emberek ${above}%-ánál (Top ${percentile}%).`;

      highlightPercentile(percentile);
    });
  } else {
    console.warn("calcBtn not found");
  }
});
</script>
</body>
</html>
