---
layout: page
title: Személyes infláció kalkulátor
permalink: /inflation
---

<h1 class="page-title">{{ page.title | escape }}</h1>

<html lang="hu">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Személyes infláció kalkulátor</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">

  <style>
  body { background: #f8fafc; }
  .category-removed { opacity: 0.5; }
  .badge-fixed { font-variant-numeric: tabular-nums; }
  .table thead th { white-space: nowrap; }

  /* --- NAV override (Materialize markup kompatibilitás) --- */
  nav.blue.accent-4 .nav-wrapper ul.right.hide-on-med-and-down > li > a,
  nav.blue.accent-4 .nav-wrapper ul.right.hide-on-med-and-down > li > a:link,
  nav.blue.accent-4 .nav-wrapper ul.right.hide-on-med-and-down > li > a:visited,
  nav.blue.accent-4 .nav-wrapper ul.right.hide-on-med-and-down > li > a:hover,
  nav.blue.accent-4 .nav-wrapper ul.right.hide-on-med-and-down > li > a:focus,
  nav.blue.accent-4 .nav-wrapper ul.right.hide-on-med-and-down > li > a:active,
  nav.blue.accent-4 .nav-wrapper ul#nav-mobile.side-nav li > a {
    text-decoration: none !important;
    border-bottom: 0 !important;
    box-shadow: none !important;
  }

  nav.blue.accent-4 .nav-wrapper ul.right.hide-on-med-and-down > li.active > a,
  nav.blue.accent-4 .nav-wrapper ul.right.hide-on-med-and-down > li > a.active {
    text-decoration: none !important;
    border-bottom: 0 !important;
    box-shadow: none !important;
  }

  nav.blue.accent-4 .nav-wrapper ul.right.hide-on-med-and-down > li > a::after {
    content: none !important;
    border: 0 !important;
    box-shadow: none !important;
  }

  nav.blue.accent-4 .nav-wrapper ul.right.hide-on-med-and-down > li > a .material-icons,
  nav.blue.accent-4 .nav-wrapper ul#nav-mobile.side-nav li > a .material-icons {
    text-decoration: none;
    display: inline-flex;
    vertical-align: middle;
  }

  /* --- NEW: minden szöveg fekete --- */
  .spending-table,
  .spending-table h2,
  .spending-table .table,
  .spending-table .table th,
  .spending-table .table td,
  .spending-table .badge,
  .form-label,
  .form-check-label {
    color: #000 !important;
    font-family: inherit !important;
    font-weight: normal !important;
  }

  /* --- SZŰKEBB SOROK és KOMPAKT MEGJELENÉS --- */
  .table-sm > :not(caption) > * > * {
    padding-top: 0.20rem !important;
    padding-bottom: 0.20rem !important;
  }

  .form-control-sm {
    padding-top: 0.10rem !important;
    padding-bottom: 0.10rem !important;
    height: auto !important;
    line-height: 1.1 !important;
  }

  .table td, .table th {
    vertical-align: middle !important;
    line-height: 1.1 !important;
  }

  /* --- BADGE színek --- */
  .badge.bg-primary,
  .badge.bg-success,
  .badge.bg-danger,
  .badge.bg-info,
  .badge.bg-warning {
    color: #fff !important;
  }

  /* --- Kompakt táblázat --- */
  .table { margin-bottom: 0.5rem !important; }
  .table-striped > tbody > tr:nth-of-type(odd) > * {
    background-color: #f9fafb !important;
  }

  .card-body { padding: 0.75rem 1rem !important; }

  .badge-fixed {
    font-size: 0.85rem !important;
    padding: 0.25rem 0.4rem !important;
  }

  /* --- SZEMÉLYES INFLÁCIÓ KIEMELT STÍLUS --- */
  .personal-infl-badge {
    display: inline-block;
    font-size: 2.6rem !important;
    font-weight: 700 !important;
    padding: 0.8rem 2rem !important;
    border-radius: 0.8rem !important;
    background-color: #0d6efd !important;
    color: #fff !important;
    text-align: center;
    line-height: 1 !important;
    min-width: 7rem;
    box-shadow: 0 4px 8px rgba(0,0,0,0.15);
    margin: 0 auto;
  }

  @media (max-width: 768px) {
    .personal-infl-badge {
      font-size: 2rem !important;
      padding: 0.6rem 1.5rem !important;
    }
  }
  
  /* === Calculator visual refresh === */
  .calculator-shell{background:linear-gradient(135deg,#eef6ff 0%,#f8fbff 100%);border:1px solid #d7e9ff;border-radius:22px;padding:24px;box-shadow:0 14px 36px rgba(13,110,253,.08)}
  .calculator-kicker{font-size:.75rem;font-weight:800;letter-spacing:.1em;text-transform:uppercase;color:#0d6efd;margin-bottom:6px}
  .calculator-shell .card{border:1px solid #e3eaf2;border-radius:16px;overflow:hidden;box-shadow:0 8px 22px rgba(15,23,42,.06)!important}
  .calculator-shell thead th{background:#f1f5f9!important;color:#475569!important;font-size:.78rem;text-transform:uppercase;letter-spacing:.03em;border-bottom:1px solid #dbe3ec}
  .calculator-shell tbody td{border-color:#edf1f5}
  .calculator-shell input[type=number]{background:#eaf4ff!important;border:2px solid #90c2ff!important;border-radius:9px!important;font-weight:700!important;color:#0f172a!important;box-shadow:none!important}
  .calculator-shell input[type=number]:hover{background:#dceeff!important;border-color:#5aa5ff!important}
  .calculator-shell input[type=number]:focus{background:#fff7d6!important;border-color:#e0a800!important;box-shadow:0 0 0 3px rgba(224,168,0,.14)!important}
  .result-card{background:linear-gradient(135deg,#0d6efd,#0756c9)!important;color:#fff;border:0!important;position:sticky;top:18px}
  .result-card h2,.result-card strong,.result-card p{color:#fff!important}
  .result-card .personal-infl-badge{background:#fff!important;color:#0d6efd!important;box-shadow:0 8px 20px rgba(0,0,0,.16)}
  .result-card .muted{color:rgba(255,255,255,.82)!important}
  @media(max-width:991px){.calculator-shell{padding:16px}.result-card{position:static}}


/* Adam on FIRE - homepage palette (colors only) */

.calculator-shell { background: linear-gradient(145deg,#0d47a1 0%,#123b85 48%,#16243a 100%) !important; color:#eaf1ff; border-color:#ffffff26; }
.calculator-shell h2,.calculator-shell h3,.calculator-shell h5 {color:#fff;}
.calculator-shell .calculator-kicker,.calculator-shell .step-kicker {color:#b9e0fa;}
.calculator-shell .card,.calculator-shell .chart-card,.calculator-shell .wealth-tax-result,.calculator-shell .table-wrap {background:#0b2145;color:#eaf1ff;border-color:#294367;}
.calculator-shell .muted,.calculator-shell .text-muted,.calculator-shell .form-label,.calculator-shell .form-check-label,.calculator-shell .inline-label,.calculator-shell .business-input-grid label,.calculator-shell .property-index-note,.calculator-shell .calculator-heading p,.calculator-shell .income-head p {color:#c5d5ef !important;}
.calculator-shell a {color:#79baff;}
.calculator-shell .table {--bs-table-color:#eaf1ff;--bs-table-bg:#0b2145;--bs-table-striped-color:#eaf1ff;--bs-table-striped-bg:#142f55;--bs-table-border-color:#294367;--bs-table-hover-color:#fff;--bs-table-hover-bg:#1b3c68;color:#eaf1ff;background:#0b2145 !important;}
.calculator-shell table td,.calculator-shell table th {color:#eaf1ff;border-color:#294367;}
.calculator-shell table thead th {background:#173c72 !important;color:#dbe8ff !important;border-color:#294367;}
.calculator-shell .table-striped > tbody > tr:nth-of-type(odd) > * {background-color:#142f55 !important;}
.calculator-shell .table-light > *,.calculator-shell .table-secondary > *,.calculator-shell .spending-table tfoot th,.calculator-shell #nw-table .table-secondary td {background:#173c72 !important;color:#dbe8ff !important;border-color:#294367;}
.calculator-shell tbody tr:hover {background:#142f55;}
.calculator-shell input:not([type=checkbox]):not([type=range]):not(:disabled),.calculator-shell select {background:#162f53 !important;color:#fff !important;border-color:#79baff !important;}
.calculator-shell input:not([type=checkbox]):not([type=range]):not(:disabled):hover {background:#1b3c68 !important;}
.calculator-shell input:not([type=checkbox]):not([type=range]):not(:disabled):focus,.calculator-shell select:focus {background:#263b55 !important;color:#fff !important;border-color:#f2bd79 !important;box-shadow:0 0 0 3px #f2bd7933 !important;}
.calculator-shell input::placeholder {color:#b9cce9;}
.calculator-shell input:disabled {background:#16243a !important;color:#aabbd4 !important;border-color:#294367 !important;}
.calculator-shell .badge.bg-light,.calculator-shell .spending-table tbody tr:not(.category-removed) td:last-child .badge {background:#173c72 !important;color:#b9e0fa !important;border-color:#294367;}
.calculator-shell .result-card,.calculator-shell .summary-card,.calculator-shell .net-result-card {background:linear-gradient(135deg,#2962ff,#245bb8) !important;color:#fff !important;}
.calculator-shell .result-card .muted,.calculator-shell .summary-card .text-muted {color:#dbe8ff !important;}
.calculator-shell .result-card .personal-infl-badge,.calculator-shell .net-result-card #pct-chip {background:#0b2145 !important;color:#b9e0fa !important;}
.calculator-shell .form-check,.calculator-shell .quick-fill-panel {background:#142f55;border-color:#294367;}
.calculator-shell .form-check-input {background-color:#16243a;border-color:#79baff;}
.calculator-shell .form-check-input:checked {background-color:#2962ff;border-color:#79baff;}
.calculator-shell .alert-secondary {background:#173c72;color:#dbe8ff;border-color:#294367;}
.calculator-shell .btn,.calculator-shell #reset {background:#173c72;color:#eaf1ff;border-color:#79baff;}
.calculator-shell .btn:hover,.calculator-shell .btn:focus-visible {background:#245bb8;color:#fff;border-color:#b9e0fa;}
.calculator-shell .btn-outline-danger {color:#e5a097;border-color:#e5a097;background:#0b2145;}
.calculator-shell .btn-outline-danger:hover {background:#663c4a;color:#fff;}
.calculator-shell .calculator-badge,.calculator-shell #serviceYearsLabel {background:#173c72;color:#b9e0fa;border-color:#79baff;}
.calculator-shell #serviceYears::-webkit-slider-runnable-track {background:#294367;}
.calculator-shell #serviceYears::-moz-range-track {background:#294367;}
.calculator-shell #serviceYears::-webkit-slider-thumb {background:#79baff;border-color:#fff;}
.calculator-shell #serviceYears::-moz-range-thumb {background:#79baff;border-color:#fff;}
.calculator-shell input.invalid-days:not(:disabled) {background:#663c4a !important;border-color:#e5a097 !important;}
.calculator-shell #nw-table input[data-field=debt]:not(:disabled) {background:#442c40 !important;border-color:#e5a097 !important;}
.calculator-shell .property-index-note.warning {color:#f2bd79 !important;}
.calculator-shell .wealth-tax-result strong {color:#f2bd79;}
.calculator-shell #nw-ft {color:#fff;}
.calculator-shell #sum-net {color:#86cda8;}
</style>
</head>

<body>
<div class="container py-4">
<div class="calculator-shell">
  <div class="calculator-kicker">Interaktív kalkulátor</div>

  <p class="muted">
    Add meg, mennyit költesz havonta az alábbi kategóriákban.  
    A kalkulátor a <strong>KSH 10 éves átlagos inflációs rátáit</strong> használja fixen,  
    és ezek alapján kiszámítja a <strong>személyes inflációdat</strong>.
  </p>

  <div class="row g-4 align-items-start">

    <!-- BAL OSZLOP: táblázat -->
    <div class="col-lg-7">
      <div class="card shadow-sm">
        <div class="card-body">
          <h2 class="h6 mb-3">Havi átlagos költés kategóriánként</h2>
          <div class="table-responsive">
            <table class="table table-sm table-striped align-middle">
              <thead>
                <tr>
                  <th>Kategória</th>
                  <th class="text-end">Költés</th>
                  <th class="text-end">Relatív súly</th>
                  <th class="text-end">10 év átlagos infláció</th>
                </tr>
              </thead>
              <tbody id="spendBody"></tbody>
              <tfoot>
                <tr>
                  <th>Összes költés</th>
                  <th class="text-end"><span id="totalSpend" class="badge bg-light text-dark badge-fixed">0,00</span></th>
                  <th class="text-end"><span class="badge bg-light text-dark badge-fixed">100,0%</span></th>
                  <th></th>
                </tr>
              </tfoot>
            </table>
          </div>
        </div>
      </div>
    </div>

    <!-- JOBB OSZLOP: eredmény -->
    <div class="col-lg-5">
      <div class="card shadow-sm result-card">
        <div class="card-body text-center">
          <h2 class="h6 mb-3">Eredmény</h2>
          <div class="mb-2"><strong>Személyes infláció</strong> (súlyozott átlag)</div>
          <span id="personalInfl" class="personal-infl-badge">0,0%</span>
          <hr>
          <p class="small muted mb-0">
            Az inflációs százalékok a 2015–2024 közötti időszak KSH által közölt 
            <strong>átlagos éves inflációját</strong> mutatják kategóriánként.
          </p>
        </div>
      </div>
    </div>

  </div>
</div>
</div>

<script>
const CATS = [
  { key: "elelmiszer", label: "Élelmiszer", rate: 0.082 },
  { key: "alkohol", label: "Alkohol", rate: 0.055 },
  { key: "dohany", label: "Dohányáru", rate: 0.098 },
  { key: "ruhazat", label: "Ruházat", rate: 0.023 },
  { key: "lakasszolg", label: "Rezsi és lakáshoz kötött költségek", rate: 0.043 },
  { key: "lakber", label: "Lakberendezés és lakás karbantartása", rate: 0.047 },
  { key: "egeszsegugy", label: "Egészségügy", rate: 0.057 },
  { key: "auto", label: "Közlekedés saját autóval", rate: 0.058 },
  { key: "auto_ertek", label: "Autó értékvesztése", rate: 0.027 },
  { key: "egyeb_kozlekedes", label: "Egyéb közlekedés", rate: 0.074 },
  { key: "tavkozles", label: "Távközlés", rate: 0.008 },
  { key: "oktatas", label: "Oktatás", rate: 0.041 },
  { key: "szabadido", label: "Szabadidő és hobbi", rate: 0.044 },
  { key: "vendeglatas", label: "Vendéglátás és szálláshely", rate: 0.090 },
  { key: "egyeb", label: "Egyéb termékek és szolgáltatások (pl. biztosítások, banki díjak)", rate: 0.051 },
];

const fmtPct = (v) => (v * 100).toFixed(1).replace('.', ',') + '%';
const fmtAmt = (v) => new Intl.NumberFormat('hu-HU', { minimumFractionDigits: 2, maximumFractionDigits: 2 }).format(v);

const spendBody = document.getElementById('spendBody');
CATS.forEach(c => {
  const tr = document.createElement('tr');
  tr.innerHTML = `
    <td>${c.label}</td>
    <td class="text-end">
      <input type="number" class="form-control form-control-sm text-end" id="amt_${c.key}" min="0" step="100" value="0">
    </td>
    <td class="text-end"><span id="w_${c.key}" class="badge bg-light text-dark badge-fixed">0,0%</span></td>
    <td class="text-end text-muted">${fmtPct(c.rate)}</td>
  `;
  spendBody.appendChild(tr);
});

function readSpends() {
  const out = {};
  CATS.forEach(c => {
    const v = Number(document.getElementById('amt_' + c.key).value) || 0;
    out[c.key] = Math.max(0, v);
  });
  return out;
}

function recompute() {
  const spends = readSpends();
  const total = Object.values(spends).reduce((s, v) => s + v, 0);

  // relatív súlyok
  CATS.forEach(c => {
    const w = total > 0 ? spends[c.key] / total : 0;
    document.getElementById('w_' + c.key).textContent = fmtPct(w);
  });

  document.getElementById('totalSpend').textContent = fmtAmt(total);

  // személyes infláció
  let personalInflation = 0;
  if (total > 0) {
    CATS.forEach(c => {
      const weight = spends[c.key] / total;
      personalInflation += weight * c.rate;
    });
  }

  const inflValue = (personalInflation * 100).toFixed(1).replace('.', ',') + '%';
  document.getElementById('personalInfl').textContent = inflValue;
}

// eseményfigyelés
document.addEventListener('DOMContentLoaded', () => {
  CATS.forEach(c => {
    document.getElementById('amt_' + c.key).addEventListener('input', recompute);
  });
  recompute();
});
</script>

</body>
</html>
