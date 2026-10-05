---
layout: page
title: FIRE blog
permalink: /blog
---

<style>
.blog-header { margin: 55px 0 40px; }
.blog-header .eyebrow { font-size: 12px; font-weight: 700; letter-spacing: 2px; text-transform: uppercase; color: #2962ff; margin-bottom: 8px; }
.blog-header h1 { margin: 0; font-size: 48px; font-weight: 700; letter-spacing: -1.5px; }
.blog-header p { margin-top: 12px; max-width: 650px; font-size: 18px; line-height: 1.6; color: #666; }
.blog-section-title { display: flex; align-items: center; gap: 18px; margin: 45px 0 28px; }
.blog-section-title h4 { margin: 0; font-weight: 600; white-space: nowrap; }
.blog-section-title:after { content: ""; flex: 1; height: 1px; background: #e0e0e0; }
.blog-grid { display: flex; flex-wrap: wrap; }
.blog-grid > .col { display: flex; margin-bottom: 24px; }
.blog-grid > .col > a { display: flex; width: 100%; }
.blog-card { width: 100%; height: 100%; display: flex; flex-direction: column; border-radius: 12px; overflow: hidden; background: #4f83d1; color: white; border: 1px solid rgba(255,255,255,.15); box-shadow: 0 3px 12px rgba(0,0,0,.07); transition: transform .22s ease, box-shadow .22s ease, background .22s ease; }
.blog-card:hover { transform: translateY(-5px); box-shadow: 0 12px 30px rgba(13,71,161,.20); background: #4779bf; }
.blog-card .card-content { flex: 1; }
.blog-meta { display: flex; gap: 8px; margin-bottom: 15px; align-items: center; }
.blog-category { display: inline-block; background: rgba(255,255,255,.16); color: white; border: 1px solid rgba(255,255,255,.28); border-radius: 20px; padding: 4px 10px; font-size: 11px; font-weight: 700; letter-spacing: .4px; text-transform: uppercase; }
.blog-date { font-size: 12px; color: rgba(255,255,255,.72); }
.blog-card .card-title { font-size: 23px; line-height: 1.25; margin-bottom: 14px !important; }
.blog-card .card-content p { font-size: 15px; line-height: 1.65; color: rgba(255,255,255,.90); }
.blog-card .card-action { border-top: 1px solid rgba(255,255,255,.20); color: white; font-weight: 600; text-transform: none; letter-spacing: 0; }
.arrow { display: inline-block; transition: transform .2s ease; }
.blog-card:hover .arrow, .blog-featured:hover .arrow { transform: translateX(5px); }
.blog-featured { position: relative; border-radius: 16px; overflow: hidden; background: linear-gradient(135deg,#0d47a1 0%,#2962ff 100%); color: white; padding: 42px 45px; margin-bottom: 45px; box-shadow: 0 15px 40px rgba(41,98,255,.18); transition: transform .22s ease, box-shadow .22s ease; }
.blog-featured:hover { transform: translateY(-3px); box-shadow: 0 20px 45px rgba(41,98,255,.24); }
.blog-featured .featured-label { font-size: 11px; letter-spacing: 2px; text-transform: uppercase; font-weight: 700; opacity: .8; }
.blog-featured h2 { font-size: 35px; font-weight: 700; line-height: 1.15; margin: 12px 0 16px; max-width: 700px; }
.blog-featured p { font-size: 17px; line-height: 1.6; max-width: 700px; opacity: .9; }
.blog-featured .featured-link { display: inline-block; margin-top: 16px; color: white; font-weight: 700; font-size: 15px; }
.blog-featured .featured-hitbox { position: absolute; inset: 0; z-index: 10; display: block; }
.blog-featured > *:not(.featured-hitbox) { position: relative; z-index: 2; }
.blog-featured:after { content: "FIRE"; position: absolute; right: -10px; bottom: -45px; font-size: 150px; font-weight: 900; letter-spacing: -10px; opacity: .055; pointer-events: none; }
@media only screen and (max-width: 600px) { .blog-header { margin: 35px 0 30px; } .blog-header h1 { font-size: 38px; } .blog-header p { font-size: 16px; } .blog-featured { padding: 30px 25px; } .blog-featured h2 { font-size: 28px; } .blog-featured:after { font-size: 100px; } .blog-section-title h4 { font-size: 1.7rem; } }
</style>

<div class="blog-header">
  <div class="eyebrow">Adam on FIRE</div>
  <h1>{{ page.title | escape }}</h1>
  <p>Befektetés, pénzügyi függetlenség és az élet a FIRE felé vezető úton — számokkal, tapasztalatokkal és néha tévedésekkel.</p>
</div>

<div class="blog-featured">
  <a class="featured-hitbox" href="/blog-15" aria-label="Brain Bar és a kötvénypiacok"></a>
  <div class="featured-label">Legfrissebb bejegyzés · Befektetés · 2026</div>
  <h2>Brain Bar és a kötvénypiacok</h2>
  <p>Brain Bar előadás, 5% fölötti amerikai kötvényhozamok és egy új portfólió-vizualizáció. Gondolatok arról, mit jelenthet a tartósan magas kamatkörnyezet a részvény- és kötvénypiacoknak.</p>
  <div class="featured-link">Olvasd tovább <span class="arrow">→</span></div>
</div>

<div class="section">
  <div class="blog-section-title"><h4>Összes korábbi bejegyzés</h4></div> 
  <div class="row blog-grid">
    <div class="col s12 m6">
      <a href="/blog-14" style="color: inherit;">
        <div class="card hoverable blog-card">
          <div class="card-content">
            <div class="blog-meta"><span class="blog-category">Élet</span><span class="blog-date">2026</span></div>
            <span class="card-title"><strong>Irányvesztés és nyári depresszió</strong></span>
            <p>A 3 napos munkahét első hónapjai nem hozták automatikusan a várt szabadságérzést. Gondolatok motivációról, post-FIRE célokról és a Bátor Táborban szerzett tapasztalatokról.</p>
          </div>
          <div class="card-action">Olvasd tovább <span class="arrow">→</span></div>
        </div>
      </a>
    </div>
    <div class="col s12 m6">
      <a href="/blog-13" style="color: inherit;">
        <div class="card hoverable blog-card">
          <div class="card-content">
            <div class="blog-meta"><span class="blog-category">Utazás</span><span class="blog-date">2026</span></div>
            <span class="card-title"><strong>Az első autós nyaralásom tanulságai</strong></span>
            <p>1700 kilométer nyolc nap alatt Ausztriában és Szlovéniában. Mit tanultam az autós utazásról, az árakról és arról, mennyire más élmény így nyaralni?</p>
          </div>
          <div class="card-action">Olvasd tovább <span class="arrow">→</span></div>
        </div>
      </a>
    </div>
    <div class="col s12 m6">
      <a href="/blog-12" style="color: inherit;">
        <div class="card hoverable blog-card">
          <div class="card-content">
            <div class="blog-meta"><span class="blog-category">FIRE</span><span class="blog-date">2026</span></div>
            <span class="card-title"><strong>Bátor Tábor, FIRE előadások, és a 3-napos munkarend</strong></span>
            <p>FIRE-előadások, Bátor Táboros önkéntesség és egy fontos döntés: júniustól heti három nap munka, több idő a saját projektekre és fokozatosabb átmenet a teljes FIRE felé.</p>
          </div>
          <div class="card-action">Olvasd tovább <span class="arrow">→</span></div>
        </div>
      </a>
    </div>
    <div class="col s12 m6">
      <a href="/blog-11" style="color: inherit;">
        <div class="card hoverable blog-card">
          <div class="card-content">
            <div class="blog-meta"><span class="blog-category">Politika</span><span class="blog-date">2026</span></div>
            <span class="card-title"><strong>Vége az Orbán-rendszernek</strong></span>
            <p>141 mandátum, kétharmados Tisza-győzelem és egy korszak vége. Személyes visszatekintés a választásra, a forint reakciójára és egy választási integritási szimuláció kulisszái mögé.</p>
          </div>
          <div class="card-action">Olvasd tovább <span class="arrow">→</span></div>
        </div>
      </a>
    </div>
    <div class="col s12 m6">
      <a href="/blog-10" style="color: inherit;">
        <div class="card hoverable blog-card">
          <div class="card-content">
            <div class="blog-meta"><span class="blog-category">Politika</span><span class="blog-date">2026</span></div>
            <span class="card-title"><strong>Beindult a választási szezon</strong></span>
            <p>Már csak 24 nap van a magyar választásig. Várakozások a kampány hajrájáról, politikai előadásokról és arról, hogyan befolyásolhatja az eredmény a következő éveket.</p>
          </div>
          <div class="card-action">Olvasd tovább <span class="arrow">→</span></div>
        </div>
      </a>
    </div>
    <div class="col s12 m6">
      <a href="/blog-9" style="color: inherit;">
        <div class="card hoverable blog-card">
          <div class="card-content">
            <div class="blog-meta"><span class="blog-category">TBSZ</span><span class="blog-date">2026</span></div>
            <span class="card-title"><strong>Az első TBSZ mozgatás tanulságai</strong></span>
            <p>Hat év befektetés után először kellett lejáró TBSZ-t mozgatnom. Tranzakciós díjak, többnapos újrabefektetés és néhány tanulság a következő transzferhez.</p>
          </div>
          <div class="card-action">Olvasd tovább <span class="arrow">→</span></div>
        </div>
      </a>
    </div>
    <div class="col s12 m6">
      <a href="/blog-8" style="color: inherit;">
        <div class="card hoverable blog-card">
          <div class="card-content">
            <div class="blog-meta"><span class="blog-category">FIRE</span><span class="blog-date">2026</span></div>
            <span class="card-title"><strong>Visszatekintés 2025-re és előretekintés 2026-ra</strong></span>
            <p>2025 végére sikerült elérnem a FIRE célomat, a nagyjából 600 ezer eurós vagyont. Visszatekintés a portfólióra és arra, mi következik 2026-ban.</p>
          </div>
          <div class="card-action">Olvasd tovább <span class="arrow">→</span></div>
        </div>
      </a>
    </div>
    <div class="col s12 m6">
      <a href="/blog-7" style="color: inherit;">
        <div class="card hoverable blog-card">
          <div class="card-content">
            <div class="blog-meta"><span class="blog-category">Utazás</span><span class="blog-date">2025</span></div>
            <span class="card-title"><strong>Japán a legjobb hely nyaralásra</strong></span>
            <p>Japán sokak fejében továbbra is drága úti cél, pedig a gyenge jen és az alacsony árszínvonal miatt meglepően kedvező lehet egy utazás.</p>
          </div>
          <div class="card-action">Olvasd tovább <span class="arrow">→</span></div>
        </div>
      </a>
    </div>
    <div class="col s12 m6">
      <a href="/blog-6" style="color: inherit;">
        <div class="card hoverable blog-card">
          <div class="card-content">
            <div class="blog-meta"><span class="blog-category">FIRE</span><span class="blog-date">2025</span></div>
            <span class="card-title"><strong>Megkaptam a zöld lámpát a FIRE-re</strong></span>
            <p>Hogyan lehet ténylegesen felmérni egy portfólió FIRE-készültségét, és honnan lehet tudni, hogy pénzügyileg valóban minden a helyén van?</p>
          </div>
          <div class="card-action">Olvasd tovább <span class="arrow">→</span></div>
        </div>
      </a>
    </div>
    <div class="col s12 m6">
      <a href="/blog-5" style="color: inherit;">
        <div class="card hoverable blog-card">
          <div class="card-content">
            <div class="blog-meta"><span class="blog-category">Adatok</span><span class="blog-date">2025</span></div>
            <span class="card-title"><strong>Új vizualizációk</strong></span>
            <p>A FIRE-utam egyik legfontosabb része a transzparencia: részletes adatokkal és vizualizációkkal mutatom meg, hogyan változik a portfólióm és a vagyonom.</p>
          </div>
          <div class="card-action">Olvasd tovább <span class="arrow">→</span></div>
        </div>
      </a>
    </div>
    <div class="col s12 m6">
      <a href="/blog-4" style="color: inherit;">
        <div class="card hoverable blog-card">
          <div class="card-content">
            <div class="blog-meta"><span class="blog-category">Élet</span><span class="blog-date">2025</span></div>
            <span class="card-title"><strong>Elkezdtem kosarazni</strong></span>
            <p>Egy hosszabb betegség után új hobbit kerestem, és végül a kosárlabdánál kötöttem ki. Egy személyesebb bejegyzés a FIRE-en túli életről.</p>
          </div>
          <div class="card-action">Olvasd tovább <span class="arrow">→</span></div>
        </div>
      </a>
    </div>
    <div class="col s12 m6">
      <a href="/blog-3" style="color: inherit;">
        <div class="card hoverable blog-card">
          <div class="card-content">
            <div class="blog-meta"><span class="blog-category">Befektetés</span><span class="blog-date">2025</span></div>
            <span class="card-title"><strong>Elkészült a portfóliókövetőm</strong></span>
            <p>A piaci turbulencia megmutatta, hogy jobb rendszerre van szükségem a portfólióm követéséhez. Így született meg a saját portfóliókövetőm.</p>
          </div>
          <div class="card-action">Olvasd tovább <span class="arrow">→</span></div>
        </div>
      </a>
    </div>
    <div class="col s12 m6">
      <a href="/blog-2" style="color: inherit;">
        <div class="card hoverable blog-card">
          <div class="card-content">
            <div class="blog-meta"><span class="blog-category">Befektetés</span><span class="blog-date">2025</span></div>
            <span class="card-title"><strong>Trump miatt én is pánikoltam</strong></span>
            <p>A piacok hirtelen esése engem is próbára tett. Mit csináltam a portfóliómmal, hogyan reagáltam, és mit tanultam a saját viselkedésemből?</p>
          </div>
          <div class="card-action">Olvasd tovább <span class="arrow">→</span></div>
        </div>
      </a>
    </div>
    <div class="col s12 m6">
      <a href="/blog-1" style="color: inherit;">
        <div class="card hoverable blog-card">
          <div class="card-content">
            <div class="blog-meta"><span class="blog-category">FIRE</span><span class="blog-date">2025</span></div>
            <span class="card-title"><strong>Még 550 nap van hátra</strong></span>
            <p>A számításaim szerint 2026 közepére érhetem el a FIRE-célomat. De mit jelent ez akkor, amikor közben a részvénypiacok történelmi magasságokban járnak?</p>
          </div>
          <div class="card-action">Olvasd tovább <span class="arrow">→</span></div>
        </div>
      </a>
    </div>
  </div>
</div>
