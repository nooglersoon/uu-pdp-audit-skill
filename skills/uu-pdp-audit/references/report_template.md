# Laporan Audit Kepatuhan UU PDP No. 27 Tahun 2022

> **Proyek / Aplikasi:** [Nama proyek atau repo]
> **Tanggal Audit:** [Tanggal]
> **Tech Stack:** [Contoh: NestJS 10, PostgreSQL 15, TypeORM]
> **Auditor:** Claude (UU PDP Audit Skill)
> **Metode:** [Inspeksi kode langsung / Deskripsi arsitektur]

---

## 📖 Panduan Membaca Laporan Ini

### Status Kepatuhan

| Simbol | Arti |
|--------|------|
| ✅ **Compliant** | Sudah diimplementasikan dengan benar — tidak perlu tindakan |
| ⚠️ **Partial** | Ada implementasi tapi belum lengkap atau masih ada celah |
| ❌ **Non-compliant** | Belum ada sama sekali, atau implementasi yang ada salah |
| ❓ **Unknown** | Tidak ditemukan / tidak disebutkan — perlu verifikasi manual ke codebase |

### Tingkat Prioritas

| Prioritas | Arti | Kapan Harus Ditangani |
|-----------|------|-----------------------|
| 🔴 **HIGH** | Risiko hukum langsung — potensi sanksi dari BPPA, atau pelanggaran hak dasar subjek data | Segera, sebelum go-live atau dalam 2 minggu |
| 🟡 **MEDIUM** | Penting untuk kepatuhan jangka panjang, tapi belum darurat | Dalam 30 hari |
| 🟢 **LOW** | Peningkatan kualitas — sudah ada tapi bisa diperkuat | Dalam 90 hari / backlog |

### Referensi Pasal UU PDP

| Pasal | Topik |
|-------|-------|
| Pasal 7 & 13 | Hak subjek data: akses dan portabilitas data |
| Pasal 15 & 40 | Hak menarik consent (consent withdrawal) |
| Pasal 16 | Minimisasi data, pembatasan tujuan, dan retensi data |
| Pasal 20 | Kewajiban memiliki dasar hukum pemrosesan (termasuk consent) |
| Pasal 21 | Consent harus dicatat dan dapat dibuktikan |
| Pasal 27 | Pembatasan tujuan pemrosesan data |
| Pasal 35 | Kewajiban notifikasi kebocoran data ke BPPA (maks. 14 hari) |
| Pasal 39 | Kewajiban keamanan teknis dan enkripsi |
| Pasal 40 | Kewajiban kontrol akses berbasis peran dan audit trail |
| Pasal 43 | Kewajiban retensi dan penghapusan data |

---

## Ringkasan Eksekutif

[2–3 kalimat: jenis aplikasi ini, data pribadi apa yang diproses, dan gambaran umum posisi kepatuhan saat ini.]

### Status Per Area

| Area | Status | Prioritas |
|------|--------|-----------|
| 1. Data Minimisation (Pasal 16) | ✅ / ⚠️ / ❌ / ❓ | 🔴 / 🟡 / 🟢 |
| 2. Explicit Consent (Pasal 20 & 21) | | |
| 3. Data Security & Encryption (Pasal 39) | | |
| 4. RBAC & Access Audit Trail (Pasal 40) | | |
| 5. Data Portability & IDOR (Pasal 7 & 13) | | |
| 6. Data Breach Response (Pasal 35) | | |
| 7. Data Deletion & Anonymisation (Pasal 16 & 43) | | |
| 8. Consent Withdrawal (Pasal 15 & 40) | | |
| 9. Purpose Limitation (Pasal 16 & 27) | | |
| 10. Data Retention Policy (Pasal 16 & 43) | | |

---

## Penilaian Keamanan Umum

### Yang Sudah Baik
- [Sebutkan praktik keamanan yang sudah benar]

### Masalah Ditemukan

| Severity | Masalah | Lokasi | Catatan |
|----------|---------|--------|---------|
| 🔴 HIGH | | | |
| 🟡 MED | | | |

---

## Detail Temuan UU PDP

### 1. Data Minimisation (Pasal 16)

**Status:** ✅ / ⚠️ / ❌ / ❓
**Prioritas:** 🔴 HIGH / 🟡 MEDIUM / 🟢 LOW

