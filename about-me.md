---
layout: page
title: Rólam
permalink: /about-me
---

<style>
.about-fire {--blue:#2962ff;--deep:#0d47a1;--line:#d6e2f7;--ink:#24324a;--muted:#64748b;margin:8px auto 65px;}
.about-fire *{box-sizing:border-box}
.about-fire .eyebrow{color:var(--blue);font-size:12px;font-weight:700;letter-spacing:2px;text-transform:uppercase}
.about-fire .hero{margin:55px 0 36px}
.about-fire h1{font-size:48px;letter-spacing:-1.5px;font-weight:700;margin:8px 0 12px}
.about-fire .lead{font-size:18px;line-height:1.7;color:#666;max-width:790px}
.about-fire h2{font-size:26px;color:var(--deep);font-weight:700;display:flex;align-items:center;gap:16px;margin:35px 0 24px}
.about-fire h2:after{content:"";height:1px;background:var(--line);flex:1}
.about-fire .intro{display:grid;grid-template-columns:minmax(0,1.65fr) minmax(260px,1fr);gap:25px;align-items:start}
.about-fire .panel{border:1px solid var(--line);border-radius:14px;background:#fff;padding:28px;box-shadow:0 6px 24px rgba(13,71,161,.06)}
.about-fire .panel p{line-height:1.85;color:var(--ink);margin:0 0 17px}
.about-fire .panel p:last-child{margin-bottom:0}
.about-fire .portrait{width:100%;max-height:320px;object-fit:cover;object-position:center 30%;border-radius:10px;margin-bottom:17px}
.about-fire .small-label{font-size:12px;color:var(--blue);font-weight:700;text-transform:uppercase;letter-spacing:1.2px}
.about-fire .aside-title{font-size:21px;font-weight:700;color:var(--deep);margin:8px 0 15px}
.about-fire .facts{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:16px;margin:25px 0 8px}
.about-fire .fact{background:#f3f7ff;border:1px solid var(--line);border-radius:12px;padding:20px}
.about-fire .fact strong{display:block;color:var(--deep);font-size:25px;margin-bottom:5px}
.about-fire .fact span{color:#52617a;font-size:14px;line-height:1.5}
.about-fire .media-grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:22px}
.about-fire .media-card{border-radius:14px;overflow:hidden;background:linear-gradient(135deg,#2f6fd0 0%,#4e86dd 100%);color:#fff;box-shadow:0 8px 22px rgba(13,71,161,.14);display:flex;flex-direction:column;transition:transform .22s,box-shadow .22s}
.about-fire .media-card:hover{transform:translateY(-4px);box-shadow:0 14px 32px rgba(13,71,161,.22)}
.about-fire .media-body{padding:23px;flex:1}
.about-fire .media-card .kind{color:#e0ecff;font-size:12px;letter-spacing:1px;font-weight:700;text-transform:uppercase}
.about-fire .media-card h3{font-size:21px;line-height:1.35;font-weight:700;color:white;margin:9px 0 12px}
.about-fire .media-card p{color:rgba(255,255,255,.91);line-height:1.65;margin:0}
.about-fire .media-action{padding:15px 23px;background:rgba(8,45,104,.14);border-top:1px solid rgba(255,255,255,.2)}
.about-fire .media-action a{color:white!important;font-weight:700;text-transform:none!important}
.about-fire .media-preview{height:140px;background:#eaf1ff;padding:22px;display:flex;flex-direction:column;justify-content:center;gap:12px}
.about-fire .media-preview .publisher{color:var(--deep);font-size:25px;font-weight:800;letter-spacing:-.7px}
.about-fire .media-preview .preview-note{color:#60718f;font-size:13px}
.about-fire .video-wrap{position:relative;width:100%;padding-top:56.25%;background:#0b1d39}
.about-fire .video-wrap iframe{position:absolute;inset:0;width:100%;height:100%;border:0}
.about-fire .links{display:flex;flex-wrap:wrap;gap:12px;margin-top:20px}
.about-fire .link-pill{display:inline-block;border:1px solid #c8d9f8;border-radius:9px;padding:12px 18px;color:var(--deep)!important;font-weight:700;background:#f5f8ff;transition:background .2s}
.about-fire .link-pill:hover{background:#e3edff}
.about-fire .disclaimer{font-size:13px;color:#64748b;line-height:1.7;margin-top:25px}
@media(max-width:800px){.about-fire .intro{grid-template-columns:1fr}.about-fire .facts{grid-template-columns:1fr 1fr}}
@media(max-width:600px){.about-fire .hero{margin:35px 0 28px}.about-fire h1{font-size:38px}.about-fire .lead{font-size:16px}.about-fire h2{font-size:23px}.about-fire .panel{padding:20px}.about-fire .facts,.about-fire .media-grid{grid-template-columns:1fr}}

/* Interactive chronological timeline */
.about-fire .timeline{position:relative;margin:26px 0 48px;padding:22px 0 12px}
.about-fire .timeline:before{content:"";position:absolute;left:0;right:0;top:58px;height:4px;background:linear-gradient(90deg,#b6cef9,#2962ff);border-radius:4px}
.about-fire .timeline-track{display:grid;grid-template-columns:repeat(8,minmax(0,1fr));gap:4px;position:relative}
.about-fire .timeline-item{position:relative;min-width:0;text-align:center}
.about-fire .timeline-item summary{cursor:pointer;list-style:none;display:flex;flex-direction:column;align-items:center;gap:11px;color:#0d47a1;font-weight:700;font-size:13px;outline-offset:5px}
.about-fire .timeline-item summary::-webkit-details-marker{display:none}
.about-fire .timeline-date{height:24px;white-space:nowrap;font-size:12px}
.about-fire .timeline-dot{width:20px;height:20px;border:4px solid #2962ff;border-radius:50%;background:#fff;z-index:1;transition:transform .2s,background .2s}
.about-fire .timeline-item[open] .timeline-dot,.about-fire .timeline-item summary:hover .timeline-dot{background:#2962ff;transform:scale(1.15)}
.about-fire .timeline-year{font-size:13px;color:#0d47a1}
.about-fire .timeline-detail{position:relative;margin:14px -35px 0;padding:14px;border:1px solid #c8d9f8;border-radius:10px;background:#f3f7ff;box-shadow:0 6px 18px rgba(13,71,161,.08);color:#24324a;font-size:13px;line-height:1.6;z-index:3;text-align:left}
.about-fire .timeline-item:first-child .timeline-detail{margin-left:0}
.about-fire .timeline-item:last-child .timeline-detail{margin-right:0}
.about-fire .timeline-note{font-size:13px;color:#64748b;margin:12px 0}
.about-fire .playlist-panel{border:1px solid #d6e2f7;border-radius:14px;overflow:hidden;background:#fff}
.about-fire .playlist-panel .video-wrap{max-width:100%}
.about-fire .playlist-info{padding:20px 24px;color:#24324a;line-height:1.7}
.about-fire .playlist-info strong{color:#0d47a1}
@media(max-width:800px){.about-fire .timeline:before{left:16px;right:auto;top:0;bottom:0;width:4px;height:auto}.about-fire .timeline-track{display:flex;flex-direction:column;gap:14px}.about-fire .timeline-item{text-align:left;padding-left:0}.about-fire .timeline-item summary{flex-direction:row;gap:12px}.about-fire .timeline-date{order:2;height:auto;min-width:95px}.about-fire .timeline-dot{order:1;flex:none}.about-fire .timeline-year{order:3}.about-fire .timeline-detail,.about-fire .timeline-item:first-child .timeline-detail,.about-fire .timeline-item:last-child .timeline-detail{margin:10px 0 0 34px}}
</style>

<div class="container about-fire">
  <header class="hero">
    <div class="eyebrow">Adam on FIRE</div>
    <h1>{{ page.title | escape }}</h1>
    <p class="lead">Sanyó Ádám vagyok, adatelemző, politikai elemző, kisbefektető, és podcaster.</p>
  </header>

  <section class="intro" aria-label="Bemutatkozás">
    <div class="panel">
      <div class="small-label">A történetem</div>
      <h2 style="margin-top:12px">Hogyan lettem kisbefektető?</h2>
      <p>Nem pénzügyi szakemberként, hanem a saját megtakarításaimat kezelő magánemberként kezdtem el foglalkozni a befektetésekkel. A 2012 és 2016 között Angliában éltem és dolgoztam, és alkalmazotti jövedelemből kezdtem felépíteni a vagyonomat.</p>
      <p>Az első 10 millió forint összegyűjtése különösen fontos mérföldkő volt számomra. Ekkor tudatosult bennem, hogy lehet esélyem elérni az anyagi függetlenséget. A kezdeti években hibáztam is, például devizakereskedéssel veszítettem több ezer dollárt. Ezekből a tapasztalatokból tanulva egyre inkább a hosszú távú, diverzifikált és alacsony költségű befektetések felé fordultam, különösen 2020 tavasza után, miután eladtam a lakásom, és ETF-ekbe és állampapírba fektettem a pénzt.</p>
      <p>2026-ra elértem a pénzügyi függetlenség számomra kitűzött szintjét. A FIRE elérése számomra nem a munka teljes feladását, hanem a döntési szabadságot jelenti. Azt, hogy az időmmel és a munkámmal kapcsolatos döntéseket ne kizárólag a pénz határozza meg. Ezért is szeretnék tartalomgyártóként és elemzőként a pénzügyi tudatossággal foglalkozni, továbbá a politika és pénzügy kapcsolatával.</p>
      <p>Az Adam on FIRE oldalon a saját tapasztalataimat, pénzügyi elemzéseimet és kalkulátoraimat osztom meg. A ZsugaZsonglőrök podcastban pedig a megtakarításokról, befektetésekról, és a gazdaság kérdéseiről beszélgetünk.</p>
    </div>
    <aside class="panel">
      <img class="portrait" src="{{ '/images/adam_2.jpg' | relative_url }}" alt="Sanyó Ádám portréja" loading="lazy">
      <div class="small-label">Sanyó Ádám</div>
      <div class="aside-title">Adatelemző, kisbefektető</div>
      <p>A pénzügyi függetlenséghez vezető utamról és a hosszú távú befektetés tanulságairól írok.</p>
    </aside>
  </section>

  <section aria-label="Életem fontos mérföldkövei">
    <h2>Életutam idővonalon</h2>
    <p class="timeline-note">Kattints egy évszámra vagy pontra a mérföldkő részleteiért. A 2027-es esemény terv.</p>
    <div class="timeline"><div class="timeline-track">
      <details class="timeline-item"><summary aria-label="2010 június: részletek"><span class="timeline-date">2010 június</span><span class="timeline-dot" aria-hidden="true"></span><span class="timeline-year">2010</span></summary><div class="timeline-detail">Elkezdek dolgozni Budapesten</div></details>
      <details class="timeline-item"><summary aria-label="2012 május: részletek"><span class="timeline-date">2012 május</span><span class="timeline-dot" aria-hidden="true"></span><span class="timeline-year">2012</span></summary><div class="timeline-detail">Angliába költözök, hogy karriert építsek</div></details>
      <details class="timeline-item"><summary aria-label="2015 február: részletek"><span class="timeline-date">2015 február</span><span class="timeline-dot" aria-hidden="true"></span><span class="timeline-year">2015</span></summary><div class="timeline-detail">Az első 10 millió Ft-om összegyűjtése</div></details>
      <details class="timeline-item"><summary aria-label="2018 június: részletek"><span class="timeline-date">2018 június</span><span class="timeline-dot" aria-hidden="true"></span><span class="timeline-year">2018</span></summary><div class="timeline-detail">Másoddiplomát szerzek a CEU-n üzleti elemzésből</div></details>
      <details class="timeline-item"><summary aria-label="2020 február: részletek"><span class="timeline-date">2020 február</span><span class="timeline-dot" aria-hidden="true"></span><span class="timeline-year">2020</span></summary><div class="timeline-detail">Eladom a budapesti lakásom, hogy a pénzt befektessem</div></details>
      <details class="timeline-item"><summary aria-label="2023 május: részletek"><span class="timeline-date">2023 május</span><span class="timeline-dot" aria-hidden="true"></span><span class="timeline-year">2023</span></summary><div class="timeline-detail">Kijelölöm a FIRE célom dátumát (2028)</div></details>
      <details class="timeline-item"><summary aria-label="2026 február: részletek"><span class="timeline-date">2026 február</span><span class="timeline-dot" aria-hidden="true"></span><span class="timeline-year">2026</span></summary><div class="timeline-detail">A kedvező piaci körülmények miatt 2026-ra elérem a FIRE-t</div></details>
      <details class="timeline-item"><summary aria-label="2027 május: részletek"><span class="timeline-date">2027 május</span><span class="timeline-dot" aria-hidden="true"></span><span class="timeline-year">2027</span></summary><div class="timeline-detail">Elkezdem a "második életem", 17 évnyi multinacionális karrier után</div></details>
    </div></div>
  </section>

  <section aria-labelledby="media-heading">
    <h2 id="media-heading">Médiamegjelenéseim</h2>
    <div class="media-grid">
      <article class="media-card">
        <div class="media-preview"><div class="publisher">Portfolio.hu</div><div class="preview-note">Sajtómegjelenés · 2026. október</div></div>
        <div class="media-body"><div class="kind">Cikk · Lightyear Universe 2026</div><h3>A befektetés ma már nem a gazdagok kiváltsága</h3><p>Panelbeszélgetés a pénzügyi függetlenségről, a hosszú távú befektetésről és a kisbefektetők tapasztalatairól.</p></div>
        <div class="media-action"><a href="https://www.portfolio.hu/befektetes/20261009/a-befektetes-ma-mar-nem-a-gazdagok-kivaltsaga-de-fegyelem-es-bizalom-nelkul-nincs-attores-868510" target="_blank" rel="noopener noreferrer">Cikk elolvasása →</a></div>
      </article>
      <article class="media-card">
        <div class="media-preview"><div class="publisher">Ingatlan FM</div><div class="preview-note">Interjú · 2026. június</div></div>
        <div class="media-body"><div class="kind">Interjú · FIRE</div><h3>Így érhető el az anyagi szabadság alkalmazotti fizetésből is</h3><p>Beszélgetés a vagyonépítésről, az ingatlanok és a tőzsde szerepéről, valamint a pénzügyi szabadságról.</p></div>
        <div class="media-action"><a href="https://ingatlan.fm/igy-erheto-el-az-anyagi-szabadsag-alkalmazotti-fizetesbol-is-fire/" target="_blank" rel="noopener noreferrer">Interjú megnyitása →</a></div>
      </article>
    </div>
  </section>

  <section aria-labelledby="playlist-heading">
    <h2 id="playlist-heading">ZsugaZsonglőrök – lejátszási lista</h2>
    <div class="playlist-panel">
      <div class="video-wrap"><iframe src="https://www.youtube-nocookie.com/embed/videoseries?list=PLHQj57ybEm6qScyR8Eye6lF-Te3c9IKEo" title="ZsugaZsonglőrök – YouTube lejátszási lista" loading="lazy" referrerpolicy="strict-origin-when-cross-origin" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe></div>
      <div class="playlist-info"><strong>ZsugaZsonglőrök – összes epizód</strong><p>A lejátszóban a lista további videói is kiválaszthatók. <a href="https://www.youtube.com/playlist?list=PLHQj57ybEm6qScyR8Eye6lF-Te3c9IKEo" target="_blank" rel="noopener noreferrer">Lejátszási lista megnyitása a YouTube-on →</a></p></div>
    </div>
  </section>


  <section aria-labelledby="more-heading">
    <h2 id="more-heading">További tartalmaim</h2>
    <div class="panel">
      <p>Ha érdekelnek a hosszú távú befektetések, a pénzügyi függetlenség és a gyakorlati pénzügyi számítások, az alábbi oldalakon további anyagokat találsz.</p>
      <div class="links"><a class="link-pill" href="{{ '/blog' | relative_url }}">Blogbejegyzések →</a><a class="link-pill" href="{{ '/resources' | relative_url }}">Kalkulátorok és eszközök →</a><a class="link-pill" href="{{ '/consulting' | relative_url }}">Konzultáció →</a></div>
    </div>
  </section>
</div>
