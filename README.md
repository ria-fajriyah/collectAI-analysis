# CollectAI — AI Agent Initiative for Multifinance Collection

## 📌 Summary

**CollectAI** adalah inisiatif AI Agent yang dirancang untuk mengoptimalkan proses *collection* (penagihan) pada perusahaan multifinance melalui *behavioural intelligence*, *predictive recovery scoring*, dan rekomendasi *Next Best Action (NBA)* bagi field collector maupun supervisor.

Proyek ini merepresentasikan hasil kerja **business & systems analysis**, mencakup:
- Analisis masalah bisnis (problem background & opportunities)
- Desain proses bisnis (business process flow & decision rules)
- Desain solusi sistem (module navigation flow, wireframe/mockup UI)
- Dokumentasi pitch/initiative untuk stakeholder (COI Season 2 – Spark Phase)

## 🎯 Problem Background Analysis

Proses collection di multifinance konvensional menghadapi beberapa tantangan:
- Biaya collection tinggi (15–25% dari OPEX)
- Prioritas penagihan & assignment collector masih bersifat *rule-based* statis
- Data historis LKP (Lembar Kerja Penugasan), aktivitas collection, dan hasil kunjungan harian belum dimanfaatkan secara optimal
- Treatment/penanganan nasabah masih bersifat *one-size-fits-all*, berisiko terhadap kepatuhan regulasi (POJK No. 22/POJK.04/2023)

## 💡 Proposed Solution

CollectAI menganalisis histori LKP, pola pembayaran, dan outcome collection untuk:
1. **Mengklasifikasikan nasabah** ke dalam segmen risiko: *Self-Cure, Can Pay, Cannot Pay, Won't Pay*
2. **Menghasilkan Recovery Probability Score** secara prediktif
3. **Merekomendasikan Next Best Action** (WA reminder, deskcoll, visit, somasi, pickup unit, restrukturisasi) sesuai profil dan tingkat risiko nasabah
4. **Mendukung keputusan supervisor** melalui *AI Reasoning & Analysis* (LLM-generated insight) dan approval workflow untuk restrukturisasi

Sistem diposisikan sebagai **Decision Support System** yang memberi insight kepada collector — bukan menggantikan proses Core Collection yang sudah berjalan.

## 🧩 Document Analysis

| Dokumen | Deskripsi |
|---|---|
| [`pitch-deck/`](pitch-deck) | Deck inisiatif lengkap: problem background, opportunity, solution design, how-it-works, business value, roadmap, dan MVP scope |
| [`process-flow/business-process-flow.png`](process-flow/business-process-flow.png) | Activity diagram end-to-end: ML scoring → business rules (risk segmentation) → rekomendasi NBA → aksi collector/supervisor → integrasi Core Collection |
| [`process-flow/module-navigation-flow.png`](process-flow/module-navigation-flow.png) | Peta navigasi modul sistem: Dashboard, Customer, Contract, Restructuring Approval, AI Intelligence (Collector vs Supervisor workspace) |
| [`screenshots/`](screenshots) | Mockup UI aplikasi hasil desain: Dashboard, Customer List, Customer Detail (AI Reasoning), Contract List, Restructuring Approval, AI Intelligence Config |

## 🖥️ Main Module

- **Dashboard** — Consolidated view: total outstanding, active delinquent accounts, PTP keep rate, distribusi risk segment, DPD bucket vs PTP status
- **Customer** — Daftar nasabah dengan behavioral grade, B-list status, priority, dan filter (Critical Risk, Broken PTP, High Billing Amount)
- **Customer Detail — AI Reasoning & Analysis** — Narasi AI atas kondisi debitur, faktor kunci risiko, dan rekomendasi Next Best Action per kontrak
- **Contract** — Daftar kontrak dengan DPD, outstanding, dan risk segment (Can Pay / Cannot Pay / Won't Pay / Self-cure)
- **Restructuring Approval** — Antrian persetujuan supervisor untuk penawaran restrukturisasi (refinance) hasil rekomendasi AI
- **AI Intelligence Config** — Konfigurasi bobot scoring model (payment rate, PTP reliability, interaction, delay score) dan monitoring model health

## ⚙️ Business Rules

Segmentasi risiko nasabah ditentukan dari kombinasi *recovery score* dan indikator perilaku:

- **Won't Pay** — recovery score < 0.30 & (rejection count ≥ 2 atau hasil kontak = menolak/tidak bisa dihubungi) → NBA: Visit / Somasi / Pickup (berdasarkan total outstanding)
- **Cannot Pay** — skor 0.30–0.50 & (broken PTP > 0 atau income-debt ratio > 2.0) → NBA: Deskcoll / Visit & Negosiasi
- **Can Pay** — kondisi lainnya (skor ≥ 0.50) → NBA: WA / Deskcoll
- **Self-Cure** — skor ≥ 0.70 & DPD saat ini ≤ 7 & payment rate ≥ 0.80 → NBA: Reminder WA otomatis

Priority level ditentukan dari matriks *risk segment × total outstanding*. Untuk kasus yang membutuhkan restrukturisasi, sistem membedakan jalur **Auto** (tampil langsung ke nasabah) vs **Manual** (perlu approval supervisor).

## 🗺️ Roadmap Development

1. **Phase 1 – MVP Launch**: LKP predictive scoring & treatment recommendation, integrasi core system multifinance
2. **Phase 2 – Scale & Optimization**: treatment effectiveness analytics, adaptive learning dari historical outcome
3. **Phase 3 – Autonomous AI Agent**: automated next best action engine, restrukturisasi otomatis, predictive write-off

## 🛠️ Tools & Metodologi

- Diagram proses & flow: draw.io / Mermaid
- Dokumentasi inisiatif & pitch: PowerPoint
- Pendekatan analisis: problem-opportunity-solution framing, business process modeling (swimlane), rule-based decision table
