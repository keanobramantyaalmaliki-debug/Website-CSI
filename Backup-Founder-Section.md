# Backup — Founder Section

> Disimpan 2026-06-29 sebelum Founder section dihapus (permintaan atasan).
> File ini berisi **semua** potongan yang terkait Founder agar mudah dipasang ulang.
> Urutan re-integrasi: CSS → HTML → JS. Semua tinggal copy-paste balik ke `index.html`.

Komponen yang terlibat (semua founder-specific, aman untuk dihapus bersama):
1. CSS blok Founder + Achievement overlay + mobile override
2. HTML: `#custom-cursor` + `#floating-wrapper`, `#ach-overlay`, `<section id="founder">`
3. JS: IIFE Founder hover + IIFE Achievement overlay

Posisi lama saat di-backup: **setelah `#careers`, sebelum `#cta`** (Hero → Manifesto → Deployments → Living Architecture → Careers → **Founder** → CTA → Footer).

---

## 1. CSS

### 1a. Blok Founder (taruh di `<style>`, setelah blok Manifesto)

```css
/* ── Founder ── */
#founder { position: relative; background: #0A0A0A; padding: 120px var(--pad); z-index: 1; }
.founder-label { font-size: 9px; letter-spacing: 0.18em; text-transform: uppercase; color: #3A3A3A; margin-bottom: 72px; }
.achievement-list { width: 100%; }
.achievement-item { display: grid; grid-template-columns: 220px 1fr; gap: 48px; padding: 88px 0; border-top: 1px solid #262626; cursor: none; transition: opacity 0.25s ease; }
.achievement-item:last-child { border-bottom: 1px solid #262626; }
.achievement-list.has-hover .achievement-item:not(.is-hovered) { opacity: 0.2; }
.founder-card { display: flex; align-items: flex-start; gap: 12px; padding: 10px 14px; border: 1px solid #1F1F1F; background: #111; align-self: flex-start; }
.thumb { width: 40px; height: 40px; flex-shrink: 0; background: #222; border: 1px solid #2A2A2A; overflow: hidden; }
.thumb img { width: 100%; height: 100%; object-fit: cover; object-position: center 22%; display: block; }
.card-info { display: flex; flex-direction: column; gap: 3px; padding-top: 2px; }
.card-name { font-size: 12px; font-weight: 500; color: #D0D0D0; letter-spacing: 0.01em; }
.card-title { font-size: 9px; color: #444; letter-spacing: 0.1em; text-transform: uppercase; }
.item-content { display: flex; flex-direction: column; justify-content: space-between; gap: 48px; }
.item-desc { font-size: clamp(22px, 2.8vw, 36px); font-weight: 400; color: #D0D0D0; line-height: 1.3; letter-spacing: -0.03em; cursor: none; overflow: hidden; }
.item-meta { display: flex; align-items: center; font-size: 9px; letter-spacing: 0.12em; text-transform: uppercase; color: #3A3A3A; }
.item-meta span { margin-right: 24px; }
.item-meta .mdot { width: 3px; height: 3px; background: #2A2A2A; border-radius: 50%; display: inline-block; margin-right: 24px; vertical-align: middle; flex-shrink: 0; }
.item-meta .arrow { margin-left: auto; font-size: 13px; color: #2A2A2A; transition: color 0.2s, transform 0.2s; }
.achievement-item:hover .item-meta { color: #555; }
.achievement-item:hover .item-meta .arrow { color: #888; transform: translate(3px, -3px); }
#custom-cursor { position: fixed; width: 8px; height: 8px; background: #F0F0F0; border-radius: 50%; pointer-events: none; z-index: 9999; transform: translate(-50%, -50%); transition: width 0.25s ease, height 0.25s ease, background 0.25s ease; opacity: 0; }
#custom-cursor.is-hovering { width: 32px; height: 32px; background: transparent; border: 1px solid rgba(240,240,240,0.6); }
#custom-cursor.is-hovering::before, #custom-cursor.is-hovering::after { content: ''; position: absolute; background: #F0F0F0; top: 50%; left: 50%; transform: translate(-50%, -50%); }
#custom-cursor.is-hovering::before { width: 10px; height: 1px; }
#custom-cursor.is-hovering::after  { width: 1px; height: 10px; }
#floating-wrapper { position: fixed; top: 0; left: 0; pointer-events: none; z-index: 100; transform: translate(-50%, -62%) rotate(0deg); will-change: transform; }
#floating-img { width: 240px; height: 320px; transform: scale(0.05); opacity: 0; transition: opacity 1.1s cubic-bezier(0.34, 1.56, 0.64, 1), transform 1.1s cubic-bezier(0.34, 1.56, 0.64, 1); }
#floating-img.visible { opacity: 1; transform: scale(1); }
#floating-img.hiding { opacity: 0; transform: scale(0.05); transition: opacity 0.2s ease, transform 0.2s ease; }
#floating-img img { width: 100%; height: 100%; object-fit: cover; display: block; background: #161616; }

/* ── Achievement detail overlay (terminal style) ── */
#ach-overlay { position: fixed; inset: 0; z-index: 250; background: rgba(8,8,8,0.86); backdrop-filter: blur(7px); -webkit-backdrop-filter: blur(7px); display: flex; flex-direction: column; padding: 0 var(--pad); opacity: 0; pointer-events: none; font-family: ui-monospace, 'SF Mono', 'Menlo', 'Consolas', monospace; }
#ach-overlay.is-open { pointer-events: auto; }
.ach-top { height: 64px; display: flex; align-items: center; justify-content: space-between; flex-shrink: 0; }
.ach-top .nav-brand img { height: 30px; width: auto; mix-blend-mode: screen; }
.ach-close { background: none; border: none; font-family: inherit; font-size: 12.5px; letter-spacing: 0.11em; text-transform: uppercase; color: #777; cursor: pointer; padding: 0; display: flex; align-items: center; gap: 10px; transition: color 0.25s; }
.ach-close::before { content: ''; display: block; width: 20px; height: 1px; background: currentColor; transition: width 0.3s ease; }
.ach-close:hover { color: #E0E0E0; }
.ach-close:hover::before { width: 32px; }
.ach-body { flex: 1; display: flex; align-items: center; justify-content: center; overflow-y: auto; }
.ach-inner { width: 100%; max-width: 680px; padding: 48px 0 80px; color: #B8B8B8; }
.ach-label { font-size: 12px; letter-spacing: 0.05em; color: #555; margin-bottom: 22px; }
.ach-title { font-size: clamp(22px, 3vw, 34px); line-height: 1.3; letter-spacing: -0.01em; color: #F0F0F0; font-weight: 400; margin-bottom: 30px; }
.ach-summary { font-size: 14px; line-height: 1.85; color: #9A9A9A; white-space: pre-line; margin-bottom: 48px; }
.ach-section-label { font-size: 12px; letter-spacing: 0.05em; color: #555; margin-bottom: 16px; }
.ach-meta { font-size: 12.5px; letter-spacing: 0.12em; text-transform: uppercase; color: #888; margin-bottom: 48px; display: flex; flex-wrap: wrap; align-items: center; gap: 14px; }
.ach-meta .mdot { width: 3px; height: 3px; border-radius: 50%; background: #444; }
.ach-links { display: flex; flex-wrap: wrap; gap: 24px; }
.ach-links a { font-size: 13px; letter-spacing: 0.04em; color: #C8C8C8; text-decoration: none; transition: color 0.2s ease; }
.ach-links a:hover { color: #FFFFFF; }
.ach-links a .lk-arr { display: inline-block; margin-left: 4px; transition: transform 0.2s ease; }
.ach-links a:hover .lk-arr { transform: translate(2px, -2px); }
/* IGLOO-style spatial scramble: chars near the cursor decode-scramble + brighten, trailing chars fade back */
.ach-zip .zw { white-space: nowrap; }
.ach-zip .zc { transition: none; }
@media (max-width: 768px) {
  .ach-inner { padding: 24px 0 64px; }
  .ach-title { font-size: clamp(20px, 6vw, 28px); }
}
```

