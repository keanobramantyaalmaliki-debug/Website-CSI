# Revisi Konten Web — dari `revisi content web.pdf`

> Revisi dari atasan. Sumber: `revisi content web.pdf` (9 halaman).
> Dirangkum 2026-06-29. Tanda: ✅ sudah dikerjakan · ⏳ belum · ❓ perlu diskusi.

---

## Ringkasan arah besar

Revisi ini menggeser positioning dari **abstrak/misterius** ("Intelligence Infrastructure", sengaja tanpa daftar layanan, gaya McKinsey/Stripe) → menjadi **company profile eksplisit**: ada daftar layanan, industri yang dilayani, proses kerja, serta visi & misi. Lebih jelas "perusahaannya ngapain".

Implikasi struktur: muncul beberapa section baru (Our Services, Why Choose Cogniti, Our Development Process, Industries We Serve, Vision & Mission, closing CTA) dan beberapa headline existing diganti.

---

## Halaman 1 — Hero + CTA + catatan Founder

### Slogan (ganti) ✅
- **Dari:** "We build the infrastructure that thinks."
- **Jadi:** **Think Beyond Software. Build Intelligence.**

### Subtext (ganti) ✅
> We build intelligent digital solutions that help businesses, enterprises, and governments innovate, automate, and grow.
>
> At Cogniti, we believe software should do more than function, it should create value, simplify complexity, and empower organizations to make smarter decisions.

> Catatan: di PDF kalimat terpotong di "...make smarter". Dilengkapi jadi "...make smarter **decisions.**" (disetujui).

### Call to Action — 2 tombol ⏳ ❓
- **Start Your Project**
- **Book a Free Consultation**

> ❓ Posisi belum disepakati: di Hero (bawah subtext) atau di section CTA bawah? Hero saat ini cuma punya 1 link teks "Explore our thinking".

### Founder achievement → pindah ke akhir ✅
- Slide founder (Award + Speaking) ditandai **"slide ini di akhir aja"**.
- Sudah dipindah: Founder kini setelah Careers, sebelum CTA. (Lihat juga hal. 9 — diperjelas jadi "lowongan dan award".)

---

## Halaman 2 — Deployments headline + Our Services (baru)

### Headline "Built for real-world..." (ganti) ⏳
- **Dari:** "Built for real-world environments where decisions matter."
- **Jadi:** **Building Intelligent Digital Solutions**
- Paragraf pendamping:
  > Cogniti is a technology company specializing in custom software development, digital transformation, and Artificial Intelligence solutions. We partner with businesses, startups, enterprises, and public institutions to design and develop innovative software that solves real-world challenges.

### Our Services (section baru) ✅
Daftar layanan (judul + deskripsi):
1. **Custom Software Development** — Tailor-made software designed around your unique business processes, helping you improve productivity, streamline operations, and support long-term growth.
2. **Web Application Development** — Modern, responsive, and secure web applications built with performance, scalability, and user experience in mind.
3. **Mobile App Development** — Native and cross-platform mobile applications for Android and iOS that deliver seamless user experiences.
4. **Artificial Intelligence Solutions** — Leverage AI to automate workflows, enhance customer engagement, analyze data, and unlock new business opportunities through intelligent digital solutions.
   - AI services include: **Jenna.ai**, **Knowledge Assistants**, **Process Automation**, **AI-Powered Analytics**, **Custom AI Integration**
5. **Enterprise Solutions** — Develop enterprise-grade platforms that integrate departments, automate operations, and improve decision-making across your organization. *(hal. 3)*
6. **System Integration** — Connect existing applications, third-party services, and business systems through secure and reliable API integrations. *(hal. 3)*
7. **UI/UX Design** — Create intuitive and engaging digital experiences through user-centered interface and experience design. *(hal. 3)*
8. **Cloud & DevOps** — Deploy, monitor, and optimize applications with modern cloud infrastructure and DevOps best practices for maximum reliability and scalability. *(hal. 3)*
9. **Maintenance & Technical Support** — Ensure your applications remain secure, updated, and optimized with continuous support and proactive maintenance. *(hal. 3)*

