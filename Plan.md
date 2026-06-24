# Plan — cogniti Landing Page MVP 1

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
| **Logo (dark bg)** | `asset/Logo-Final.png` (gray) |
| **Logo (light bg)** | `asset/Logo-Final 2.png` (navy) |

---

## Stack (MVP 1 — Single HTML)

- GSAP + ScrollTrigger (CDN)
- Three.js (CDN)
- Lenis smooth scroll (CDN)
- Tailwind CSS (CDN)

> Next.js dipakai saat migrasi ke production (post MVP 1)

---

## Color Palette

Filosofi: **accent bukan warna, tapi kontras.** Monokromatik murni.

| Role | Hex |
|---|---|
| Background | `#0A0A0A` |
| Surface | `#141414` |
| Border | `#1F1F1F` |
| Text primary | `#F0F0F0` |
| Text secondary | `#888888` |
| Text muted | `#444444` |
| Accent (cold white) | `#FFFFFF` — sparingly |
| Logo mark | Merah — logo only, tidak masuk UI |

Feel referensi: Linear, Vercel.

---

## Theme

Hybrid — bukan pure dark, bukan pure light:

| Section | Theme |
|---|---|
| Hero | Dark |
| Manifesto / Approach | Dark / near-black |
| Who We Serve | Sedikit lebih terang |
| CTA / Footer | Dark |

---

## Struktur Section

| # | Section | Fungsi |
|---|---|---|
| 1 | **Hero** | Curiosity |
| 2 | **Manifesto** | "Kami percaya bahwa..." — Signal of Thinking, bukan Scale |
| 3 | **Founder** | Otoritas personal — Fami Maliki |
| 4 | **Approach** | Cara berpikir & bekerja CSI |
| 5 | **Who We Serve** | Visitor self-identify |
| 6 | **CTA / Contact** | Dorongan konversi |
| 7 | **Footer** | — |

> Minimal project, klien, dan produk — credibility dibangun lewat cara berpikir dan siapa di baliknya, bukan portfolio. Pendekatan McKinsey/Stripe.
> Loading Screen ditunda, bukan bagian dari MVP 1 awal.

---

## Section 1 — Hero

### Headline
```
We build the infrastructure that thinks.
```

### WebGL Concept — "The Core"

Kombinasi dua pendekatan:

- **C (base):** Morphing geometric form (sphere/polyhedron) di center — breathes/morphs perlahan → **intelligence**
- **B (layer):** Data streams mengalir masuk dan keluar dari form → **infrastructure**

| Elemen | Detail |
|---|---|
| Background | Near-black `#0A0A0A` |
| Form | Wireframe / subtle glow, putih low opacity |
| Streams | Putih/abu, very low opacity, varying thickness |
| Pulse | Bright white flash sesekali travel di sepanjang stream |
| Cursor | Form terdistorsi, streams deflect/tertarik |

Narasi visual: Form = intelligence, Streams = infrastructure → menceritakan *"infrastructure that thinks"* secara visual tanpa teks.

### Entry Animation — "Collapse into Text"

Terinspirasi dari analisis frame-by-frame Make Reign (`asset/frames/`, 215 frame).

**Sequence:**

1. WebGL **full-screen** saat entry — immersive, belum ada teks
2. On load selesai → WebGL **mengkerut** dan reposition ke inline
3. Headline muncul, WebGL mini duduk di dalam kalimat:

```
We build the [◉] infrastructure that thinks.
```

`[◉]` = miniatur WebGL yang terus breathing/morphing.

**Teknikal:**
- GSAP timeline mengontrol seluruh sequence
- Three.js canvas di-scale dan di-reposition via `gsap.to(canvas, { width, height, x, y })`
- Setelah settle, canvas tetap animating (ambient loop)

**Kenapa ini works:**
- WebGL full-screen di awal = rasa penasaran maksimal
- Collapse ke dalam teks = reveal yang satisfying
- Headline jadi lebih bernyawa — bukan teks di atas background, tapi teks yang *mengandung* intelligence

---

## Section 2 — Manifesto ✅ Demo selesai

**Demo:** `manifesto-demo.html`

**Konsep:** Worldview building — kalimat dibangun kata per kata saat scroll. ATM dari MakeReign (word-by-word reveal). Tidak ada foto, tidak ada produk. Pure teks.

**Copy (final — 4 block):**
1. Software connected information. Intelligence connects decisions.
2. Organizations are drowning in data. Yet struggling to act.
3. The future belongs not to those who collect, but to those who act.
4. Intelligence should exist across every interaction. Every workflow. Every decision.