### 1b. Touch hide rule (gabungan — saat re-add, kembalikan `#custom-cursor` & `#floating-wrapper`)

Aturan asli menggabung tiga selektor:
```css
html.is-touch #trail,
html.is-touch #custom-cursor,
html.is-touch #floating-wrapper { display: none !important; }
```
> Saat dihapus: sisakan `html.is-touch #trail { display: none !important; }` saja.

### 1c. Mobile override (di dalam `@media (max-width: 768px)`)

```css
  /* founder → single column, photo card stays static & visible */
  .achievement-item { grid-template-columns: 1fr; gap: 16px; padding: 32px 0; }
  .item-content { gap: 20px; }
  .item-desc { font-size: clamp(20px, 5.5vw, 30px); }
  .thumb { width: 56px; height: 56px; }
```

Juga di `@media (max-width: 768px)` ada `.role-photo-mobile` — itu **Careers**, jangan dihapus.

---

## 2. HTML

### 2a. `#custom-cursor` + `#floating-wrapper` (lama: tepat sebelum `<main>`)

```html
<div id="custom-cursor"></div>
<div id="floating-wrapper">
  <div id="floating-img">
    <img id="floating-photo" src="" alt="">
  </div>
</div>
```

### 2b. `#ach-overlay` (lama: di area overlay atas, setelah `#menu-overlay`)