> ✅ Diputuskan: dibuat section baru murni `#services` (setelah Deployments, sebelum Living Architecture). Layout = **3D conveyor / rotating bookshelf** (CSS 3D `preserve-3d` + drag, bukan grid kartu statis). Front face = nomor + judul; tap kartu yang di tengah → flip 180° menampilkan deskripsi di belakang (no-redundancy). Kartu #4 (AI) flip ke 5 sub-item. Mobile: 3D di-skip, ganti list bertumpuk yang legible.

---

## Halaman 3 — lanjutan Our Services
(Sudah digabung ke daftar hal. 2 di atas: Enterprise Solutions, System Integration, UI/UX Design, Cloud & DevOps, Maintenance & Technical Support.)

---

## Halaman 4 — Living Architecture → Why Choose Cogniti

### Headline (ganti) ⏳
- **Dari:** "A Living Architecture For Decisions."
- **Jadi:** **Why Choose Cogniti?**

### Subtext lama (hapus) ⏳
- Hapus "We connect signals, context, knowledge, and workflows into adaptive systems that help organizations move from awareness to action."

### Node graph → ganti jadi daftar alasan ⏳ ❓
"bulet2 ini ganti dengan" (mengganti 7 node Citizen/Operations/dst):
1. **Intelligent by Design** — We build software with intelligence at its core—combining automation, data, and AI to create smarter digital experiences.
2. **Business-Driven Solutions** — Technology should solve business problems. Every solution we build is aligned with your goals, processes, and long-term strategy.
3. **Scalable Architecture** — Our systems are designed to grow with your business, allowing future expansion without costly redevelopment.
4. **Security First** — We implement industry best practices to ensure your applications are secure, reliable, and compliant. *(hal. 5)*
5. **Agile Development** — Using agile methodologies, we deliver projects faster while maintaining flexibility, transparency, and quality throughout the development process. *(hal. 5)*
6. **Long-Term Partnership** — We don't just deliver software—we become your technology partner, supporting continuous innovation and business growth. *(hal. 5)*

> ❓ Nasib visual 3D node graph (centerpiece interaktif) belum diputuskan: dibuang, dipindah ke section lain (mis. Our Development Process), atau dipertahankan dengan konten baru. "Diskusi dulu."

---

## Halaman 5 — lanjutan Why Choose Cogniti
(Sudah digabung ke hal. 4: Security First, Agile Development, Long-Term Partnership.)

---

## Halaman 6 — Our Development Process (section baru) ✅

"tambahkan 1 page lagi" — proses kerja 6 langkah:
1. **Discovery** — Understanding your business, objectives, and technical requirements.
2. **Strategy & Planning** — Defining the project roadmap, architecture, technology stack, and development timeline.
3. **Design** — Creating intuitive UI/UX experiences that maximize usability and engagement.
4. **Development** — Building scalable, secure, and high-performance software using modern technologies.
5. **Testing & Quality Assurance** — Conducting comprehensive testing to ensure functionality, security, performance, and reliability.
6. **Deployment & Continuous Support** — Launching your product, then providing ongoing monitoring, maintenance, and continuous improvement. *(deskripsi dilengkapi sendiri — tidak ada di PDF)*

> ✅ Implementasi (`#process`, setelah Living Architecture): sticky cinematic split — kolom kiri = 6 langkah ber-nomor yang menyala saat scroll, kolom kanan sticky = motif canvas generatif berbeda per tahap (Discovery/Plan/Shape/Build/Verify/Launch). Tiap motif rAF-nya di-gate IntersectionObserver.
> ✅ Visual 3D node graph TIDAK jadi dipindah ke sini — node graph tetap di Living Architecture (sebagai "Why cogniti?"), Process pakai motif canvas sendiri.

---

## Halaman 7 — Careers tetap + Industries We Serve (baru)

### Careers ✅ (tetap)
- Headline "Build What Comes Next." tetap.
- Role tetap: Innovation & Growth Manager, Technical Lead, Product Builder, Full Stack Engineer.

### Industries We Serve (section baru) ✅
> We develop intelligent digital solutions across various industries:

Government & Public Sector · Smart Cities · Digital Villages · Healthcare · Education · Finance · Hospitality · Retail & E-Commerce · Manufacturing · Logistics · Property & Real Estate · Professional Services · Startups & Enterprises

