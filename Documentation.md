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
| 4 | **Living Architecture** | `#living-arch` | Interactive 3D simulation — centerpiece |
| 5 | **Careers** | `#careers` | Talent acquisition |
| 6 | **CTA / Contact** | `#cta` | Dorongan konversi |
| 7 | **Footer** | `#footer` | — |

> Minimal project, klien, dan produk — credibility dibangun lewat cara berpikir dan siapa di baliknya, bukan portfolio. Pendekatan McKinsey/Stripe.
> Loading Screen ditunda, bukan bagian dari MVP 1 awal.
> "Who We Serve" section dihapus — digantikan Living Architecture.
> **Founder section dihapus (2026-06-29)** atas permintaan atasan. Semua kode (CSS + HTML + JS hover & achievement overlay) di-backup ke `Backup-Founder-Section.md` untuk re-integrasi sewaktu-waktu. Kandidat pengganti slot lama: "Industries We Serve" (lihat `Revisi.md`) — belum diputuskan.

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

**Kandidat pengganti slot lama (Careers → CTA):** "Industries We Serve" (13 sektor, dari `Revisi.md`) — belum diputuskan; ada pertimbangan tumpang tindih dengan Deployments.

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
- **Mobile (`hover:none`):** auto assemble↔scatter pelan via sin wave (fallback tanpa kursor), ikut morph C→S→I.
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

---

## Pending / To Do

- [x] Foto founder — thumbnail `Photo profile.jpg` + floating `Foto Award.jpeg` / `Foto Speaking.jpg`
- [x] Preview images Careers — foto editorial per role (`Photo-careers-section/`: 4 role)
- [x] Arc Deployments bleed ke tepi atas/bawah (`DVISHALF` vs `DHALF`)
- [ ] Konten pencapaian founder yang nyata (teks masih placeholder — dikonfirmasi ke founder)
- [ ] Konfirmasi metadata role Careers (work-arrangement `Full-time/Remote/Hybrid` + divisi masih asumsi)
- [ ] Navbar blur/scrim saat scroll lewat hero (ditunda — "nanti aja")