```html
<!-- Achievement detail overlay -->
<div id="ach-overlay" aria-hidden="true">
  <div class="ach-top">
    <a class="nav-brand" href="#"><img src="Logo/Logo-Final.png" alt="cogniti"></a>
    <button class="ach-close" id="achClose">Close</button>
  </div>
  <div class="ach-body">
    <div class="ach-inner">
      <div class="ach-label">/////// Summary</div>
      <h2 class="ach-title" id="achTitle"></h2>
      <p class="ach-summary" id="achSummary"></p>
      <div class="ach-section-label">/// Details</div>
      <div class="ach-meta" id="achMeta"></div>
      <div class="ach-section-label">/// Discover</div>
      <div class="ach-links" id="achLinks"></div>
    </div>
  </div>
</div>
```

### 2c. `<section id="founder">` (lama: setelah `</section>` Careers, sebelum `<!-- CTA -->`)

```html
  <!-- Founder -->
  <section id="founder">
<div class="achievement-list" id="achievementList">
      <div class="achievement-item" data-photo="Photo-Founder-section/Foto Award.jpeg">
        <div class="founder-card">
          <div class="thumb"><img src="Photo-Founder-section/Photo profile.jpg" alt="Fami Maliki" loading="lazy"></div>
          <div class="card-info"><span class="card-name">Fami Maliki</span><span class="card-title">Founder &amp; CEO</span></div>
        </div>
        <div class="item-content">
          <p class="item-desc">Penghargaan atas inovasi digital terbaik dalam kategori teknologi bisnis.</p>
          <div class="item-meta"><span>Award</span><span class="mdot"></span><span>Digital Innovation</span><span class="mdot"></span><span>2023</span><span class="arrow">↗</span></div>
        </div>
      </div>
      <div class="achievement-item" data-photo="Photo-Founder-section/Foto Speaking.jpg">
        <div class="founder-card">
          <div class="thumb"><img src="Photo-Founder-section/Photo profile.jpg" alt="Fami Maliki" loading="lazy"></div>
          <div class="card-info"><span class="card-name">Fami Maliki</span><span class="card-title">Founder &amp; CEO</span></div>
        </div>
        <div class="item-content">
          <p class="item-desc">Keynote speaker pada konferensi teknologi dan inovasi bisnis terkemuka.</p>
          <div class="item-meta"><span>Speaking</span><span class="mdot"></span><span>Technology</span><span class="mdot"></span><span>2024</span><span class="arrow">↗</span></div>
        </div>
      </div>
    </div>
  </section>
```

---

## 3. JS (di dalam `<script>` utama)

### 3a. IIFE Founder hover (floating photo + custom cursor + text scramble)

