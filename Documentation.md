# Documentation — cogniti Landing Page MVP 1

---

## North Star

> Website ini harus menciptakan **rasa penasaran, otoritas, dan dorongan untuk menghubungi Cogniti.**

Setiap keputusan desain dan konten harus berkontribusi ke salah satu dari tiga tujuan ini.

---

## Brand

| | |
|---|---|
| **Brand facing** | cogniti (lowercase) |
| **Legal** | Cognitiva Solusi Indonesia |
| **Positioning** | Intelligence Infrastructure Company |
| **Typography** | Inter |
| **Logo (dark bg)** | `Logo/Logo-Final.png` (gray) — satu-satunya logo dipakai |

> `Logo-Final 2.png` (navy, light-bg) dihapus saat finalize — tidak pernah direferensikan (site full dark).

---

## Stack (MVP 1 — Single HTML)

- GSAP 3.12.5 + ScrollTrigger (CDN)
- Three.js r128 (CDN)

> Lenis dan Tailwind tidak dipakai di implementasi akhir.
> Next.js dipakai saat migrasi ke production (post MVP 1)

---

## Color Palette

Filosofi: **accent bukan warna, tapi kontras.** Monokromatik murni.

| Role | Hex |
|---|---|
| Background | `#0A0A0A` |
| Surface | `#141414` |
| Border | `#1A1A1A` |
| Text primary | `#F0F0F0` |
| Text secondary | `#888888` |
| Text muted | `#444444` |
| Accent (cold white) | `#FFFFFF` — sparingly |
| Logo mark | Merah — logo only, tidak masuk UI |

Feel referensi: Linear, Vercel.

---

## Global Design Decisions

- **Tidak ada section labels** — semua label uppercase kecil di atas section (e.g. "Living Architecture", "Selected Deployment Environments", "Careers", "Contact") dihapus. Konten berbicara sendiri.
- **Scroll restoration** — Chrome mengabaikan `history.scrollRestoration = 'manual'` dan tetap restore scroll secara internal saat refresh. Fix: tambah class `page-loading` ke `<html>` via head script, CSS `html.page-loading { overflow: hidden }` + `html.page-loading main { visibility: hidden }` menyembunyikan seluruh main content. Saat entry animation selesai, `scrollTo(0,0)` + `scrollTop=0` dipanggil sebelum dan sesudah `classList.remove('page-loading')` untuk memastikan posisi kembali ke 0 sebelum konten terlihat.

---

## Struktur Section

| # | Section | ID | Fungsi |
|---|---|---|---|
| 1 | **Hero** | `#hero` | Curiosity — WebGL sphere full-screen |
| 2 | **Manifesto** | `#manifesto` | Worldview building — word-by-word reveal |
| 3 | **Selected Deployments** | `#deployments` | Implied authority — arc-spine |
| 4 | **Our Services** | `#services` | 3D conveyor — daftar 9 layanan (drag + flip) |
| 5 | **Living Architecture** | `#living-arch` | Interactive 3D simulation — centerpiece |
| 6 | **Our Development Process** | `#process` | Sticky split — 6 langkah + motif canvas per tahap |
| 7 | **Careers** | `#careers` | Talent acquisition |
| 8 | **Industries We Serve** | `#industries` | Dual-row marquee — 13 sektor |
| 9 | **Vision & Mission** | `#vision` | Editorial split — vision sticky + mission list |
| 10 | **CTA / Contact** | `#cta` | Dorongan konversi |
| 11 | **Footer** | `#footer` | — |

> Minimal project, klien, dan produk — credibility dibangun lewat cara berpikir dan siapa di baliknya, bukan portfolio. Pendekatan McKinsey/Stripe.
> Loading Screen ditunda, bukan bagian dari MVP 1 awal.
> "Who We Serve" section dihapus — digantikan Living Architecture.
> **Founder section dihapus (2026-06-29)** atas permintaan atasan. Semua kode (CSS + HTML + JS hover & achievement overlay) di-backup ke `Backup-Founder-Section.md` untuk re-integrasi sewaktu-waktu. Slot lama (Careers → CTA) kini diisi **Industries We Serve** + **Vision & Mission** (lihat section baru di bawah).
> **Section baru ditambah (2026-06-30)** dari revisi PDF atasan: Our Services, Our Development Process, Industries We Serve, Vision & Mission. Positioning bergeser dari abstrak/misterius → company profile eksplisit. Detail per section di bawah.

---

## Section 1 — Hero ✅ Implemented

### Headline
```
We build the infrastructure that thinks.
```

### WebGL — "The Core"

IcosahedronGeometry (detail 5) dengan tiga layer:
- Wireframe mesh `opacity: 0.06` — struktur
- Points (vertex colors) — glow individual
- Wireframe glow (AdditiveBlending) — pulse ripple

**Entry Animation — "Collapse into Text":**
1. WebGL full-screen saat load — immersive
2. First scroll/click → canvas shrinks ke `orbSlot` inline dalam headline
3. Canvas fade out → hero text reveal → navbar swap (minimal → full)
4. Scroll animations aktif setelah entry selesai

**Scroll:** `#hero` fade out saat `#manifesto` masuk (ScrollTrigger scrub).

---

## Section 2 — Manifesto ✅ Implemented

**Copy (final — 4 block):**
1. Software connected information. Intelligence connects decisions.
2. Organizations are drowning in data. Yet struggling to act.
3. The future belongs not to those who collect, but to those who act.
4. Intelligence should exist across every interaction. Every workflow. Every decision.

**Interaksi:**
- Section pinned, total scroll `4 × 100vh`
- Word-by-word reveal via GSAP ScrollTrigger `scrub: 2`
- **Reveal:** `opacity 0→1`, `y: 14→0`, `rotation: +6°→0°` (power3.out)
- **Keluar:** `opacity 1→0`, `y: 0→14` tanpa rotate (power3.in)
- Progress bar 4 segmen di bottom center
- Ambient trail visible di background

