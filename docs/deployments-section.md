# Section — Selected Deployments

**Status:** Planned — belum diimplementasi  
**Demo file:** `deployments-demo.html` (akan dibuat)

---

## Objective

Memberi kredibilitas tanpa membuka portfolio detail. Bukan case study section — ini adalah implied authority: coverage sektor sebagai sinyal kepercayaan.

Pola ini dipakai McKinsey, BCG, Deloitte: tunjukkan sektor tanpa buka nama klien. Untuk audiens Enterprise dan Government, ketidakjelasan yang confident terasa lebih profesional dari case study yang dipaksakan.

---

## Posisi dalam Funnel

| Section | Fungsi |
|---|---|
| Hero | Penasaran |
| Manifesto | Penasaran → Otoritas awal |
| Founder | Otoritas personal |
| **Deployments** | **Otoritas terbukti** |
| Who We Serve | Transisi — visitor self-identify |
| CTA | Dorongan konversi |

---

## Content

**Section label:** Selected Deployment Environments  
**Subheadline:** Built for real-world environments where decisions matter.

| # | Category | Copy | Region |
|---|---|---|---|
| 01 | Public Services | Digital transformation initiatives for citizen engagement, operational visibility, and service coordination. | Indonesia |
| 02 | Infrastructure | Integrated monitoring environments connecting assets, operations, and situational awareness. | Indonesia |
| 03 | Logistics | Operational intelligence deployments supporting visibility, workflow optimization, and decision support. | International |
| 04 | Hospitality | Intelligence-driven engagement frameworks for modern guest experiences. | Southeast Asia |
| 05 | Communities | Connected environments that improve communication, participation, and collective action. | Indonesia |

**Rules (hard):**
- No client logo
- No project name
- No screenshots
- No pricing
- No product detail

---

## Visual Reference

**Referensi:** WOVE by Polyera — `Deployment-assets/frames/` (353 frame)

### Mekanik Inti: Arc-Spine

Sebuah kurva besar (bagian kanan dari lingkaran dengan radius ~900px, center di far-left viewport) berfungsi sebagai "tulang punggung." Items ditempatkan sebagai titik-titik sepanjang kurva.

**Signature mechanic:** Teks setiap item dirotasi mengikuti sudut tangen kurva di posisi item itu — bukan horizontal. Item di atas kurva miring ~+15°, item di tengah ~0°, item di bawah ~-15°. Teks secara literal "mengikuti" arah kurva.

---

## Layout

```
[KIRI — fixed/sticky]              [KANAN — arc bergerak saat scroll]

Selected                           ·  01  Public Services     Indonesia
Deployment                         ·  02  Infrastructure      Indonesia
Environments.                      ·  03  Logistics           International
                                   ·  04  Hospitality         Southeast Asia
[copy aktif muncul di sini]        ·  05  Communities         Indonesia
```

- Copy tiap deployment muncul di panel kiri saat item tersebut aktif (di center viewport)
- Arc bergerak ke atas saat scroll, items menaikinya dan berotasi mengikuti tangen
- Item aktif: opacity 1, warna `#D0D0D0` → `#F0F0F0`
- Item inactive (below): opacity ~0.35, muted
- Item passed (above): fade out, hampir invisible

---

## Implementasi Teknikal

### Arc Math

```js
// Arc = bagian kanan dari lingkaran besar
// Center lingkaran di luar viewport kiri
const R = 900; // radius
const centerX = -R + 120; // pusat lingkaran di sebelah kiri
const centerY = viewportH / 2;

// Sudut arc yang visible: dari -50° sampai +50°
const arcStart = -Math.PI * 0.28; // atas
const arcEnd   =  Math.PI * 0.28; // bawah

// Posisi item ke-i (0-indexed) pada progress scroll t (0→1):
// t dikontrol GSAP ScrollTrigger scrub
function getItemState(itemIndex, scrollT) {
  const n = 5; // total items
  const spacing = (arcEnd - arcStart) / (n - 1);

  // Offset scroll mendorong semua item bergerak
  const scrollOffset = scrollT * (arcEnd - arcStart);

  const angle = arcStart + (itemIndex * spacing) - scrollOffset;

  const x = centerX + R * Math.cos(angle);
  const y = centerY + R * Math.sin(angle);

  // Sudut tangen = tegak lurus terhadap radius
  const tangentDeg = (angle * 180 / Math.PI) + 90;

  // Opacity berdasarkan jarak dari center (angle ≈ 0)
  const distFromCenter = Math.abs(angle);
  const opacity = Math.max(0, 1 - distFromCenter * 2.2);

  return { x, y, tangentDeg, opacity };
}
```