```javascript
/* ── Founder ── */
(function(){
  if(window.IS_TOUCH)return;             // floating photo + scramble + cursor = mouse-only; foto card statis tetap tampil
  const cursor=document.getElementById('custom-cursor');
  const fw=document.getElementById('floating-wrapper');
  const fi=document.getElementById('floating-img');
  const fp=document.getElementById('floating-photo');
  const list=document.getElementById('achievementList');
  let mouseX=0,mouseY=0,prevMouseX=0,imgX=0,imgY=0,rotation=0,targetRotation=0;
  document.addEventListener('mousemove',e=>{mouseX=e.clientX;mouseY=e.clientY;cursor.style.left=mouseX+'px';cursor.style.top=mouseY+'px';});
  function lerp(a,b,t){return a+(b-a)*t;}
  (function loop(){
    const vx=mouseX-prevMouseX; prevMouseX=mouseX;
    targetRotation=-vx*0.4; rotation=lerp(rotation,targetRotation,0.08);
    imgX=lerp(imgX,mouseX,0.09); imgY=lerp(imgY,mouseY,0.09);
    fw.style.left=imgX+'px'; fw.style.top=imgY+'px';
    fw.style.transform=`translate(20px,-50%) rotate(${rotation}deg)`;
    requestAnimationFrame(loop);
  })();
  class TextScramble{
    constructor(el){this.el=el;this.original=el.innerText;this.chars='ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';this.raf=null;}
    scramble(){
      this.el.style.width=this.el.offsetWidth+'px';this.el.style.height=this.el.offsetHeight+'px';
      const text=this.original,duration=420,start=performance.now();cancelAnimationFrame(this.raf);
      const update=now=>{const progress=Math.min((now-start)/duration,1);let output='';for(let i=0;i<text.length;i++){if(text[i]===' '){output+=' ';continue;}output+=progress>i/text.length?text[i]:this.chars[Math.floor(Math.random()*this.chars.length)];}this.el.innerText=output;if(progress<1)this.raf=requestAnimationFrame(update);else this.el.innerText=text;};
      this.raf=requestAnimationFrame(update);
    }
    reset(){cancelAnimationFrame(this.raf);this.el.innerText=this.original;this.el.style.width='';this.el.style.height='';}
  }
  document.querySelectorAll('.achievement-item').forEach(item=>{
    item.addEventListener('mouseenter',()=>{ cursor.style.opacity='1'; });
    item.addEventListener('mouseleave',()=>{ cursor.style.opacity='0'; });
  });
  document.querySelectorAll('.item-desc').forEach(desc=>{
    const item=desc.closest('.achievement-item'),scrambler=new TextScramble(desc);
    desc.addEventListener('mouseenter',()=>{scrambler.scramble();cursor.classList.add('is-hovering');const src=item.getAttribute('data-photo');if(src&&fp.getAttribute('src')!==src)fp.setAttribute('src',src);fi.classList.remove('hiding');fi.classList.add('visible');list.classList.add('has-hover');item.classList.add('is-hovered');});
    desc.addEventListener('mouseleave',()=>{scrambler.reset();cursor.classList.remove('is-hovering');fi.classList.remove('visible');fi.classList.add('hiding');list.classList.remove('has-hover');item.classList.remove('is-hovered');});
  });
})();
```

### 3b. IIFE Achievement detail overlay (terminal + IGLOO spatial scramble)