---

## Founder ❌ Removed (2026-06-29)

Founder section dihapus dari `index.html` atas permintaan atasan (revisi PDF: "slide founder di akhir aja" → lalu diputuskan dihapus seluruhnya).

**Yang dihapus:** CSS blok Founder + achievement overlay + mobile override; HTML `<section id="founder">`, `#ach-overlay`, `#custom-cursor`, `#floating-wrapper`; 2 IIFE JS (founder hover floating-photo/scramble + achievement detail overlay IGLOO-style).

**Backup penuh:** `Backup-Founder-Section.md` — semua potongan kode + posisi lama + urutan re-integrasi. Foto di `Photo-Founder-section/` belum dihapus (masih dipakai sebagai OG/Twitter share image di `<head>`).

**Slot lama (Careers → CTA) — sudah diisi (2026-06-30):** "Industries We Serve" (13 sektor, dual-row marquee) + "Vision & Mission" (editorial split) ditambahkan. Tumpang tindih dengan Deployments dihindari: Deployments tetap pakai arc + nama klien implisit, Industries pakai marquee sektor murni. Lihat section masing-masing di bawah.

---

## Section 3 — Selected Deployments ✅ Implemented

**Konsep:** Implied authority — coverage sektor tanpa nama klien. Pola McKinsey/Deloitte.

**Visual:** Arc-spine — lingkaran besar (center di luar viewport kiri), 5 sector sebagai titik di kurva. Teks dirotasi mengikuti tangen kurva.

**Enrichment (✅):** Guide-arc (dua, di `DR-20` & `DR+26`) + tick-marks perpendikular (minor sepanjang span, major di slot sektor). Stroke redup monokrom (`arc-path` 0.085, `arc-guide` 0.05, tick 0.10 / major 0.20). Progress dots dihapus (tidak perlu). Label aktif: `01 — Public Services` dst, transisi fade.

**Arc bleed (✅):** Rentang visual dipisah dari spacing item. `DHALF` (`asin(DVH*0.46/DR)`) tetap untuk posisi sektor + tick, tapi arc-path + dua guide pakai `DVISHALF` (`asin(DVH*0.62/DR)`) sehingga garis lengkung menembus tepi atas-bawah viewport (~12% bleed tiap sisi) dan tidak terlihat terpotong di tengah layar.

**Interaksi:** GSAP ScrollTrigger scrub, section di-pin `5 × 100vh`.

**Sectors:** Public Services · Infrastructure · Logistics · Hospitality · Communities

**Arc bleed ✅:** Span visual arc (`DVISHALF`, DVH*0.62) dipisah dari span item/tick (`DHALF`, DVH*0.46) — garis arc + guide (inner/outer) memanjang lewat tepi atas/bawah viewport biar tidak keliatan terpotong, tapi titik sektor & tick tetap dalam area aman.

**Rules:** No client logo, no project name, no screenshots, no pricing.

---

## Section — Our Services ✅ Implemented (2026-06-30)

**Konsep:** Daftar 9 layanan eksplisit (revisi PDF hal. 2–3) — membalik keputusan desain lama "tidak ada daftar layanan". Disajikan sebagai **3D conveyor / rotating bookshelf** (terinspirasi Active Theory), bukan grid kartu statis.

**Kenapa CSS 3D, bukan Three.js:** teks real-font tetap tajam, tidak menambah WebGL context baru (hero sphere + living-arch graph sudah 2 context — menambah lagi memicu rAF-starvation), reuse stack GSAP yang ada. Motion (translateZ + rotateY) native ke CSS `transform-style: preserve-3d`.

**Mekanik (desktop):**
- `.svc-stage` = perspective container (1600px); `.svc-track` = preserve-3d; 9 `.svc-card` absolut.
- **Drag-driven, BUKAN scroll-pinned** — page mengalir normal (tidak ada scroll-jacking). Press & drag sideways menggerakkan conveyor; satu kartu menghadap kamera (readable) di center, tetangga mundur + rotateY edge-on.
- `pos` = float kontinu di [0, N-1]; inertia + snap ke kartu terdekat. **rAF loop hanya jalan saat bergerak**, idle saat settled → no rAF starvation.
- **No-redundancy:** front face = nomor + judul saja; tap kartu yang di center → flip 180° (`.is-flipped`) menampilkan deskripsi di back face. Tap kartu samping → slide ke center.
- Kartu #4 (AI Solutions) punya back face khusus = 5 sub-item (Jenna.ai · Knowledge Assistants · Process Automation · AI-Powered Analytics · Custom AI Integration).
- Back face deskripsi di-inject via JS untuk 8 kartu non-AI (AI sudah punya back face di HTML).
- **Active-card FX:** flow-field particle canvas (cursor-reactive) di belakang judul kartu center; hanya 1 instance jalan, IO-gated (`svcVisible`), berhenti saat drag/section off-screen → time-exclusive dengan loop WebGL lain.
- A11y: `.svc-stage` `tabindex=0`, ArrowLeft/Right navigasi kartu.

**Mobile (`IS_TOUCH` / ≤768px):** 3D conveyor **dipertahankan** (sama seperti desktop) atas permintaan user (2026-06-30) — drag-driven, jadi tidak ada scroll-jacking; finger-drag horizontal menggerakkan conveyor, vertical scroll halaman tetap jalan (`.svc-stage touch-action: pan-y`). Hanya `.svc-headline` diperkecil (`clamp(18px,5.5vw,26px)`) biar muat. Kartu 260px muat di 390px. `buildServicesMobile()` / `.svc-list-mobile` masih ada sebagai fallback (di-build tapi `display:none`) — tidak dipakai selama conveyor aktif. (Verifikasi Puppeteer iPhone 390×844 `/tmp/csi-shots/svc-mobile.js`: stage `display:flex`, touch-drag menggeser active card 0→1, page scrollY tetap berubah = tidak ter-trap.)