**Temuan:**
[Apa yang ditemukan di kode? Field apa yang ada? Apakah ada masking?]

**Bukti:**
```
File: src/users/user.entity.ts, baris 23
religion: string  // field berlebih, tidak digunakan di logika bisnis manapun
```

**Rekomendasi:**
[Apa yang perlu diubah — sertakan contoh kode sesuai stack pengguna.]

---

### 2. Explicit Consent (Pasal 20 & 21)

**Status:** ✅ / ⚠️ / ❌ / ❓  **Prioritas:** 🔴 / 🟡 / 🟢

**Temuan:** [...] **Bukti:** [...] **Rekomendasi:** [...]

---

### 3. Data Security & Encryption (Pasal 39)

**Status:** ✅ / ⚠️ / ❌ / ❓  **Prioritas:** 🔴 / 🟡 / 🟢

**Temuan:** [...] **Bukti:** [...] **Rekomendasi:** [...]

---

### 4. RBAC & Access Audit Trail (Pasal 40)

**Status:** ✅ / ⚠️ / ❌ / ❓  **Prioritas:** 🔴 / 🟡 / 🟢

**Temuan:** [...] **Bukti:** [...] **Rekomendasi:** [...]

---

### 5. Data Portability & IDOR Protection (Pasal 7 & 13)

**Status:** ✅ / ⚠️ / ❌ / ❓  **Prioritas:** 🔴 / 🟡 / 🟢

**Temuan:** [...] **Bukti:** [...] **Rekomendasi:** [...]

---

### 6. Data Breach Response (Pasal 35)

**Status:** ✅ / ⚠️ / ❌ / ❓  **Prioritas:** 🔴 / 🟡 / 🟢

**Temuan:** [...] **Bukti:** [...] **Rekomendasi:** [...]

---

### 7. Data Deletion & Anonymisation (Pasal 16 & 43)

**Status:** ✅ / ⚠️ / ❌ / ❓  **Prioritas:** 🔴 / 🟡 / 🟢

**Temuan:** [...] **Bukti:** [...] **Rekomendasi:** [...]

---

### 8. Consent Withdrawal (Pasal 15 & 40)

**Status:** ✅ / ⚠️ / ❌ / ❓  **Prioritas:** 🔴 / 🟡 / 🟢

**Temuan:** [...] **Bukti:** [...] **Rekomendasi:** [...]

---

### 9. Purpose Limitation (Pasal 16 & 27)

**Status:** ✅ / ⚠️ / ❌ / ❓  **Prioritas:** 🔴 / 🟡 / 🟢

**Temuan:** [...] **Bukti:** [...] **Rekomendasi:** [...]

---

### 10. Data Retention Policy (Pasal 16 & 43)

**Status:** ✅ / ⚠️ / ❌ / ❓  **Prioritas:** 🔴 / 🟡 / 🟢

**Temuan:** [...] **Bukti:** [...] **Rekomendasi:** [...]

---

## Rencana Tindakan Berdasarkan Prioritas

### 🔴 HIGH — Lakukan Segera (sebelum go-live atau dalam 2 minggu)

| # | Tindakan | Area | Pasal | Estimasi Waktu |
|---|----------|------|-------|----------------|
| 1 | | | | |

### 🟡 MEDIUM — Lakukan dalam 30 Hari

| # | Tindakan | Area | Pasal | Estimasi Waktu |
|---|----------|------|-------|----------------|
| 1 | | | | |

### 🟢 LOW — Backlog (dalam 90 hari)

| # | Tindakan | Area | Pasal | Estimasi Waktu |
|---|----------|------|-------|----------------|
| 1 | | | | |

---

## Catatan untuk Tim

[Konteks penting: apa yang sudah solid, area mana yang paling berisiko, nuansa hukum khusus untuk jenis aplikasi ini (pemerintah, kesehatan, data anak-anak, dll).]

---

*Laporan ini dihasilkan oleh analisis kode otomatis. Temuan berlabel ❓ harus diverifikasi secara manual. Laporan ini bukan merupakan pendapat hukum resmi — konsultasikan dengan konsultan hukum privasi data untuk keperluan kepatuhan formal.*