### Scroll Setup

```js
// Section di-pin selama 5 × 100vh
gsap.to(scrollProxy, {
  val: 1,
  ease: 'none',
  scrollTrigger: {
    trigger: '#deployments',
    start: 'top top',
    end: '+=500%',
    scrub: 1.2,
    pin: true,
    onUpdate: (self) => updateArc(self.progress)
  }
});
```

### Update Loop

```js
function updateArc(t) {
  items.forEach((item, i) => {
    const { x, y, tangentDeg, opacity } = getItemState(i, t);
    item.style.transform = `translate(${x}px, ${y}px) rotate(${tangentDeg}deg)`;
    item.style.opacity = opacity;
  });

  // Tentukan item aktif (paling dekat center)
  const activeIndex = getActiveIndex(t);
  updateActiveCopy(activeIndex);
}
```

### Arc SVG

```html
<!-- Arc digambar sebagai SVG path, bukan border/div -->
<svg class="arc-spine" viewBox="0 0 1456 900" preserveAspectRatio="none">
  <path
    d="M 680,0 Q 400,450 680,900"
    fill="none"
    stroke="rgba(255,255,255,0.05)"
    stroke-width="1"
  />
</svg>
```

Arc bisa juga dikalkulasi dari arc math di atas dan dirender lewat `<path>` dengan arc commands (`A`).

### HTML Structure

```html
<section id="deployments">
  <svg class="arc-spine">...</svg>

  <!-- Panel kiri — fixed saat scroll -->
  <div class="deploy-left">
    <p class="section-label">Selected Deployment Environments</p>
    <h2 class="deploy-headline">Built for real-world environments where decisions matter.</h2>
    <div class="deploy-copy" id="deployCopy">
      <!-- copy aktif muncul di sini -->
    </div>
  </div>

  <!-- Arc items — posisi dikontrol JS -->
  <div class="arc-container">
    <div class="arc-item" data-index="0">
      <span class="arc-dot">·</span>
      <span class="arc-num">01</span>
      <span class="arc-category">Public Services</span>
      <span class="arc-region">Indonesia</span>
    </div>
    <!-- ... 4 item lainnya -->
  </div>
</section>
```

---

## Color System (Cogniti palette)

| Elemen | Value |
|---|---|
| Background | `#0A0A0A` |
| Arc line | `rgba(255,255,255,0.05)` |
| Arc dot (•) | `#2A2A2A` → `#555` saat aktif |
| Item number | `#2A2A2A` → `#888` saat aktif |
| Category name | `#555` → `#D0D0D0` saat aktif |
| Region tag | `#2A2A2A` |
| Left panel headline | `#D0D0D0` |
| Active copy text | `#555` |

---

## Perbedaan dari Referensi WOVE

| Aspek | WOVE (referensi) | Cogniti (adaptasi) |
|---|---|---|
| Background | Light gray | `#0A0A0A` dark |
| Font | Bold, rounded | Inter weight 300 |
| Drive | Navigation overlay (click) | Scroll-driven (GSAP scrub) |
| Content | Product features | Deployment sectors |
| Copy | Subtitle singkat di arc | Copy panjang muncul di panel kiri |
| Arc color | Dark line on light | Very subtle white on dark |

---

## Estimasi Kompleksitas

**Kompleksitas:** Tinggi — tertinggi dari semua section sejauh ini  
**Komponen utama:**
1. Arc math (trigonometri — satu kali, bisa distatic-kan)
2. GSAP ScrollTrigger scrub + pin
3. Real-time position + rotation update per item
4. Active copy panel (fade in/out)
5. SVG arc path yang match dengan item positions

**Tidak memerlukan:**
- Three.js (pure CSS/JS)
- Canvas
- Library tambahan di luar GSAP

---

## Catatan

- Copy "Communities" perlu ditinjau — terasa NGO, perlu reframing ke B2B language
- Foto/screenshot tidak dipakai (sesuai Rules)
- Section ini menggantikan "Approach" section dari plan awal