> **Reversal:** keputusan lama "drop conveyor di mobile" dibalik — user menilai list bertumpuk terlalu makan tempat; conveyor lebih ringkas (1 layar) dan tetap interaktif via drag. Untuk revert ke list: kembalikan gate JS `if(window.IS_TOUCH||window.innerWidth<=768){buildServicesMobile();return;}` + CSS override `.svc-stage{display:none}` / `.svc-pin{position:static}` / `.svc-list-mobile{display:flex}`.

**9 layanan:** Custom Software Development · Web Application Development · Mobile App Development · Artificial Intelligence Solutions · Enterprise Solutions · System Integration · UI/UX Design · Cloud & DevOps · Maintenance & Technical Support.

---

## Section 4 — Living Architecture ✅ Implemented

**Konsep:** Interactive 3D network simulation — centerpiece website. Menjelaskan kemampuan Cogniti tanpa membuka IP produk.

**Layout:** Grid 2 kolom — kiri (copy panel) | kanan (Three.js canvas)

**Copy:**
- Headline: "A Living Architecture For Decisions."
- Sub: "We connect signals, context, knowledge, and workflows into adaptive systems that help organizations move from awareness to action."

### Nodes (7)

| Node | Microcopy |
|---|---|
| Citizen | Every interaction becomes a signal. |
| Operations | Workflows gain visibility. |
| Knowledge | Information becomes structured context. |
| Infrastructure | Assets become part of the intelligence layer. |
| Intelligence | Patterns become recommendations. |
| Decision | Leaders act with better context. |
| Action | Decisions move into execution. |

### Interaksi

**Hover:**
- Node → state `h` (brighter), connected edges brightened
- Cursor `grab`
- Hint text update: "Drag to reposition — Click to activate"

**Drag (reposition):**
- `mousedown` pada node → drag di 3D plane tegak lurus kamera
- Mouse velocity ditrack via EMA (Exponential Moving Average) selama drag
- `mouseup` → velocity ditransfer ke node sebagai **throw physics**:
  - Drag cepat = terlempar jauh, drag pelan = terlempar pelan
  - Diam > 100ms sebelum lepas = tidak terlempar
  - Friction: `vel *= 0.88` per frame
- **Invisible walls:** Y bounds ±1.8, cylindrical XZ radius 3.0 — node memantul (restitution 0.5)
- Orbit kamera berhenti saat drag untuk stabilitas
- Edge geometry update realtime mengikuti posisi node baru

**Click (trigger signal):**
- Click tanpa drag (threshold < 5px) → BFS propagation dari node tersebut
- Tier delay: 950ms per tier
- Partikel travel dari node ke node via edge
- Pulse rings spawn di setiap node yang aktif
- Completion ("From awareness to action") hanya muncul jika semua 7 node aktif (eksklusif dari Citizen)

**Floating animation:**
- Setiap node: oscillasi X/Y/Z dengan fase berbeda (sin dengan frekuensi 0.73, 1.0, 0.55)
- Period ~17–30 detik, amplitude ±0.025–0.042 units
- Floating berbasis `basePos` — drag mengupdate `basePos`, floating berlanjut dari sana

**Camera:**
- Orbit lambat (ORBIT_S = 0.0006) sekitar Y axis
- Mouse parallax (laTX/laTY)
- Orbit berhenti saat node di-drag

**Auto-demo:** `triggerSignal(0)` setelah 4500ms jika user belum berinteraksi

**Panel states:**
- Default: headline + hint
- Active: node number + scramble name + micro text + progress dots
- Complete: "Signal Complete" + "From awareness to action"

**Mobile (`IS_TOUCH` / ≤768px):** graph 3D di-skip total (`.la-right display:none` + early `return` di IIFE), diganti static list 6 alasan (`#laListMobile`) — context WebGL kedua + rAF loop tidak jalan. Lihat "Mobile Responsive — Drop Heavy Effects".

---

## Section — Our Development Process ✅ Implemented (2026-06-30)

**Konsep:** 6 langkah proses kerja (revisi PDF hal. 6). Layout = **sticky cinematic split**.

**Mekanik:**
- `.proc-grid` = 2 kolom (42% / 58%). Kiri = 6 `.proc-step` ber-nomor yang scroll normal; kanan = `.proc-stage` **sticky** (`position: sticky; top:0; height:100vh`).
- Step aktif ditentukan via scroll: step yang centernya paling dekat ke anchor (`innerHeight*0.5`) → `.is-active`; step di atasnya → `.is-past` (connector line terisi).
- **No-redundancy:** kolom kiri sudah menamai + menomori tiap step, jadi pane kanan TIDAK mengulang — tiap tahap dapat **motif canvas generatif** yang menunjukkan apa yang dilakukan tahap itu, plus kicker satu-kata (Understand/Plan/Shape/Build/Verify/Launch) + caption.
- 6 motif draw-function: `drawDiscovery` (sinyal konvergen), `drawStrategy` (rute milestone + pulse), `drawDesign` (wireframe assembling), `drawDevelopment` (baris kode menumpuk + kursor blink), `drawTesting` (scan-line + checkmark grid), `drawDeployment` (broadcast node ke network).
- Caption crossfade via 2 layer bertumpuk (`.cap-layer`) biar tidak overlap saat scroll cepat.
- **rAF di-gate IntersectionObserver** (`visible`) — render loop diam saat section off-screen → no starvation. `prefers-reduced-motion` → stage jadi `position: relative` (un-stick).

**Catatan:** Deskripsi step 6 ("Deployment & Continuous Support") dilengkapi sendiri — tidak tercantum di PDF.

