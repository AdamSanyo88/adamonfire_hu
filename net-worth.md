---
layout: page
title: Net worth calculator
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
	  <p>This calculator shows you how wealthy your household was at the end of 2024 compared to all household in Hungary. The percentiles are created using the 2023 data collected by the Hungarian Central Bank (MNB) and modified to match the estimated wealth increase between 2023 and 2024. The calculation takes into account the value of your primary residence, so include that as well. All calculations are made in forint (Ft).</p>
    </div>

    <div class="row">
      <div class="col-lg-6">
        <div class="card bg-orange">
          <div class="card-body">
            <h4 class="h5">🏠 Real Estate</h4>
            <label for="propertyCount" class="form-label">Number of Properties</label>
            <input type="number" class="form-control" id="propertyCount" min="0" max="5" value="0" onchange="generatePropertyInputs()"/>
            <div id="propertyInputs"></div>
            <div class="mt-3"><strong>Total Real Estate:</strong> <span id="realEstateTotal">0 Ft</span></div>
          </div>
        </div>

        <div class="card bg-green">
          <div class="card-body">
            <h4 class="h5">📊 Investments</h4>
            <label class="form-label">Private Pension</label>
            <input type="number" class="form-control" id="privatePension" value="0"/>
            <label class="form-label mt-2">Government Bonds</label>
            <input type="number" class="form-control" id="govBonds" value="0"/>
            <label class="form-label mt-2">Tax-efficient Investments</label>
            <input type="number" class="form-control" id="taxInvestments" value="0"/>
            <label class="form-label mt-2">Other Investments</label>
            <input type="number" class="form-control" id="otherInvestments" value="0"/>
            <div class="mt-3"><strong>Total Investments:</strong> <span id="investmentTotal">0 Ft</span></div>
          </div>
        </div>

        <div class="card bg-blue">
          <div class="card-body">
            <h4 class="h5">💶 Other Assets</h4>
            <label class="form-label">Cars & Other Assets</label>
            <input type="number" class="form-control" id="otherAssets" value="0"/>
            <div class="mt-3"><strong>Total Other Assets:</strong> <span id="otherAssetsTotal">0 Ft</span></div>
          </div>
        </div>

        <div class="card bg-red">
          <div class="card-body">
            <h4 class="h5">➖ Liabilities</h4>
            <label class="form-label">Other Liabilities</label>
            <input type="number" class="form-control" id="otherLiabilities" value="0"/>
            <div class="mt-3"><strong>Total Liabilities:</strong> <span id="liabilitiesTotal">0 Ft</span></div>
          </div>
        </div>
      </div>

      <div class="col-lg-6">
        <div class="card bg-lightblue">
          <div class="card-body">
            <h4 class="h5">📈 Results</h4>
            <button class="btn btn-primary mb-3" id="calcBtn">Calculate Net Worth</button>
            <div id="result" class="result mb-3">Click “Calculate Net Worth” to highlight your percentile.</div>

            <div class="small muted mb-1">Percentile chart (100 → 1)</div>
            <div class="chart-wrap">
              <canvas id="percentileChart" aria-label="Percentile chart" role="img"></canvas>
            </div>
            <div class="small mt-2" id="percentileSummary">Your position will be highlighted in blue.</div>
          </div>
        </div>
      </div>
    </div>
  </div>

<script>
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

const CHART_LABELS = Array.from({ length: 100 }, (_, i) => String(100 - i));
const CHART_DATA   = [...PCT_THRESHOLDS].reverse();

let percentileChart = null;

const FtFormatter = (val) => `${(val / 1_000_000).toFixed(0)}M`;

// ✅ NEW FUNCTION
function generatePropertyInputs() {
  const count = parseInt(document.getElementById("propertyCount").value) || 0;
  const container = document.getElementById("propertyInputs");
  container.innerHTML = '';

  for (let i = 0; i < count; i++) {
    const group = document.createElement('div');
    group.classList.add('row', 'mb-2');

    const valueCol = document.createElement('div');
    valueCol.classList.add('col-6');
    valueCol.innerHTML = `
      <label class="form-label">Property ${i + 1} Value</label>
      <input type="number" class="form-control" id="propertyValue${i}" value="0"/>
    `;

    const mortgageCol = document.createElement('div');
    mortgageCol.classList.add('col-6');
    mortgageCol.innerHTML = `
      <label class="form-label">Property ${i + 1} Mortgage</label>
      <input type="number" class="form-control" id="propertyMortgage${i}" value="0"/>
    `;

    group.appendChild(valueCol);
    group.appendChild(mortgageCol);
    container.appendChild(group);
  }
}

function initChartStatic() {
  const canvas = document.getElementById("percentileChart");
  if (!canvas) return;
  const ctx = canvas.getContext("2d");
  if (!ctx) return;

  const baseColors = new Array(100).fill("#b9c2cf");

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
            label:  (item)  => `Threshold: ${Number(item.raw).toLocaleString()} Ft`
          }
        }
      },
      scales: {
        x: { grid: { display: false }, ticks: { maxRotation: 0, autoSkip: true } },
        y: {
          beginAtZero: true,
          ticks: {
            callback: (v) => `${FtFormatter(v)} Ft`,
            stepSize: 50000000
          }
        }
      }
    }
  });
}

function highlightPercentile(percentile) {
  if (!percentileChart) return;
  const p = Math.max(1, Math.min(100, percentile));
  const highlightIndex = 100 - p;
  const colors = new Array(100).fill("#b9c2cf");
  colors[highlightIndex] = "#0d6efd";
  percentileChart.data.datasets[0].backgroundColor = colors;
  percentileChart.update();
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

  document.getElementById("realEstateTotal").innerText = `${realEstateTotal.toLocaleString()} Ft`;
  document.getElementById("investmentTotal").innerText = `${investments.toLocaleString()} Ft`;
  document.getElementById("otherAssetsTotal").innerText = `${otherAssets.toLocaleString()} Ft`;
  document.getElementById("liabilitiesTotal").innerText = `${liabilities.toLocaleString()} Ft`;

  let percentile = 100;
  for (let i = 0; i < PCT_THRESHOLDS.length; i++) {
    if (netWorth >= PCT_THRESHOLDS[i]) {
      percentile = i + 1;
      break;
    }
  }

  return { netWorth, percentile };
}

document.addEventListener("DOMContentLoaded", () => {
  initChartStatic();

  document.getElementById("calcBtn").addEventListener("click", () => {
    const { netWorth, percentile } = calculateNetWorthAndPercentile();
    const above = Math.max(0, Math.min(100, 100 - percentile));

    document.getElementById("result").textContent =
      `Estimated Net Worth: ${netWorth.toLocaleString()} Ft\nEstimated Wealth Percentile: Top ${percentile}%`;

    document.getElementById("percentileSummary").textContent =
      `You’re above approximately ${above}% of people (Top ${percentile}%).`;

    highlightPercentile(percentile);
  });
});
</script>
</body>
</html>