> ✅ Implementasi (`#industries`, setelah Careers, sebelum Vision): **dual-row marquee**. 13 sektor dibagi 2 baris bergerak berlawanan arah (baris 1 ke kiri, baris 2 ke kanan), digerakkan per-frame via `translateX` (rAF di-gate IntersectionObserver). Hover memperlambat (factor 1→0.18, tidak berhenti total), ada edge-fade di kedua tepi, hormati `prefers-reduced-motion`.
> ✅ Visual arc Deployments TIDAK jadi dipindah ke sini — Deployments tetap dengan arc-nya.

---

## Halaman 8 — Vision & Mission (section baru) ✅

> ✅ Implementasi (`#vision`, setelah Industries, sebelum CTA): **editorial split**. Kolom kiri = Our Vision (sticky), kolom kanan = Our Mission sebagai daftar ber-nomor 01–05 dengan reveal bertahap saat scroll. Mobile: single-column, vision di-unstick.

### Our Vision
> To become a trusted technology partner that empowers organizations through intelligent digital innovation, creating sustainable value for businesses and communities worldwide.

### Our Mission
- Deliver innovative and high-quality software solutions.
- Accelerate digital transformation through intelligent technologies.
- Integrate Artificial Intelligence into practical business applications.
- Build long-term partnerships based on trust, collaboration, and excellence.
- Continuously innovate to help organizations thrive in the digital era.

---

## Halaman 9 — Closing CTA + urutan akhir

### Let's Build the Future Together (closing, baru) ⏳
> Technology is evolving rapidly, and organizations need more than software, they need intelligent solutions that adapt, scale, and create lasting value.
>
> At Cogniti, we combine innovation, engineering excellence, and Artificial Intelligence to help businesses transform ideas into impactful digital products.
>
> **Ready to build your next digital solution?**
> Let's create something intelligent together.

### Urutan akhir halaman ⏳ ❓
- "page selanjutnya baru lowongan dan award yg didapat"
- Artinya: setelah closing CTA → **Careers (lowongan)** → **Award (achievement founder)** di paling akhir.

> ❓ Perlu konfirmasi urutan final keseluruhan section (lihat usulan di bawah).

---

## Usulan urutan section baru (perlu disepakati) ❓

| # | Section | Status |
|---|---|---|
| 1 | Hero (slogan + subtext + 2 CTA) | slogan/subtext ✅, CTA ⏳ |
| 2 | Manifesto | tetap |
| 3 | Building Intelligent Digital Solutions (intro company) | ⏳ |
| 4 | Our Services | ✅ (3D conveyor) |
| 5 | Why Choose Cogniti? | ⏳ (headline masih "Why cogniti?") |
| 6 | Our Development Process | ✅ (sticky split + motif canvas) |
| 7 | Industries We Serve | ✅ (dual-row marquee) |
| 8 | Vision & Mission | ✅ (editorial split) |
| 9 | Let's Build the Future Together (closing CTA) | ⏳ |
| 10 | Careers (lowongan) | tetap, pindah ke akhir |
| 11 | Awards (achievement founder) | ✅ dipindah ke akhir |
| 12 | Footer | tetap |

---

## Pertanyaan terbuka yang perlu diputuskan

1. **Posisi 2 tombol CTA** (Hero vs section bawah)? — ⏳ masih terbuka.
2. ~~**Nasib visual 3D node graph** (Living Architecture)~~ — ✅ diputuskan **dipertahankan** di Living Architecture; Process pakai motif canvas terpisah.
3. ~~**Nasib visual arc** (Deployments)~~ — ✅ diputuskan **dipertahankan** di Deployments; Industries pakai marquee terpisah.
4. ~~**Our Services & Industries** — layout~~ — ✅ diputuskan: Services = 3D conveyor, Industries = dual-row marquee; daftar layanan eksplisit **disetujui** (mengganti keputusan desain lama).
5. **Urutan final** semua section. — ⏳ sebagian: Vision & closing CTA belum di urutan akhir sesuai usulan; Founder/Award section saat ini sudah dihapus dari HTML (foto founder dihapus).
6. ~~Deskripsi **"Deployment & Continuous Support"**~~ — ✅ dilengkapi sendiri (lihat hal. 6).