**Visual 3D node graph TIDAK dipindah ke sini** — tetap di Living Architecture; Process pakai motif canvas terpisah.

**Mobile (`IS_TOUCH` / ≤768px):** motif canvas di-drop (`.proc-stage display:none`) + stage init di-skip (early `return` setelah IO reveal label) — tiap step sudah punya nomor/judul/deskripsi sendiri, tidak ada konten hilang. Lihat "Mobile Responsive — Drop Heavy Effects".

---

## Section 5 — Careers ✅ Implemented

**Headline:** Build What Comes Next.

**Open Positions:**
- Innovation & Growth Manager
- Technical Lead
- Product Builder
- Full Stack Engineer

**Enrichment editorial (✅):** Tiap role-item kini punya index `01–04`, metadata per baris (`Full-time · Remote · Growth` dst — work-arrangement masih asumsi, perlu konfirmasi), dan hover diperkuat (judul geser `translateX(12px)`, fill gradient redup, index/meta/panah menyala). "What you bring" label + tag diperbesar/diterangkan, tag punya hover-to-brighten. Padding role-header & body-inner pakai `clamp(10px,1.4vw,26px)` agar panah tidak terpotong oleh `overflow:hidden`.

**Interaksi — dua layer:**

*Scan (hover):* Preview image di posisi cursor, curtain reveal/close animation.

*Read (click):* Accordion expand, role lain `opacity: 0.2`.

**Preview images ✅ ditambahkan:**
- Folder `Photo-careers-section/`, dipasang via `background-image` pada `.preview-N .preview-inner` (`cover`/center)
- Mapping per role: `innovation & growth manager.jpg`, `technical lead.jpg`, `product builder.jpg`, `fullstack engineer.jpg`
- Overlay gelap `rgba(10,10,10,0.32)` (`::after`) biar tetap restrained, `◉` placeholder dihapus

**Catatan:** Metadata role (Full-time · Remote/Hybrid · divisi) masih asumsi — perlu dikonfirmasi.

---

## Section — Industries We Serve ✅ Implemented (2026-06-30)

**Konsep:** 13 sektor yang dilayani (revisi PDF hal. 7). Layout = **dual-row marquee**.

**Mekanik:**
- `#industries` `overflow: hidden`; head block (`label` + `headline` + `sub`) reveal IO-gated.
- 2 baris (`.ind-row`), tiap baris berisi `.ind-track` dengan 2 `.ind-group` identik (group ke-2 `aria-hidden`) supaya saat scroll wrap, group duplikat menutup seam.
- **JS-driven, BUKAN CSS animation:** CSS animation cuma bisa play/pause (binary); untuk hover **memperlambat** (bukan stop), `translateX` di-set per-frame dan speed `factor` di-ease 1 → 0.18 saat `mouseenter`. Baris 1 jalan ke kiri (`dir=-1`, 38px/s), baris 2 ke kanan (`dir=1`, 32px/s).
- `t.pos` selalu naik di `[0, half)` (half = lebar 1 group); translate dijaga dalam `(-half, 0]`.
- **rAF di-gate IntersectionObserver** — loop diam saat off-screen. `prefers-reduced-motion` → IIFE langsung `return` (marquee statis).
- Edge-fade gradient di kedua tepi (`::before`/`::after`) supaya item larut, bukan terpotong tajam.

**Catatan:** Visual arc Deployments TIDAK jadi dipindah ke sini — Deployments tetap dengan arc-nya.

**13 sektor:** Government & Public Sector · Smart Cities · Digital Villages · Healthcare · Education · Finance · Hospitality · Retail & E-Commerce · Manufacturing · Logistics · Property & Real Estate · Professional Services · Startups & Enterprises.

---

## Section — Vision & Mission ✅ Implemented (2026-06-30)

**Konsep:** Visi + 5 poin misi (revisi PDF hal. 8). Layout = **editorial split**.

**Mekanik:**
- `.vm-grid` = 2 kolom (`minmax(0,1fr)` / `minmax(0,1.05fr)`). Kiri = Our Vision (`.vm-vision` `position: sticky; top:120px`), kanan = Our Mission sebagai `<ol>` ber-nomor 01–05.
- **No-redundancy:** vision = satu kalimat besar yang menetap; mission = daftar aksi numerik — dua pane beda peran, tidak mengulang.
- Reveal bertahap: label/vision-text + tiap `.vm-item` di-IO-gate, `transition-delay` di-stagger (`0.06 + i*0.08`s).
- Hover pada mission item menyalakan nomor + teks.
- Mobile: single-column (`grid-template-columns: 1fr`), vision di-unstick (`position: static`).

---

## Section 6 — CTA / Contact ✅ Implemented

**Headline:** Let's Start A Conversation.

**Mechanic:** Conversational sentence-form:
- "My name is _______, and I represent _______."
- "Reach me at _______."
- Inquiry type: pill selector (Partnership / Government / Enterprise / Investor / Career / General)
- Message textarea
- Submit → `mailto:info@cogniti.id`

---

## Section 7 — Footer ✅ Implemented

- Logo + nav links (Deployments · Careers · Contact) — "Founder" dihapus saat finalize
- © 2026 Cognitiva Solusi Indonesia · "Intelligence Infrastructure"
- Logo nav-brand smooth-scroll ke top (bukan `href="#"` mati)

---

## Hero Ambient — Particle "C → S → I" Assembly ✅ Implemented (final)

**Lokasi:** Modul IIFE pertama di dalam `<script>` utama (sebelum `/* ── Three.js sphere ── */`), render ke `<canvas id="hero-ambient">` di dalam `#hero` (z-index -1). Plus blok `.hero-meta` (pojok kanan bawah: "Systems Online" + live clock WIB + koordinat 6°10′S 106°49′E).

