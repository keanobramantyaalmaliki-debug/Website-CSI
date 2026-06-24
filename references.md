# Website References — CSI Landing Page

Referensi visual dan teknikal untuk membangun landing page CSI (Cognitiva Solusi Indonesia).

---

## 1. Locomotive — [locomotive.ca](https://locomotive.ca)

**Kategori:** Creative Digital Agency

### Visual & Feel
- Minimalis tapi berkarakter — typografi besar, whitespace luas
- Animasi teks cycling di hero (stagger/typewriter effect)
- Transisi halaman yang smooth dan intentional

### Teknikal
- Vanilla JS (sengaja tidak pakai framework)
- **Locomotive Scroll** — library scroll buatan mereka sendiri
- Lazy-loading dengan SVG placeholder

### Yang bisa diadopsi untuk CSI
- Teknik smooth scroll
- Typografi hero yang bold dan cycling
- Filosofi "less is more" — animasi yang purposeful, bukan sekadar gimmick

---

## 2. Active Theory — [activetheory.net](https://activetheory.net)

**Kategori:** Creative Digital Experience Studio

### Visual & Feel
- Full immersive — WebGL/3D sebagai elemen utama, bukan dekorasi
- Tagline: *"Creative Digital Experiences"*
- Dark, cinematic, high-impact
- Interaksi cursor yang reaktif

### Teknikal
- Heavy Three.js / WebGL
- Custom GLSL shaders
- High GPU-demanding experience

### Yang bisa diadopsi untuk CSI
- Pendekatan 3D/particle sebagai background atau hero element
- Cursor interaktif
- Tone dark & immersive yang sesuai dengan "Intelligence Infrastructure"

---

## 3. Basement Studio — [basement.studio](https://basement.studio)

**Kategori:** Digital Product & Creative Studio

### Visual & Feel
- Next-generation digital experience
- Kombinasi 3D, motion design, dan typografi
- Dark aesthetic, performance-conscious
- Layout yang tight dan dense tapi tetap breathable

### Teknikal
- **Next.js** (confirmed dari `/_next/image`)
- **Sanity CMS** untuk konten
- **Vercel** untuk hosting
- GSAP / Framer Motion (inferred)

### Yang bisa diadopsi untuk CSI
- Stack Next.js + Sanity (scalable dari MVP ke full site)
- Pendekatan 3D motion yang tetap readable
- Dark theme yang terasa premium bukan murahan

---

## 4. Make Reign — [makereign.com](https://www.makereign.com)

**Kategori:** Digital Interface & Transformation Company

### Visual & Feel
- "Beta Mode" aesthetic — ada elemen loading counter, progress indicator
- Dynamic counter & live metrics sebagai elemen UI (`Insights 18`, `We are Hiring 03`)
- Multi-step form / modal panel yang smooth
- Interaksi yang terasa seperti software/product, bukan website biasa

### Teknikal
- JavaScript-heavy rendering
- Loading/progress animation di entry
- Reactive UI (kemungkinan React/Vue)

### Yang bisa diadopsi untuk CSI
- Loading screen dengan counter (sangat cocok untuk "Intelligence" feel)
- Angka/metrik sebagai elemen visual
- UI yang terasa seperti dashboard/product — selaras dengan positioning tech company

---

## 5. Stripe — [stripe.com](https://stripe.com)

**Kategori:** Financial Infrastructure / Enterprise Tech

### Visual & Feel
- Premium, dark-gradient dengan animated wave hero yang ikonik
- Typografi editorial besar dengan italic emphasis
- Layout bento grid untuk showcase produk
- Data sebagai desain — angka besar (`$1.9T`, `99.999% uptime`) sebagai visual anchor
- Subtle tapi purposeful — scrolling marquee, accordion, carousel

### Teknikal
- Custom animated WebGL/Canvas hero (wave)
- Subtle scroll-triggered animations
- Real UI screenshots dalam product cards
- Dual-audience language: developer + enterprise buyer

### Yang bisa diadopsi untuk CSI
- **Statistik/angka besar sebagai trust signal** — sangat relevan untuk audiens Enterprise & Government
- Bento grid untuk showcase layanan
- Tone: *authoritative yet approachable*
- Animated hero element yang ikonik (CSI versi: data/neural network visualization?)

---

## Synthesis — Arah Visual CSI

Dari 5 referensi di atas, CSI Landing Page idealnya berada di perpotongan:

| Elemen | Inspirasi |
|---|---|
| **Immersive 3D/WebGL** | Active Theory |
| **Smooth scroll & typografi** | Locomotive |
| **Stack & scalability** | Basement Studio |
| **UI/product feel + loading screen** | Make Reign |
| **Trust signals & enterprise tone** | Stripe |

### Tone yang dituju
> Dark. Intelligent. Immersive — tapi tetap credible di mata Enterprise, Investor, dan Government.

### Elemen yang wajib ada
- Loading screen dengan animasi (Make Reign influence)
- Hero dengan 3D/particle/WebGL element (Active Theory influence)
- Typografi besar dan bold (Locomotive influence)
- Angka/statistik sebagai visual (Stripe influence)
- Smooth scroll (Locomotive Scroll / Lenis)