**Interaksi (final):**
- Section pinned saat scroll, total scroll `4 × 100vh`
- Tiap kata reveal satu per satu via GSAP ScrollTrigger `scrub: 2`
- **Reveal:** `opacity 0 → 1`, `y: 14 → 0`, `rotation: +6° → 0°` — kata jatuh dari bawah sambil meluruskan diri (`ease: power3.out`)
- **Hold:** semua kata visible sebentar setelah blok selesai
- **Keluar:** `opacity 1 → 0`, `y: 0 → 14` — slide down tanpa rotate (`ease: power3.in`, lebih cepat dari reveal)
- Progress bar 4 segmen di bottom center
- Ambient trail tetap jalan di background

**Keputusan desain:**
- Font: Inter, `clamp(26px, 3.4vw, 52px)`, letter-spacing `-0.03em`
- `.word` harus `display: inline-block` agar GSAP bisa transform (inline tidak bisa)
- Tidak ada snap — user kontrol penuh ritme baca lewat scroll
- Referensi animasi: `asset3/frames/` (MakeReign word-by-word reveal)

---

## Section 3 — Founder ✅ Demo selesai

**Konsep:** ATM dari MakeReign — cursor-following image preview applied ke profil founder.

**Demo:** `founder-section-demo.html`

**Layout (final):**
- Kiri: card kecil — thumbnail foto + "Fami Maliki" + "FOUNDER & CEO" (per row)
- Kanan atas: deskripsi singkat pencapaian (36px, letter-spacing tight)
- Kanan bawah: metadata bar — `TYPE · CATEGORY · YEAR · ↗`
- Divider `1px #1A1A1A` antar item, padding `88px 0`

**Interaksi (final):**
- Hover zone: hanya text deskripsi (`.item-desc`)
- On hover → foto founder muncul sebagai floating card mengikuti cursor
- Pop-in: scale `0.05 → 1`, spring easing `cubic-bezier(0.34, 1.56, 0.64, 1)`, durasi `0.7s`
- Pop-out: scale `1 → 0.05`, `0.2s ease` (cepat)
- Momentum tilt: foto rotate berlawanan arah kecepatan mouse (`velocityX * 0.4`)
- Text scramble: karakter acak resolve kiri→kanan dalam `420ms`, dimensi dikunci saat scramble (fix reflow bug)
- Cursor berubah jadi `+` crosshair saat hover
- Non-hovered items: opacity `0.2`

**Konten:**
| Elemen | Isi |
|---|---|
| Nama | Fami Maliki |
| Jabatan | Founder & CEO, Cognitiva Solusi Indonesia |
| Pencapaian | 3 item — Awards + Speaking (TBD — dikonfirmasi ke founder) |
| Foto | Placeholder → diganti foto editorial founder |

**Fungsi:** Otoritas personal — membangun kepercayaan via kredibilitas manusia di balik perusahaan.

**Referensi:** `asset2/Screen Recording 2026-06-23 at 07.09.02.mov` + `asset2/frames/`

---

## Section 4 — Approach

> TBD — cara berpikir & bekerja CSI

---

## Section 5 — Who We Serve

5 segmen target + value prop masing-masing:

1. Enterprise
2. Investor
3. Government
4. Strategic Partner
5. Talent

> TBD — copy per segmen

---

## Section 6 — CTA / Contact

> TBD — email placeholder

---

## Section 7 — Footer

> TBD

---

## Global Background — Ambient Trail ✅ Demo selesai

**Demo:** `manifesto-trail-demo.html`

**Konsep:** Spring-trail canvas animation sebagai ambient background di semua section.

**Teknikal:**
- 20 rantai node (trail), tiap trail 60 node, spring physics follow cursor
- `lighter` blend mode — area padat lebih terang secara natural
- Warna: `hsla(210–230, 10%, 95%, 0.035)` — cold white, hampir ghost
- Line width: `0.75px`
- Canvas: `position: fixed`, `z-index: 0`, `pointer-events: none` — duduk di bawah semua konten
- Hanya terasa saat trails menumpuk dekat cursor

**Feel:** Subtle, intelligent, ambient — tidak distract dari teks/konten.

---

## Referensi Visual

| Elemen | Inspirasi |
|---|---|
| Immersive 3D/WebGL | Active Theory |
| Smooth scroll + typografi bold | Locomotive |
| Stack & scalability | Basement Studio |
| Entry animation mechanic | Make Reign |
| Trust signals + enterprise tone | Stripe |
