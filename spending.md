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
border-bottom: 0 !important; /* handles themes that fake underline as border */
box-shadow: none !important; /* handles themes using bottom shadow */
}


/* Active item variants */
nav.blue.accent-4 .nav-wrapper ul.right.hide-on-med-and-down > li.active > a,
nav.blue.accent-4 .nav-wrapper ul.right.hide-on-med-and-down > li > a.active {
text-decoration: none !important;
border-bottom: 0 !important;
box-shadow: none !important;
}


/* Kill any pseudo-element underline decorations */
nav.blue.accent-4 .nav-wrapper ul.right.hide-on-med-and-down > li > a::after {
content: none !important;
border: 0 !important;
box-shadow: none !important;
}


/* Keep icons themselves clean */
nav.blue.accent-4 .nav-wrapper ul.right.hide-on-med-and-down > li > a .material-icons,
nav.blue.accent-4 .nav-wrapper ul#nav-mobile.side-nav li > a .material-icons {
text-decoration: none;
display: inline-flex;
vertical-align: middle;
}


/* --- NEW: fekete szöveg a havi átlagos költés táblázathoz --- */
.spending-table,
.spending-table h2,
.spending-table .table,
.spending-table .table th,
.spending-table .table td,
.spending-table .badge {
color: #000 !important;
}
</style>
</head>
<body>
<div class="container py-4">
<p class="text-muted mb-4">
Add meg a havi költésedet. A kalkulátor a magyar fogyasztói kosár súlyai szerint osztja szét.
A kijelölt tételek eltávolításra kerülnek, majd a súlyuk arányosan újraelosztódik a maradék kategóriák között. A kalkulátor lakbért nem számol, ezt érdemes kivonni a teljes költségvetésből.
</p>


<!--
Új elrendezés:
- Bal oszlop: Összefoglaló (fent), Havi átlagos költés (alatta)
- Jobb oszlop (>= md): Kategóriák táblázata
- < md: oszlopok egymás alatt jelennek meg (mobilon marad, ahogy volt)
-->
<div class="row g-4 align-items-start">
<!-- Bal oszlop -->
<div class="col-md-6">
<!-- Összefoglaló KÁRTYA – felülre helyezve -->
<div class="card shadow-sm mb-4">
<div class="card-body">
<h2 class="h6 mb-2">Összefoglaló</h2>
<ul class="small text-muted mb-0">
<li>Az eredeti súlyok a KSH fogyasztói kosárból származnak normalizálva 100%-ra.</li>
<li>Az eltávolított kategóriák súlya arányosan kerül szétosztásra a megmaradt kategóriák között.</li>
</ul>
</div>
</div>


<!-- Havi átlagos költés KÁRTYA -->
<div class="card shadow-sm">
<div class="card-body">
<label for="monthlyInput" class="form-label">Havi átlagos költés</label>
</html>