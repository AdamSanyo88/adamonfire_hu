---
layout: page
title: Hasznos eszközök
permalink: /resources
---

<style>
/* ==========================================
   ADAM ON FIRE - RESOURCES PAGE
   ========================================== */
.resources-page {
  margin-top: 8px;
}

.resources-header {
  margin: 55px 0 40px;
}

.resources-header .eyebrow {
  margin-bottom: 8px;
  color: #2962ff;
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 2px;
  text-transform: uppercase;
}

.resources-header h1 {
  margin: 0;
  font-size: 48px;
  font-weight: 700;
  letter-spacing: -1.5px;
}

.resources-header p {
  max-width: 650px;
  margin-top: 12px;
  color: #666;
  font-size: 18px;
  line-height: 1.6;
}

.resources-page .section > h4 {
  display: flex;
  align-items: center;
  gap: 16px;
  margin: 20px 0 26px !important;
  color: #0d47a1;
  font-weight: 700;
}

.resources-page .section > h4::after {
  content: "";
  flex: 1;
  height: 1px;
  background: #d6e2f7;
}

.resources-page .card {
  overflow: hidden;
  border-radius: 14px;
  border: 1px solid rgba(255,255,255,.22);
  background: linear-gradient(135deg, #2f6fd0 0%, #4e86dd 100%);
  color: #fff;
  box-shadow: 0 8px 22px rgba(13,71,161,.14);
  transition: transform .22s ease, box-shadow .22s ease, filter .22s ease;
}

.resources-page .card:hover {
  transform: translateY(-4px);
  box-shadow: 0 14px 32px rgba(13,71,161,.22);
  filter: brightness(.98);
}

.resources-page .card-content {
  color: #fff;
}

.resources-page .card-title,
.resources-page .card-title strong,
.resources-page .card-content p {
  color: #fff !important;
}

.resources-page .card-title {
  line-height: 1.3 !important;
}

.resources-page .card-content p {
  color: rgba(255,255,255,.90) !important;
  line-height: 1.65;
}

.resources-page .card-action {
  border-top: 1px solid rgba(255,255,255,.20) !important;
  background: rgba(8,45,104,.14);
  color: #fff !important;
  font-weight: 700;
}

.resources-page .card-action a,
.resources-page > .section .card-action a {
  color: #fff !important;
  text-transform: none !important;
  font-weight: 700;
  letter-spacing: 0;
}

.resources-page .card-image {
  background: #fff;
}

.resources-page .card-image img,
.resources-page .card-image iframe {
  display: block;
}

@media only screen and (max-width: 600px) {
  .resources-header {
    margin: 35px 0 30px;
  }

  .resources-header h1 {
    font-size: 38px;
  }

  .resources-header p {
    font-size: 16px;
  }

  .resources-page .section > h4 {
    font-size: 1.65rem;
  }
}
</style>

<div class="resources-header">
  <div class="eyebrow">Adam on FIRE</div>
  <h1>{{ page.title | escape }}</h1>
  <p>Hasznos linkek, kalkulátorok, prezentációk és videók, amelyek segíthetnek a saját FIRE-utadat megtervezni és a pénzügyeidet tudatosabban kezelni.</p>
</div>

<div class="container resources-page">


  <!-- TBSZ ÉS PORTFÓLIÓ -->
  <div class="section">
    <h4 style="margin-bottom: 25px;">TBSZ és portfóliómenedzsment</h4>

    <div class="row">

      <div class="col s12 m6">
        <a href="tbsz" style="color: inherit;">
          <div class="card hoverable" style="height: 100%;">
            <div class="card-content">
              <span class="card-title">
                <strong>Tartós Befektetési Számla</strong>
              </span>
              <p>
                Adóoptimalizálás Magyarországon – információ a Tartós
                Befektetési Számláról (TBSZ).
              </p>
            </div>
            <div class="card-action">
              Tovább →
            </div>
          </div>
        </a>
      </div>


      <div class="col s12 m6">
        <a href="https://docs.google.com/spreadsheets/d/1bqick4Vy13FZMrMZ44g9YiPqF8-Wobd7CH5pAhfl2Bc/copy"
           target="_blank"
           style="color: inherit;">
          <div class="card hoverable" style="height: 100%;">
            <div class="card-content">
              <span class="card-title">
                <strong>Portfólió teljesítményének követése</strong>
              </span>
              <p>
                Egyszerű, félautomatikusan kezelhető Google Sheets
                táblázat a befektetési portfóliód követésére.
              </p>
            </div>
            <div class="card-action">
              Táblázat megnyitása →
            </div>
          </div>
        </a>
      </div>

    </div>
  </div>


  <!-- KALKULÁTOROK -->
  <div class="section">
    <h4 style="margin-bottom: 25px;">Kalkulátorok</h4>

    <div class="row">

      <div class="col s12 m6">
        <a href="net-worth" style="color: inherit;">
          <div class="card hoverable">
            <div class="card-content">
              <span class="card-title">
                <strong>Nettó vagyon kalkulátor</strong>
              </span>
              <p>
                Milyen gazdag voltál 2025-ben Magyarországon?
                Hasonlítsd össze a nettó vagyonodat.
              </p>
            </div>
            <div class="card-action">
              Kalkulátor megnyitása →
            </div>
          </div>
        </a>
      </div>


      <div class="col s12 m6">
        <a href="spending" style="color: inherit;">
          <div class="card hoverable">
            <div class="card-content">
              <span class="card-title">
                <strong>Egyéni fogyasztás kalkulátor</strong>
              </span>
              <p>
                Nézd meg, hogyan költesz egy átlagos magyar
                háztartáshoz képest.
              </p>
            </div>
            <div class="card-action">
              Kalkulátor megnyitása →
            </div>
          </div>
        </a>
      </div>


      <div class="col s12 m6">
        <a href="pension" style="color: inherit;">
          <div class="card hoverable">
            <div class="card-content">
              <span class="card-title">
                <strong>Állami nyugdíjkalkulátor</strong>
              </span>
              <p>
                Becsüld meg, mennyi lesz az állami nyugdíjad
                a jelenlegi szabályozás szerint.
              </p>
            </div>
            <div class="card-action">
              Kalkulátor megnyitása →
            </div>
          </div>
        </a>
      </div>


      <div class="col s12 m6">
        <a href="inflation" style="color: inherit;">
          <div class="card hoverable">
            <div class="card-content">
              <span class="card-title">
                <strong>Személyes infláció kalkulátor</strong>
              </span>
              <p>
                Számold ki a saját inflációdat a fogyasztói
                kosarad összetétele alapján.
              </p>
            </div>
            <div class="card-action">
              Kalkulátor megnyitása →
            </div>
          </div>
        </a>
      </div>

    </div>
  </div>


  <!-- PREZENTÁCIÓK ÉS VIDEÓK -->
  <div class="section">
    <h4 style="margin-bottom: 25px;">Prezentációk és videók</h4>

    <div class="row">

      <!-- Presentation -->
      <div class="col s12 m6">
        <div class="card hoverable">

          <div class="card-image">
            <a href="https://www.slideshare.net/slideshow/hogyan-epits-vagyont-tapasztalatok-egy-15-eves-fire-ut-vegen/276076087"
               target="_blank">
              <img src="images/presentation-1.png"
                   alt="Hogyan építs vagyont?">
            </a>
          </div>

          <div class="card-content">
            <span class="card-title">
              <strong>Hogyan építs vagyont?</strong>
            </span>

            <p>
              Tapasztalatok egy 15 éves FIRE út végén.
              Prezentáció – 2025. február
            </p>
          </div>

          <div class="card-action">
            <a href="https://www.slideshare.net/slideshow/hogyan-epits-vagyont-tapasztalatok-egy-15-eves-fire-ut-vegen/276076087"
               target="_blank">
              Prezentáció megnyitása →
            </a>
          </div>

        </div>
      </div>

 <div class="col s12 m6">
        <div class="card hoverable">

          <div class="card-image">
            <a href="https://www.slideshare.net/slideshow/hogyan-gondolkozz-hosszu-tavban-makrogazdasagi-szempontok-az-elmult-70-evben/287004907"
               target="_blank">
              <img src="images/presentation-2.png"
                   alt="Hogyan gondolkozz hosszú távban?">
            </a>
          </div>

          <div class="card-content">
            <span class="card-title">
              <strong>Hogyan gondolkozz hosszú távban?</strong>
            </span>

            <p>
              Makrogazdasági szempontok az elmúlt 70 év tőzsdei eseményei alapján
              Prezentáció – 2026. március
            </p>
          </div>

          <div class="card-action">
            <a href="https://www.slideshare.net/slideshow/hogyan-gondolkozz-hosszu-tavban-makrogazdasagi-szempontok-az-elmult-70-evben/287004907"
               target="_blank">
              Prezentáció megnyitása →
            </a>
          </div>

        </div>
      </div>


      <!-- YouTube video 1 -->
      <div class="col s12 m6">
        <div class="card hoverable">

          <div class="card-image">
            <div style="
              position: relative;
              padding-bottom: 56.25%;
              height: 0;
              overflow: hidden;
            ">
              <iframe
                src="https://www.youtube.com/embed/i6TT_x7nPZ4"
                title="10 tévhit a FIRE mozgalommal kapcsolatban"
                style="
                  position: absolute;
                  top: 0;
                  left: 0;
                  width: 100%;
                  height: 100%;
                  border: 0;
                "
                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
                allowfullscreen>
              </iframe>
            </div>
          </div>

          <div class="card-content">
            <span class="card-title">
              <strong>10 tévhit a FIRE mozgalommal kapcsolatban</strong>
            </span>

            <p>
              A FIRE mozgalommal kapcsolatos leggyakoribb
              félreértések és tévhitek – 2025. szeptember.
            </p>
          </div>

        </div>
      </div>


      <!-- YouTube video 2 -->
      <div class="col s12 m6">
        <div class="card hoverable">

          <div class="card-image">
            <div style="
              position: relative;
              padding-bottom: 56.25%;
              height: 0;
              overflow: hidden;
            ">
              <iframe
                src="https://www.youtube.com/embed/M3R2zgmog5U"
                title="Mi történt 2025-ben, mi várható 2026-ban?"
                style="
                  position: absolute;
                  top: 0;
                  left: 0;
                  width: 100%;
                  height: 100%;
                  border: 0;
                "
                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
                allowfullscreen>
              </iframe>
            </div>
          </div>

          <div class="card-content">
            <span class="card-title">
              <strong>Mi történt 2025-ben, mi várható 2026-ban?</strong>
            </span>

            <p>
              Évértékelés és kitekintés a következő évre –
              2026. január.
            </p>
          </div>

        </div>
      </div>

    </div>
  </div>

</div>