```javascript
/* ── Achievement detail overlay ── (mouse + touch; registered outside the hover IIFE) */
(function(){
  /* Placeholder data — ganti `summary` & `links` saat copy final dari founder siap.
     Urutan array harus sama dengan urutan .achievement-item di markup. */
  const LOREM='Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.\n\nDuis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.';
  const ACH=[
    { title:'Penghargaan atas inovasi digital terbaik dalam kategori teknologi bisnis.',
      summary:LOREM,
      meta:['Award','Digital Innovation','2023'],
      links:[{label:'[X]',url:'#'},{label:'[LinkedIn]',url:'#'},{label:'[website]',url:'#'}] },
    { title:'Keynote speaker pada konferensi teknologi dan inovasi bisnis terkemuka.',
      summary:LOREM,
      meta:['Speaking','Technology','2024'],
      links:[{label:'[X]',url:'#'},{label:'[LinkedIn]',url:'#'},{label:'[website]',url:'#'}] },
  ];
  const overlay=document.getElementById('ach-overlay');
  const closeBtn=document.getElementById('achClose');
  const elTitle=document.getElementById('achTitle');
  const elSummary=document.getElementById('achSummary');
  const elMeta=document.getElementById('achMeta');
  const elLinks=document.getElementById('achLinks');
  const body=overlay.querySelector('.ach-body');
  const items=[...document.querySelectorAll('.achievement-item')];
  let isOpen=false;

  /* ── IGLOO-style spatial scramble: chars near cursor decode + brighten, trail settles back ── */
  const RADIUS=64;         // cursor disturbance radius (px) — chars inside get ignited
  const DECAY=0.98;        // per-frame disturbance falloff → length of the settle trail jejak
  const THRESH=0.012;      // below this a char settles back to its original glyph (kept low so glow fades out fully first)
  const SCRAMBLE='ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789#%&*[]<>^';
  const esc=s=>s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');
  const escAttr=s=>esc(s).replace(/"/g,'&quot;');
  /* split text into word-wrapped char spans; original glyph stored in data-ch so the
     scramble engine can restore it even after textContent is swapped for a random char.
     \n\n→paragraph break, \n→<br> */
  function zipHTML(text){
    return text.split('\n').map(line=>
      line.length===0 ? '' :
      line.split(' ').map(word=>
        '<span class="zw">'+[...word].map(ch=>`<span class="zc" data-ch="${escAttr(ch)}">${esc(ch)}</span>`).join('')+'</span>'
      ).join(' ')
    ).join('<br>');
  }
  function render(d){
    elTitle.innerHTML=zipHTML(d.title);
    elSummary.innerHTML=zipHTML(d.summary);
    elMeta.innerHTML=d.meta.map(m=>`<span>${zipHTML(m)}</span>`).join('<span class="mdot"></span>');
    elLinks.innerHTML=d.links.map(l=>`<a href="${l.url}"${l.url!=='#'?' target="_blank" rel="noopener noreferrer"':''}>${l.label}<span class="lk-arr">↗</span></a>`).join('');
    [elTitle,elSummary,elMeta].forEach(el=>el.classList.add('ach-zip'));
  }

  const R2=RADIUS*RADIUS;
  const rndCh=()=>SCRAMBLE[(Math.random()*SCRAMBLE.length)|0];
  let chars=[],mx=-1e4,my=-1e4,pmx=-1e4,pmy=-1e4,zipRaf=null;
  function reset(c){ c.dist=0; c.dirty=false; if(c.el.textContent!==c.ch)c.el.textContent=c.ch; c.el.style.color=''; c.el.style.textShadow='none'; }
  /* parse 'rgb(r, g, b)' → [r,g,b]; the resting color is the char's own CSS color so
     the glow can interpolate from it (no brightness jump when a char settles) */
  function parseRGB(s){ const m=s.match(/\d+/g); return m?[+m[0],+m[1],+m[2]]:[154,154,154]; }
  function cacheChars(){
    chars=[...overlay.querySelectorAll('.ach-zip .zc')].map(el=>{
      const r=el.getBoundingClientRect();
      el.style.color='';
      const base=parseRGB(getComputedStyle(el).color);
      return {el,ch:el.getAttribute('data-ch'),cx:r.left+r.width/2,cy:r.top+r.height/2,dist:0,dirty:false,base};
    });
    chars.forEach(reset);
  }
  function loop(){
    zipRaf=requestAnimationFrame(loop);
    const moving=(mx-pmx)*(mx-pmx)+(my-pmy)*(my-pmy)>0.2; pmx=mx; pmy=my;   // only cursor motion drives scramble
    for(const c of chars){
      const dx=c.cx-mx, dy=c.cy-my, d2=dx*dx+dy*dy;
      const active=moving&&d2<R2;                      // THIS char is under the moving cursor right now
      if(active){ const hit=1-Math.sqrt(d2)/RADIUS; if(hit>c.dist)c.dist=hit; }   // charge to brightest
      if(c.dist>THRESH){
        const t=c.dist, k=Math.min(1,t*1.6);          // ramp: saturates to white fast, but eases to 0 smoothly
        c.el.textContent=active?rndCh():c.ch;         // scramble ONLY under the moving cursor; trail shows real glyph…
        const b=c.base;                               // interpolate from the char's own resting color → white
        const r2=Math.round(b[0]+(255-b[0])*k), g2=Math.round(b[1]+(255-b[1])*k), bl=Math.round(b[2]+(255-b[2])*k);
        c.el.style.color='rgb('+r2+','+g2+','+bl+')';
        c.el.style.textShadow=`0 0 ${(6*k).toFixed(1)}px rgba(255,255,255,${(0.9*k).toFixed(2)}), 0 0 ${(16*k).toFixed(1)}px rgba(255,255,255,${(0.55*k).toFixed(2)})`;
        c.dist*=DECAY;                                // …but the glow trail keeps fading every frame regardless
        c.dirty=true;
      } else if(c.dirty){ reset(c); }                 // settled: restore original glyph + clear glow once
    }
  }
  function onMove(e){ mx=e.clientX; my=e.clientY; }
  function open(i,push){
    const d=ACH[i]; if(!d||isOpen)return;
    isOpen=true; render(d);
    overlay.classList.add('is-open'); overlay.setAttribute('aria-hidden','false');
    const tl=gsap.timeline();
    gsap.set(['.ach-label','.ach-title','.ach-summary','.ach-section-label','.ach-meta','.ach-links'],{y:24,opacity:0});
    tl.to(overlay,{opacity:1,duration:0.3,ease:'power2.out'});
    tl.to(['.ach-label','.ach-title','.ach-summary','.ach-section-label','.ach-meta','.ach-links'],{y:0,opacity:1,stagger:0.06,duration:0.55,ease:'power3.out'},'-=0.1');
    tl.add(()=>{ cacheChars(); mx=my=pmx=pmy=-1e4; vx=vy=0; window.addEventListener('mousemove',onMove); if(!zipRaf)zipRaf=requestAnimationFrame(loop); });
    if(push!==false&&window.history){history.pushState({achOpen:true},'');}
  }
  function close(fromPop){
    if(!isOpen)return; isOpen=false;
    window.removeEventListener('mousemove',onMove);
    if(zipRaf){cancelAnimationFrame(zipRaf);zipRaf=null;}
    gsap.to(overlay,{opacity:0,duration:0.28,ease:'power2.in',onComplete:()=>{overlay.classList.remove('is-open');overlay.setAttribute('aria-hidden','true');}});
    if(!fromPop&&window.history&&history.state&&history.state.achOpen){history.back();}
  }
  body.addEventListener('scroll',()=>{ if(isOpen)cacheChars(); });
  window.addEventListener('resize',()=>{ if(isOpen)cacheChars(); });
  items.forEach((item,i)=>{
    item.style.cursor='pointer';
    item.addEventListener('click',e=>{ if(e.target.closest('a'))return; open(i); });
  });
  closeBtn.addEventListener('click',()=>close());
  overlay.addEventListener('click',e=>{ if(e.target===overlay)close(); });
  document.addEventListener('keydown',e=>{ if(e.key==='Escape'&&isOpen)close(); });
  window.addEventListener('popstate',()=>{ if(isOpen)close(true); });
})();
```

---

## Catatan re-integrasi

- **Foto**: folder `Photo-Founder-section/` (`Photo profile.jpg`, `Foto Award.jpeg`, `Foto Speaking.jpg`) — JANGAN dihapus dari repo kalau ada kemungkinan re-add. Kalau yakin tidak dipakai lama, boleh diarsipkan terpisah.
- **Konten** masih placeholder: deskripsi achievement nyata + summary overlay (lorem ipsum) + link `[X]/[LinkedIn]/[website]` (`#`) belum final dari founder.
- **Saat menghapus dari `index.html`**: tidak ada error JS walau IIFE ditinggal (querySelectorAll → array kosong), tapi untuk kebersihan hapus juga kedua IIFE + markup overlay + custom-cursor/floating-wrapper. Semua sudah ada di file ini.
- **Nav/Footer**: link "Founder" sudah tidak ada (dihapus saat finalize), jadi tidak ada link yang perlu dibersihkan.
```
