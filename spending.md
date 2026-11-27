---
layout: page
title: Egyéni fogyasztás kalkulátor
permalink: /spending
---

<h1 class="page-title">{{ page.title | escape }}</h1>


<html lang="hu">
<head>
  <meta charset="utf-8">  
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Monthly Spending Redistributor</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
  <style>
    body { background: #f8fafc; }
    .category-removed { opacity: 0.5; }
    .badge-fixed { font-variant-numeric: tabular-nums; }
    .table thead th { white-space: nowrap; }

    /* Page-scoped nav overrides (Materialize markup) */
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
  
    /* === Calculator visual refresh === */
    .calculator-shell{background:linear-gradient(135deg,#eef6ff 0%,#f8fbff 100%);border:1px solid #d7e9ff;border-radius:22px;padding:24px;box-shadow:0 14px 36px rgba(13,110,253,.08)}
    .calculator-kicker{font-size:.75rem;font-weight:800;letter-spacing:.1em;text-transform:uppercase;color:#0d6efd;margin-bottom:6px}
    .calculator-shell .card{border:1px solid #e3eaf2;border-radius:16px;overflow:hidden;box-shadow:0 8px 22px rgba(15,23,42,.06)!important}
    .input-card{border-top:4px solid #0d6efd!important}
    #monthlyInput{background:#eaf4ff!important;border:2px solid #90c2ff!important;border-radius:10px!important;font-size:1.35rem!important;font-weight:800!important;padding:.75rem 1rem!important}
    #monthlyInput:focus{background:#fff7d6!important;border-color:#e0a800!important;box-shadow:0 0 0 3px rgba(224,168,0,.14)!important}
    .calculator-shell .form-check{background:#f8fafc;border:1px solid #e6ebf1;border-radius:10px;padding:.65rem .8rem .65rem 2.3rem;margin-bottom:.5rem!important}
    .calculator-shell .form-check-input{margin-left:-1.45rem}
    .spending-table thead th{background:#f1f5f9!important;color:#475569!important;font-size:.75rem;text-transform:uppercase;letter-spacing:.03em}
    .spending-table tbody tr:not(.category-removed) td:last-child .badge{background:#eaf4ff!important;color:#0756c9!important;border:1px solid #b9d9ff}
    .spending-table tfoot th{background:#eaf2fb!important;font-weight:800!important}
    .summary-card{background:linear-gradient(135deg,#0d6efd,#0756c9)!important;color:#fff!important;border:0!important}
    .summary-card h2,.summary-card li{color:#fff!important}
    .summary-card .text-muted{color:rgba(255,255,255,.84)!important}
    @media(max-width:768px){.calculator-shell{padding:14px}}


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

/* Adam on FIRE palette refinement */
 .calculator-shell #monthlyInput,.calculator-shell #monthlyInput:hover,.calculator-shell #monthlyInput:focus{background:#162f53!important;color:#fff!important;-webkit-text-fill-color:#fff!important;caret-color:#fff;border-color:#79baff!important;}
.calculator-shell #monthlyInput:focus{border-color:#f2bd79!important;}
.calculator-shell .spending-table h2{color:#fff!important;}

/* Homepage palette: explicit table header styling */
.calculator-shell .spending-table .table > thead > tr > th {
  --bs-table-bg:#173c72; --bs-table-color:#fff; --bs-table-accent-bg:transparent;
  --bs-table-bg-state:transparent; --bs-table-bg-type:transparent;
  background:#173c72 !important; color:#fff !important;
  -webkit-text-fill-color:#fff; font-weight:700 !important;
  border-color:#294367 !important; border-bottom:2px solid #79baff !important;
  box-shadow:none !important;
}

/* White text throughout the spending results table. */
.calculator-shell .spending-table .table {
  --bs-table-color:#fff;
  --bs-table-striped-color:#fff;
  --bs-table-hover-color:#fff;
  --bs-table-active-color:#fff;
}
.calculator-shell .spending-table .table > tbody > tr > td,
.calculator-shell .spending-table .table > tfoot > tr > th,
.calculator-shell .spending-table .table > tbody > tr > td .badge,
.calculator-shell .spending-table .table > tfoot > tr > th .badge {
  --bs-table-color:#fff;
  --bs-table-color-type:#fff;
  --bs-table-color-state:#fff;
  color:#fff !important;
}
.calculator-shell .spending-table .table > tbody > tr.category-removed {opacity:1;}

</style>
</head>
<body>
  <div class="container py-4">
    <div class="calculator-shell">
      <div class="calculator-kicker">Interaktív kalkulátor</div>
    <p class="text-muted mb-4">
      Add meg a havi költésedet. A kalkulátor a magyar fogyasztói kosár súlyai szerint osztja szét.
      A kijelölt tételek eltávolításra kerülnek, majd a súlyuk arányosan újraelosztódik a maradék kategóriák között. A kalkulátor lakbért nem számol, ezt érdemes kivonni a teljes költségvetésből.
    </p>

    <div class="row g-4 align-items-start">
      <div class="col-md-6">
        <div class="card shadow-sm mb-4 summary-card">
          <div class="card-body">
            <h2 class="h6 mb-2">Összefoglaló</h2>
            <ul class="small text-muted mb-0">
              <li>Az eredeti súlyok a KSH fogyasztói kosárból származnak normalizálva 100%-ra.</li>
              <li>Az eltávolított kategóriák súlya arányosan kerül szétosztásra a megmaradt kategóriák között.</li>
            </ul>
          </div>
        </div>

        <div class="card shadow-sm input-card">
          <div class="card-body">
            <label for="monthlyInput" class="form-label">Havi átlagos költés</label>
            <div class="input-group mb-3">
              <input id="monthlyInput" type="number" class="form-control" min="0" step="100" value="0" />
            </div>

            <div class="form-check mb-2">
              <input class="form-check-input" type="checkbox" id="noSmoke">
              <label class="form-check-label" for="noSmoke">Nem dohányzom</label>
            </div>
            <div class="form-check mb-2">
              <input class="form-check-input" type="checkbox" id="noDrink">
              <label class="form-check-label" for="noDrink">Nem iszom alkoholt</label>
            </div>
            <div class="form-check mb-2">
              <input class="form-check-input" type="checkbox" id="noHouse">
              <label class="form-check-label" for="noHouse">Nincs saját házam</label>
            </div>
            <div class="form-check">
              <input class="form-check-input" type="checkbox" id="noCar">
              <label class="form-check-label" for="noCar">Nincs autóm</label>
            </div>

            <div id="removedAlert" class="alert alert-secondary mt-3 mb-0" role="alert">
              Eltávolított eredeti súly összesen: <strong><span id="removedPct">0.0</span>%</strong>
            </div>
          </div>
        </div>
      </div>

      <div class="col-md-6">
        <div class="card mt-md-0 mt-4 shadow-sm spending-table">
          <div class="card-body table-responsive">
            <h2 class="h6 mb-3">Kategóriák és havi átlagos költés</h2>
            <table class="table table-sm table-striped align-middle">
              <thead>
                <tr>
                  <th>Kategória</th>
                  <th class="text-end">Súly (eredeti)</th>
                  <th class="text-end">Súly (új)</th>
                  <th class="text-end">Összeg</th>
                </tr>
              </thead>
              <tbody id="tableBody"></tbody>
              <tfoot>
                <tr>
                  <th>Összesen</th>
                  <th class="text-end">100,0%</th>
                  <th class="text-end">100,0%</th>
                  <th class="text-end"><span id="totalCell" class="badge bg-light text-dark badge-fixed">0,00</span></th>
                </tr>
              </tfoot>
            </table>
          </div>
        </div>
        <p class="text-muted small mt-2 mb-0">Megjegyzés: a pénznem tetszőleges; a táblázatban szereplő összegek a megadott havi összegből számolódnak.</p>
      </div>
    </div>
    </div>
  </div>

  <script>
    const BASE = [
      { key: "elelmiszer", label: "Élelmiszer", weight: 0.2274 },
      { key: "alkohol", label: "Alkohol", weight: 0.0325 },
      { key: "dohanyaru", label: "Dohányárú", weight: 0.0591 },
      { key: "ruhazat", label: "Ruházat", weight: 0.0341 },
      { key: "rezsi_lakas", label: "Rezsi és lakáshoz kötött költségek", weight: 0.1152 },
      { key: "lakber_karb", label: "Lakberendezés és lakás karbantartása", weight: 0.0717 },
      { key: "egeszsegugy", label: "Egészségügy", weight: 0.0545 },
      { key: "auto_kozlekedes", label: "Közlekedés saját autóval", weight: 0.0872 },
      { key: "auto_vasarlas", label: "Saját autó értékvesztése", weight: 0.0437 },
      { key: "egyeb_kozlekedes", label: "Egyéb közlekedés", weight: 0.0140 },
      { key: "tavkozles", label: "Távközlés", weight: 0.0422 },
      { key: "oktatas", label: "Oktatás", weight: 0.0222 },
      { key: "szabadido", label: "Szabadidő és hobbi", weight: 0.0734 },
      { key: "vendeglatas", label: "Vendéglátás és szálláshely", weight: 0.0495 },
      { key: "egyeb_szolg", label: "Egyéb szolgáltatás (pl. biztosítások, banki díjak)", weight: 0.0733 },
    ];

    const fmtPct = (v) => (v * 100).toFixed(1).replace('.', ',');
    const fmtAmt = (v) => new Intl.NumberFormat(undefined, { minimumFractionDigits: 2, maximumFractionDigits: 2 }).format(v);

    function redistribute(base, removedSet) {
      const keep = base.filter(c => !removedSet.has(c.key));
      const removed = base.filter(c => removedSet.has(c.key));
      const sumKeep = keep.reduce((s, c) => s + c.weight, 0);
      const sumRemoved = removed.reduce((s, c) => s + c.weight, 0);
      if (sumKeep <= 0) return base.map(c => ({ ...c, adjWeight: 0 }));
      const adjusted = base.map(c => {
        if (removedSet.has(c.key)) return { ...c, adjWeight: 0 };
        const share = c.weight / sumKeep;
        const adjWeight = share * (sumKeep + sumRemoved);
        return { ...c, adjWeight };
      });
      const totalAdj = adjusted.reduce((s, c) => s + c.adjWeight, 0);
      return adjusted.map(c => ({ ...c, adjWeight: c.adjWeight / totalAdj }));
    }

    function update() {
      const monthly = Math.max(0, Number(document.getElementById('monthlyInput').value) || 0);
      const removedSet = new Set();
      if (document.getElementById('noSmoke').checked) removedSet.add('dohanyaru');
      if (document.getElementById('noDrink').checked) removedSet.add('alkohol');
      if (document.getElementById('noHouse').checked) removedSet.add('lakber_karb');
      if (document.getElementById('noCar').checked) ['auto_kozlekedes', 'auto_vasarlas'].forEach(item => removedSet.add(item));

      const adjusted = redistribute(BASE, removedSet);
      const raw = adjusted.map(r => r.adjWeight * monthly);
      const rounded = raw.map(v => Math.round(v * 100) / 100);
      const sumRounded = rounded.reduce((s, v) => s + v, 0);
      const diff = Math.round((monthly - sumRounded) * 100) / 100;
      let idxMax = -1, maxW = -Infinity;
      adjusted.forEach((r, i) => { if (r.adjWeight > maxW) { maxW = r.adjWeight; idxMax = i; } });
      if (idxMax >= 0) rounded[idxMax] = Math.round((rounded[idxMax] + diff) * 100) / 100;

      const tbody = document.getElementById('tableBody');
      tbody.innerHTML = '';
      adjusted.forEach((r, i) => {
        const tr = document.createElement('tr');
        if (r.adjWeight === 0) tr.classList.add('category-removed');
        tr.innerHTML = `
          <td>${r.label}</td>
          <td class="text-end">${fmtPct(BASE[i].weight)}%</td>
          <td class="text-end">${fmtPct(r.adjWeight)}%</td>
          <td class="text-end"><span class="badge bg-light text-dark badge-fixed">${fmtAmt(rounded[i])}</span></td>
        `;
        tbody.appendChild(tr);
      });

      const removedPct = BASE.filter(c => removedSet.has(c.key)).reduce((s, c) => s + c.weight, 0);
      document.getElementById('removedPct').textContent = (removedPct * 100).toFixed(1).replace('.', ',');
      document.getElementById('totalCell').textContent = fmtAmt(monthly);
    }

    document.addEventListener('DOMContentLoaded', () => {
      ['monthlyInput', 'noSmoke', 'noDrink', 'noHouse', 'noCar'].forEach(id => {
        const el = document.getElementById(id);
        el.addEventListener(el.type === 'number' ? 'input' : 'change', update);
      });
      update();
    });
  </script>
</body>
</html>