**Konsep (final state):**
- **Idle:** 440 partikel titik tersebar di SELURUH hero, mengalir via flow-field (layered trig pseudo-curl), wrap di tepi layar → sebaran merata, idle benar-benar acak (bukan bentuk huruf).
- **Assembly progresif:** jarak kursor ke pusat zona (CENTER x:0.76, y:0.46) menentukan `aT`. Antara `nearR` (th*0.42) dan `farR` (th*1.25) partikel merakit jadi huruf **tipografis** yang di-sample dari glyph Inter 500 (offscreen canvas → pixel alpha jadi target points). Smoothstep transisi.
- **Morph C → S → I:** 3 glyph (`LETTERS=['C','S','I']`) di-sample sekali saat font ready. Saat huruf terbentuk penuh (`ae>0.75`), tiap `HOLD=1.1` detik `curGlyph` maju ke huruf berikutnya dan target di-reassign → partikel glide morph C→S→I→C... selama kursor dekat. Tiap partikel dipetakan ke slot stabil (`i % pts.length`) per huruf agar morph bergerak jarak pendek yang koheren.
- **Assembly motion:** critically-damped lerp (`p.x += (tx-x)*k`, k=0.10*ae) — glide masuk, TANPA spring/bounce (sengaja dihindari, user tidak mau "toon force mantul").
- **Grenade burst:** saat kursor pernah masuk zona (`aT>0.6`) lalu keluar (`aT<0.25`), tiap partikel dapat impuls kecepatan radial keluar dari pusat (sp 6–8, acak) → meledak ke segala arah, friction 0.94 + flow nangkep balik. `curGlyph` di-reset ke C jadi reveal berikutnya selalu mulai dari "C".
- **Mobile (`hover:none`):** auto assemble↔scatter pelan via sin wave (fallback tanpa kursor), ikut morph C→S→I. **Tapi di ≤768px efek ini di-disable total** (`#hero-ambient display:none` + early `return`) karena assembly di-center `x:0.76` menimpa headline di layar sempit — lihat "Mobile Responsive — Drop Heavy Effects".
- **Entry:** `.hero-meta` fade-in bareng trail di `playEntry()` timeline.

**Knob utama:** `PCOUNT=440`, `th=Math.min(W,H)*0.42`, `nearR/farR`, flow `*0.30`, lerp `k=0.10`, burst `sp=6+rand*8`, morph `HOLD=1.1`, huruf `LETTERS=['C','S','I']`.

**Evolusi (untuk konteks revert):**
1. v1: random node constellation (abstrak) — ditolak, terlalu generik.
2. v2: single-line arc "C" — ditolak, terlalu seperti diagram 1 garis.
3. v3: woven mesh "C" (3 ring + diagonal) — ditolak, kelihatan network-graph cliché.
4. v4: flow-field particle → typographic C assembly + grenade burst. ✅ disukai.
5. v5 (final): + morph berurutan C→S→I saat hover (partikel tetap titik). ✅ disukai.

**Catatan selera:** "C" saja = lebih misterius/refined; "CSI" = lebih brand-forward/literal. Dipilih CSI. Kalau mau terasa lebih anggun, perlambat `HOLD` ke ~1.6–1.8s. Untuk revert ke "C" saja: set `LETTERS=['C']`.

---

## Global Background — Ambient Trail ✅ Implemented

- 20 rantai node, tiap trail 60 node, spring physics
- `lighter` blend mode, warna `hsla(210–230, 10%, 95%, 0.035)`
- `position: fixed`, `z-index: 11`, `pointer-events: none`
- Visible di semua section termasuk manifesto

---

## Mobile Responsive — Drop Heavy Effects ✅ (2026-06-30)

**Konsep:** efek dekoratif yang di-tuning untuk desktop (lebar layar + pointer presisi) di viewport sempit malah menumpuk di atas teks atau menjalankan WebGL/rAF loop mahal tanpa benefit. Solusi: di `≤768px` / `IS_TOUCH`, sembunyikan efeknya **dan** skip loop JS-nya (bukan cuma `display:none` — loop tetap jalan kalau hanya CSS), tanpa kehilangan konten (no-redundancy: tiap efek yang dibuang sudah punya teks/list penggantinya).

Branch: `feat/mobile-responsive-heavy-effects` · commit `c7e5c1d` (push ke origin). Total diff: `index.html` +53 / −12.

**4 perubahan:**

1. **Hero ambient (glyph C→S→I)** — assembly di-center pada `x:0.76`; di desktop ada ruang kosong di samping headline (max 900px), tapi di HP justru menimpa "Build Intelligence" + subtext → bug yang dilaporkan user (screenshot). Fix: `#hero-ambient { display:none }` di `@media(max-width:768px)` + early `return` di IIFE (`window.IS_TOUCH||innerWidth<=768`) supaya rAF loop tidak jalan. (index.html CSS ~532-534, JS ~1181-1184)

2. **Hero sphere (Three.js)** — di aspect portrait sphere (radius ~1 + displacement) terpotong horizontal. Fix: `fitHeroCamera()` menarik kamera mundur (`needZ=1.3/(halfH*min(1,aspect))`, `Math.max(2.8,…)` jadi desktop aspect≥1 tetap z=2.8). Independen dari math collapse `playEntry()` (yang nge-scale elemen canvas, bukan kamera). (index.html ~1348-1358)

3. **Process motif canvas** — kolom kiri sudah menamai+menomori tiap step, jadi motif kanan murni dekoratif → `.proc-stage { display:none }` + early `return` di IIFE setelah IO reveal label di-pasang (no rAF loop, no scroll listener, no draw). (index.html CSS ~591-593, JS ~1870-1872)

