---
layout: post
title: Elkészült a portfóliókövetőm
date: 2025-05-03
permalink: blog-3
---


<style>
/* ==========================================
   ADAM ON FIRE - INDIVIDUAL BLOG POST STYLE
   Copy this block into any individual blog post.
   ========================================== */

.post-shell {
  margin: 42px auto 56px;
}

.post-hero {
  position: relative;
  overflow: hidden;
  padding: 44px 46px 38px;
  border-radius: 18px 18px 0 0;
  background: linear-gradient(135deg, #0d47a1 0%, #2962ff 100%);
  color: #fff;
  box-shadow: 0 14px 34px rgba(13, 71, 161, .16);
}

.post-hero::after {
  content: "FIRE";
  position: absolute;
  right: -12px;
  bottom: -54px;
  font-size: 150px;
  line-height: 1;
  font-weight: 900;
  letter-spacing: -10px;
  color: rgba(255,255,255,.06);
  pointer-events: none;
}

.post-kicker {
  margin-bottom: 10px;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: rgba(255,255,255,.78);
}

.post-title {
  position: relative;
  z-index: 1;
  max-width: 820px;
  margin: 0;
  font-size: 42px;
  line-height: 1.15;
  font-weight: 700;
  letter-spacing: -1px;
  color: #fff;
}

.post-date {
  position: relative;
  z-index: 1;
  display: inline-flex;
  align-items: center;
  gap: 8px;
  margin-top: 18px;
  padding: 6px 11px;
  border: 1px solid rgba(255,255,255,.28);
  border-radius: 999px;
  background: rgba(255,255,255,.10);
  color: rgba(255,255,255,.92);
  font-size: 12px;
  font-weight: 600;
  letter-spacing: .2px;
}

.post-body {
  padding: 44px 48px 50px;
  border-left: 1px solid #dce8ff;
  border-right: 1px solid #dce8ff;
  background: #eef4ff;
  color: #17345f;
  font-size: 17px;
  line-height: 1.82;
}

.post-body p {
  margin: 0 0 24px;
  color: #17345f;
}

.post-body p:last-child {
  margin-bottom: 0;
}

.post-body a {
  color: #0d47a1;
  font-weight: 600;
  text-decoration: underline;
  text-decoration-thickness: 1px;
  text-underline-offset: 3px;
}

.post-body strong {
  color: #0b2f67;
}

.post-body h2,
.post-body h3,
.post-body h4,
.post-body h5,
.post-body h6 {
  margin-top: 38px;
  margin-bottom: 16px;
  color: #0d47a1;
  font-weight: 700;
}

.post-body ul,
.post-body ol {
  margin: 10px 0 28px 24px;
  padding-left: 12px;
}

.post-body li {
  margin-bottom: 14px;
  padding-left: 4px;
}

.post-body blockquote {
  margin: 32px 0;
  padding: 22px 24px;
  border-left: 5px solid #2962ff;
  border-radius: 0 10px 10px 0;
  background: #dfeaff;
  color: #17345f;
  font-style: normal;
}

.post-back {
  border-radius: 0 0 18px 18px;
  background: #164fa8;
  box-shadow: 0 14px 34px rgba(13, 71, 161, .14);
}

.post-back a {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
  padding: 22px 30px;
  color: #fff !important;
  text-decoration: none;
  font-weight: 700;
  letter-spacing: .1px;
  transition: background .2s ease, padding-left .2s ease;
}

.post-back a:hover {
  background: rgba(255,255,255,.08);
  padding-left: 36px;
}

.post-back-arrow {
  font-size: 22px;
  line-height: 1;
  transition: transform .2s ease;
}

.post-back a:hover .post-back-arrow {
  transform: translateX(-5px);
}

@media only screen and (max-width: 600px) {
  .post-shell {
    margin: 26px auto 38px;
  }

  .post-hero {
    padding: 30px 24px 28px;
    border-radius: 14px 14px 0 0;
  }

  .post-hero::after {
    font-size: 95px;
    bottom: -34px;
  }

  .post-title {
    font-size: 31px;
    letter-spacing: -.5px;
  }

  .post-body {
    padding: 30px 24px 34px;
    font-size: 16px;
    line-height: 1.75;
  }

  .post-back {
    border-radius: 0 0 14px 14px;
  }

  .post-back a {
    padding: 20px 22px;
  }
}
</style>

<div class="post-shell">

  <header class="post-hero">
    <div class="post-kicker">Adam on FIRE · Blog</div>
    <h1 class="post-title">{{ page.title | escape }}</h1>
    <div class="post-date">{{ page.date | date: "%Y. %m. %d." }}</div>
  </header>

  <article class="post-body">

<p>Volt egy pozitív hozadéka az egész vámtarifa-ügynek, és ez a FIRE-re való felkészültségemhez kapcsolódik. Trump bejelentéséig és a piaci összeomlásig azt hittem, mindenem megvan ahhoz, hogy nyomon kövessem a portfóliómat. Volt egy fő táblázatom, Yahoo és Google Finance követés, stb.<p/>  
<p>Amire viszont eddig nem gondoltam, az egy valódi, félig automatizált módszer az összes számlám követésére. Nem is sejtettem, hogy lehetséges a legtöbb vagyonelemhez – vagy legalábbis a nagy amerikai és európai piacokon jegyzettekhez – valós idejű adatfrissítést beállítani. Így aztán némi Google Sheets-varázslatnak köszönhetően most van egy fő táblázatom, amely bármely pillanatban pontosan megmutatja a portfólióm értékét, és az eszközeim több mint 70%-a automatikusan frissül. Ez megkönnyíti a havi áttekintést is – amit Trump miatt a negyedévesről havi rendszerességűre változtattam –, mivel pontosan látom, hová megy a pénzem, mik a beérkező egyenlegeim, stb.</p>  

<p>A cél egy jó 60-30-10 portfólió kialakítása a végére. 60% részvényekbe kerül – valószínűleg továbbra is többségében USA-központú ETF-ekbe –, 30% kötvényekbe – szintén főként amerikai, de néhány magyar állampapír is megmarad, hogy legyen azért forintom is a költéseimre –, és végül körülbelül 10% aranyba és bitcoinba, amit a jövőben a kötvények rovására még növelhetek is (tekintve, hogy a Bitcoin most történelmi csúcson jár, és az arany lassan afféle tartalékvalutává válik).</p>  

<p>Végül itt van néhány diagram arról, hogyan alakult át kismértékben a portfólióm Trump "nagy, gyönyörű táblázatának" bejelentése után.</p>

<br/>
<div class="row">
  <div class="col-md-6">
    <iframe title="Portfólió összetétele az elmúlt 8 hónapban" 
            aria-label="Small multiple pie chart" 
            id="datawrapper-chart-3Foxj" 
            src="https://datawrapper.dwcdn.net/3Foxj/2/" 
            scrolling="no" 
            frameborder="0" 
            style="width: 100%; border: none;" 
            height="388" 
            data-external="1"></iframe>
  </div>
  
  <div class="col-md-6">
    <iframe title="Portfólió összetétele az elmúlt 8 hónapban" 
            aria-label="Small multiple pie chart" 
            id="datawrapper-chart-1M7s1" 
            src="https://datawrapper.dwcdn.net/1M7s1/1/" 
            scrolling="no" 
            frameborder="0" 
            style="width: 100%; border: none;" 
            height="388" 
            data-external="1"></iframe>
  </div>
</div>

<script type="text/javascript">
!function(){"use strict";
  window.addEventListener("message",function(a){
    if(void 0!==a.data["datawrapper-height"]){
      var e=document.querySelectorAll("iframe");
      for(var t in a.data["datawrapper-height"])
        for(var r,i=0;r=e[i];i++)
          if(r.contentWindow===a.source){
            var d=a.data["datawrapper-height"][t]+"px";
            r.style.height=d
          }
    }
  })
}();
</script>

  </article>

  <div class="post-back">
    <a href="/blog">
      <span><span class="post-back-arrow">←</span>&nbsp;&nbsp; Vissza az összes bejegyzéshez</span>
      <span>Blog</span>
    </a>
  </div>

</div>