4. **Living Architecture 3D node graph** — graph WebGL kedua, heavy + pointer-reliant. Fix: `.la-right { display:none }`, dan JS bikin **static list** 6 alasan di kolom kiri (`#laListMobile`, class `.la-list-mobile`/`.la-m-item`/`.la-m-num`/`.la-m-name`/`.la-m-micro`) dari array `ND` lalu `return` — context WebGL kedua + rAF loop-nya tidak jalan di HP. `laHint` ("Click any node…") di-hide karena tak ada graph. (index.html CSS 274 + 571-582, HTML 862, JS 2264-2279)

**Pola seragam:** Services sudah pakai pola ini lebih dulu (`buildServicesMobile()` — 3D conveyor diganti `.svc-list-mobile`). Hero/Process/Living-Arch sekarang ikut pola yang sama: efek desktop = di-skip; konten = list/teks statis pengganti.

**Verifikasi (Puppeteer, iPhone 390×844, `/tmp/csi-shots/mobile-verify.js`):** `laListItems:6`, `laRightDisplay:"none"`, `procStageDisplay:"none"`, hero-ambient `display:none` (blob hilang, headline/orb-glyph/subtext/CTA legible). Grayscale tetap bersih, tidak ada konten hilang.

---

## Mobile Responsive — Full Audit & Layout Fixes ✅ (2026-06-30)

**Konsep:** lanjutan dari "Drop Heavy Effects". Audit menyeluruh semua section di `≤768px` (320–414px) buat ketemu overlap, tap target kekecilan, font scaling, spacing rhythm, dan dead gap. Semua perbaikan murni CSS (+ 1 geometri JS arc), no konten hilang.

**7 perubahan:**

1. **Deployments arc — overlap dgn teks kiri** (bug dilaporkan user, screenshot). Apex arc di-center `x:0.50` (DCX) numpuk sama kolom teks 62% → garis+label "01 Public Services" ketimpa headline. Fix dua arah: (a) geometri JS `DAX=DVW*(DMOB?0.56:0.50)` — apex digeser kanan di mobile (`DMOB=DVW<=768`); (b) CSS `.deploy-left` 62%→54%, headline+copy diperkecil. (index.html JS ~1554-1556, CSS ~546-554)

2. **Living-arch "Why cogniti?" — list jadi kartu** (user minta opsi list bersih). Fallback mobile sebelumnya pakai card chrome (border + gradient bg). Diganti list minimal: `border-top: 1px solid #1E1E1E` per item, item pertama tanpa garis, no border/bg. Plus `.la-left justify-content: flex-start` (dari desktop `center`) + headline `margin-bottom: 0` buat hapus dead gap antara headline & item pertama. (index.html CSS ~564-575)

3. **Hamburger tap target** — 26×16px (di bawah min a11y 44px). Jadi 44×44px flex hit area, icon `::after` di-recenter `left:50%/translate(-50%,-50%)`, `margin-right:-9px` biar tetap rapat ke edge. (index.html CSS ~522-528)

4. **Manifesto — teks ketekan** — `.block-wrap` padding `0 12vw` (≈45px/sisi di 375px) bikin teks center jadi strip sempit. Override mobile `padding: 0 var(--pad)` + `line-height:1.3`. (index.html CSS ~540-542)

5. **CTA form — dead gap antar field** (terburuk). Field stacked mewarisi desktop `.form-line line-height: 2.6` → jarak vertikal raksasa. Reset `line-height:1.5` + `.form-sentence gap:18px` buat rhythm baris. (index.html CSS ~617-621)

6. **Menu overlay — clip di HP pendek** — desktop `.menu-body overflow:hidden` + `.menu-times margin-top: clamp(80px,11vw,160px)` motong timezone block di layar pendek. Override `overflow-y:auto` + `padding 48px` + `.menu-times margin-top:8px`. (index.html CSS ~518-520)

7. **Services conveyor + 480px polish** — kartu `min(74vw,320px)`/`min(96vw,420px)` (dari floor 260px) biar center card pas, drag hint diangkat, headline `top:64px`. Block `≤480px`: subtext/CTA/deploy headline/arc-category diperkecil. (index.html CSS ~556-562, ~632-641)

**Verifikasi (Puppeteer headless Chrome, touch-emulated):** overflow horizontal **0** di 320/360/375/414px (`docW===winW` semua). Screenshot tiap section (hero, manifesto, deployments 5-step arc, services conveyor, why-cogniti list, process, careers, industries, vision, CTA form, menu overlay 390×844 + 360×640) — semua bersih, arc clear dari teks, form rhythm rapi, menu pendek scrollable. **Belum diuji:** gesture nyata (drag/tap) & landscape — headless cuma layout.

---

## Mobile Responsive — Careers Padding & Services Flip Fixes ✅ (2026-06-30)

**Konsep:** lanjutan polish dari Full Audit. Dua bug spesifik dilaporkan user (screenshot), keduanya murni CSS.

**2 perubahan:**

1. **Careers — padding role-list nggak konsisten** (bug dilaporkan user, screenshot). `.role-header { flex-wrap: wrap }` bikin judul panjang #01 "Innovation & Growth Manager" turun ke baris flex baru di bawah nomor (flush-left), sedangkan judul pendek #02-04 tetap nempel di samping nomor (ke-indent). Fix: `.role-title { flex: 1; min-width: 0 }` — judul tetap di baris nomor & wrap teksnya sendiri di dalam; `.role-meta`/`.role-arrow` dikasih `flex-basis: 100%` + `padding-left: clamp(36px, 3.5vw, 56px)` (match lebar `.role-index`) biar align rapi di bawah judul. (index.html CSS ~604-609)

2. **Services — flip card backface bleed** (bug dilaporkan user, screenshot). Pas kartu di-flip, teks front yg ke-mirror ("Custom Software Development" kebalik) nembus tembus ke back face. Penyebab: cuma back face yg punya transform 3D (`rotateY(180deg)`), jadi browser render-nya di konteks 3D & hormatin `backface-visibility: hidden`; front face nggak punya transform → dianggap flat (2D) → backface culling-nya diabaikan → front kebalik bocor. Fix: kasih identity transform eksplisit `.svc-front { transform: rotateY(0deg) }` biar front tetap di konteks 3D & backface-nya ke-cull. Satu rule shared → beresin semua 9 kartu sekaligus (termasuk AI card #4 yg back face-nya beda). (index.html CSS ~235)

**Verifikasi (Puppeteer headless Chrome):** careers 390×844 — #01 judul panjang sekarang konsisten ke-indent kayak #02-04, meta/arrow align di bawah judul. Services 1280×900 — flip kartu #0/#1/#3/#4 semua back face bersih, no mirror bleed.

---

## Mobile Responsive — Services AI Card Back-Face Overflow ✅ (2026-06-30)

**Konsep:** bug spesifik dilaporkan user (screenshot) — back face kartu AI (#4 / "Artificial Intelligence Solutions") teksnya nembus keluar card di mobile. Murni CSS, mobile-only override.

**1 perubahan:**

- **AI card back-face overflow** (bug dilaporkan user). Back face AI punya konten paling banyak dari semua kartu (corner label absolut + deskripsi + label + 5 sub-item), sementara card di mobile di-cap `height: min(96vw, 420px)`. Default `.svc-back-ai { justify-content: center }` bikin konten yang lebih tinggi dari card meluber **dua arah**: atas nabrak corner label absolut ("ARTIFICIAL INTELLIGENCE SOLUTIONS" yang wrap jadi 2 baris di card sempit), bawah bullet terakhir ("Custom AI Integration") jatuh keluar tepi bawah. Fix (override di `@media (max-width: 768px)`): `justify-content: flex-start` (anchor ke atas, bukan center), `padding-top: 74px` biar lewat 2-baris corner label, tighten `gap`/font deskripsi+sub-item, + `overflow-y: auto` sebagai jaring pengaman. (index.html CSS ~572-578)

**Verifikasi (Puppeteer iPhone, nav ArrowRight ke card #3 lalu flip):** 360px — corner clear, deskripsi penuh, 5 bullet semua di dalam frame, `scrollH===clientH` (no internal scroll), bullet terakhir 37px di dalam tepi bawah. 390px — sama, bullet terakhir 66px di dalam. Tidak ada overlap corner↔deskripsi di kedua lebar.

---

## Referensi Visual

| Elemen | Inspirasi |
|---|---|
| Immersive 3D/WebGL | Active Theory |
| Smooth scroll + typografi bold | Locomotive |
| Stack & scalability | Basement Studio |
| Entry animation mechanic | Make Reign |
| Trust signals + enterprise tone | Stripe |

---

## Finalize — Pre-Launch Hardening ✅ (2026-06-29)

Audit kritikal sebelum finalize, lalu di-fix:

**#1 — Blank-page failsafe** (`<head>`, setelah CDN scripts)
`<main>` disembunyikan via `page-loading` sampai user scroll pertama → `playEntry()`. Risiko: kalau CDN (GSAP/Three.js) gagal load, intro tidak pernah jalan & halaman blank selamanya. Fix: guard sinkron — kalau `gsap`/`THREE` undefined (CDN script render-blocking, jadi pasti sudah resolve di titik ini), langsung remove `page-loading`.
> ⚠️ JANGAN tambah timeout auto-reveal: sphere full-screen memang idle nunggu scroll user (bisa >3.5s). Timeout malah reveal `main` saat `#hero` masih `opacity:0` & sphere belum collapse → half-broken state. Versi awal sempat pakai timeout 3.5s, di-revert.

**#2 — SEO & social metadata** (`<head>`, 13 tag)
Sebelumnya nol. Ditambah: meta description, canonical, favicon (`Logo/Logo-Final.png`) + apple-touch-icon, theme-color, Open Graph (title/desc/url/image), Twitter Card. OG/Twitter image → `Foto Speaking.jpg`.
> URL absolut pakai `https://cogniti.id/` — ganti kalau domain produksi beda (crawler butuh URL absolut buat fetch preview image).

**#3 — Favicon** — sebelumnya 404, sekarang pakai logo.

**#5 — Asset hygiene**
- `loading="lazy"` di 3 img below-the-fold (2 founder thumb + footer logo); 3 navbar logo tetap eager (LCP).
- `Logo-Final 2.png` (unused, 45KB) dihapus via `git rm`.

**#6 — Dead links** (`href="#"`)
- Footer "Founder" dihapus.
- Social (menu overlay): Instagram → `instagram.com/baliinteraktifperkasa`, LinkedIn → `linkedin.com/company/bali-interaktif-perkasa`, X **diganti Facebook** → `facebook.com/p/Bali-Interaktif-Perkasa-...`. Semua `target="_blank" rel="noopener noreferrer"`.
- 3 logo nav-brand → click handler smooth-scroll ke top (no stray `#`).

**Belum dikerjakan (#4):** file non-produksi masih ter-track git (`*-demo.html`, `*.md`, dll) — publicly reachable kalau seluruh repo di-deploy. Perlu di-exclude/hapus sebelum deploy.

**#7 — A11y & kontras (2026-06-30)**
- **Link color leak:** UA default mewarnai `<a>` tanpa `color` eksplisit jadi biru (`rgb(0,0,238)`) — bocor di tema grayscale. Fix: `color: inherit` pada `.nav-brand` & `.menu-right-item`.
- **Kontras label:** sejumlah section-label pakai abu terlalu gelap (#2A2A2A/#333 di atas #0A0A0A ≈ 1.3–1.7:1, gagal WCAG). Dinaikkan ke **#5A5A5A** (≈ 3:1, lolos AA-large) di label Manifesto/Deployments/Services/Living-Arch/Careers/Process.

**#8 — Refresh-freeze keyboard (2026-06-30)**
Page-reveal di-gate sampai first scroll intent (`onFirstScroll` → `playEntry()`). Pengguna keyboard tak pernah memicu `wheel`/`touchmove`, jadi halaman beku. Fix: listener `keydown` + set `SCROLL_KEYS` (Space/PageUp-Down/Arrow/Home/End) → `onFirstScrollKey` ikut memicu reveal.

**#9 — Orb klik: reset ke sphere section (2026-07-01)**
Orb kecil di heading hero (`#orbSlot`, sebelah "Build Intelligence") dibuat interaktif. Klik orb → `replayIntro()` me-*reverse* animasi intro: hero + navbar full + trail + subtext fade out, sphere `hCanvas` mekar balik dari orb ke full-screen dan **berhenti** di state idle awal (pre-scroll) — navbar-minimal + scroll-hint muncul lagi, scroll di-lock ulang (`page-loading`), scroll-position di-reset ke atas.
- Gesture scroll-pertama di-refactor jadi pasangan `armFirstScroll()` / `disarmFirstScroll()` supaya bisa di-*re-arm* setelah reset → scroll lagi meng-collapse sphere ke orb, siklus berulang persis kunjungan pertama.
- Guard `scrollAnimsBuilt` di `setupScrollAnimations()` — ScrollTrigger cuma dibangun sekali; replay hanya re-arm scroll (mencegah trigger dobel).
- Guard `isReplaying` + cek `scrollY > innerHeight*0.5` mencegah timeline overlap & klik saat tidak di atas.
- CSS: `#orbSlot` diberi `pointer-events:auto; cursor:pointer` + hover ring lebih terang (sebelumnya inherit `pointer-events:none` dari `#hero`).

**#10 — Navbar: tambah link section Services & Approach (2026-07-01)**
Setelah revisi konten, halaman punya 8 section tapi navbar cuma nge-link 3 (Deployments/Careers/Contact). Empat section tak ter-link: manifesto, services, living-arch, process. Dikurasi **+2 yang paling menjawab intent B2B**, bukan tambah semua (navbar minimal = kekuatan brand cogniti).
- **Navbar final (5 item, urut scroll):** Deployments · Services · Approach · Careers · Contact.
  - `Services` → `#services` (gap paling kritis: pertanyaan #1 klien "kalian ngerjain apa?").
  - `Approach` → `#living-arch` (section "Why cogniti?", diferensiasi/trust). Label dipilih "Approach" (noun pendek, sejajar item lain) alih-alih "Why cogniti".
  - **Skip** Process (sekunder) & Manifesto (storytelling saat scroll, bukan destinasi).
- **Sinkron 3 lokasi nav:** `#navbar .nav-links` (desktop), `#menu-overlay .menu-nav` (mobile), DAN `.footer-nav` (footer). Sekalian membereskan inkonsistensi lama — overlay tadinya punya "Manifesto" yang tak ada di desktop; footer tadinya masih 3 item lama. Kini ketiganya identik.
- **CSS guard `@media (max-width:1024px)`:** gap `.nav-links` 40→26px + font 12.5→11.5px biar 5 link tak nabrak logo / "Talk to us" di laptop sempit. Di ≤768px desktop nav hilang total (diganti overlay), jadi aman.
- Handler smooth-scroll `.menu-nav a` sudah generik → link baru otomatis jalan.

**#11 — Process: rapetin gap heading → step pertama (2026-07-01)**
Gap antara "Our Development Process." dan step "Discovery" kejauhan (hampir 1 layar kosong). Penyebab: `.proc-steps { padding: 42vh 0 42vh }` — runway scroll yang disengaja supaya tiap step di-highlight pas pusatnya mencapai tengah viewport (`anchor = innerHeight*0.5`), selaras dgn panel visual kanan `.proc-stage` yang sticky 100vh.
- Fix: padding atas **42vh → 16vh** (rapetin gap), bawah **42vh → 36vh** (dijaga lebih besar buat sync step terakhir).
- Trade-off (minor): step-0 aktif sedikit lebih awal sebelum panel kanan fully pinned — perbedaan tipis, hampir tak kelihatan.
- Breakpoint mobile `.proc-steps` (`24px 0 64px`) tak disentuh.

**#12 — Footer: isi baris kontak + social (2026-07-01)**
Footer terasa kosong (cuma logo + nav + copyright). Ditambah baris kontak di antara `footer-top` dan `footer-bottom`, **pakai data yang sudah ada di site** (tak mengarang):
- **Email** `hello@cogniti.id` — clickable `mailto:`, warna sedikit lebih terang (utility utama footer B2B). Email juga diganti di handler form CTA (`window.location.href` mailto) supaya konsisten (2 tempat).
- **Alamat kantor** `Jl. Kediri No.27, Tuban, Badung, Bali 80361` (dari company-profile) — bukti perusahaan nyata → trust.
- **Social** Instagram / LinkedIn / Facebook — sebelumnya hanya di menu overlay, kini juga di footer (`target="_blank" rel="noopener noreferrer"`).
- Gaya konsisten dgn footer existing (uppercase kecil, centered). Mobile ≤480px: email & alamat stack vertikal, separator "·" di-hide.

---

## Pending / To Do

- [x] Foto founder — thumbnail `Photo profile.jpg` + floating `Foto Award.jpeg` / `Foto Speaking.jpg`
- [x] Preview images Careers — foto editorial per role (`Photo-careers-section/`: 4 role)
- [x] Arc Deployments bleed ke tepi atas/bawah (`DVISHALF` vs `DHALF`)
- [ ] Konten pencapaian founder yang nyata (teks masih placeholder — dikonfirmasi ke founder)
- [ ] Konfirmasi metadata role Careers (work-arrangement `Full-time/Remote/Hybrid` + divisi masih asumsi)
- [ ] Navbar blur/scrim saat scroll lewat hero (ditunda — "nanti aja")
