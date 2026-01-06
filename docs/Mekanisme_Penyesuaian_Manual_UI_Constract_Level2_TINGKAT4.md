# 🛠️ Mekanisme Penyesuaian Manual UI - Level 2 Tingkat 4
**Panduan Setup Layout di Construct 3**

---

## 📋 OVERVIEW

Level 2 T4 memiliki **17 assets** yang tersebar di layout. Sebelum implementasi Event Sheet, perlu dilakukan penyesuaian posisi UI secara manual di Construct 3.

### Masalah Saat Ini:
- Screen pages (8 halaman) posisinya tersebar di berbagai koordinat
- Tombol arah belum diposisikan dengan benar
- Notifications berada di luar viewport

### Target:
- Semua screen pages di posisi yang sama (center viewport)
- Tombol arah di posisi tetap (bawah layar)
- Notifications di tengah layar saat muncul

---

## 🎯 LANGKAH 1: Setup Instance Variables & Behaviors (PERTAMA!)

### A. Screen Pages - Instance Variables

Setiap **screenpage** perlu instance variable untuk menyimpan jawaban yang benar.

**Cara di Construct 3:**
1. Di Project Bar, expand **objectTypes/Level_2_T4/Screen/**
2. Double-click **screenpage1_level_2_t4**
3. Di panel kanan, klik **"Add/edit"** pada Instance Variables
4. Tambahkan variable baru:

| Variable Name | Type | Initial Value | Description |
|---------------|------|---------------|-------------|
| `correctAnswer` | **String** | (lihat tabel) | Jawaban yang benar untuk screen ini |

**Nilai correctAnswer per Screen:**

| Object | correctAnswer | Keterangan |
|--------|---------------|------------|
| screenpage1_level_2_t4 | `""` | Intro/instruksi (tidak perlu jawaban) |
| screenpage2_level_2_t4 | `"depan"` | Numi menghadap depan |
| screenpage3_level_2_t4 | `"kanan"` | Numi menghadap kanan |
| screenpage4_level_2_t4 | `"???"` | ⚠️ Cek visual |
| screenpage5_level_2_t4 | `"???"` | ⚠️ Cek visual |
| screenpage6_level_2_t4 | `"???"` | ⚠️ Cek visual |
| screenpage7_level_2_t4 | `"???"` | ⚠️ Cek visual |
| screenpage8_level_2_t4 | `"???"` | ⚠️ Cek visual (silhouette) |

**Ulangi untuk semua 8 screenpage!**

---

### B. Tombol Arah (Pola) - Instance Variables

Setiap **tombol arah** perlu instance variable untuk identifikasi.

**Cara di Construct 3:**
1. Di Project Bar, expand **objectTypes/Level_2_T4/Pola/**
2. Double-click **kanan_level_2_t4**
3. Tambahkan Instance Variable:

| Variable Name | Type | Initial Value | Description |
|---------------|------|---------------|-------------|
| `direction` | **String** | (lihat tabel) | Arah yang diwakili tombol |

**Nilai direction per Tombol:**

| Object | direction | Warna |
|--------|-----------|-------|
| kanan_level_2_t4 | `"kanan"` | Hijau → |
| kiri_level_2_t4 | `"kiri"` | Kuning ← |
| depan_level_2_t4 | `"depan"` | Biru ↑ |
| belakang_level_2_t4 | `"belakang"` | Merah ↓ |

---

### C. Behaviors (Opsional)

Untuk Level 2 T4, **tidak perlu behaviors khusus** karena:
- ❌ Tidak ada Drag & Drop (beda dengan T1 & T3)
- ❌ Tidak perlu BoundToLayout
- ✅ Hanya perlu Click detection (sudah ada dari Mouse plugin)

**Behaviors yang MUNGKIN berguna (opsional):**

| Object | Behavior | Fungsi |
|--------|----------|--------|
| Tombol Arah | **Button** | Untuk hover effect & click state |
| Notifications | **Fade** | Untuk animasi fade in/out |
| Notifications | **Tween** | Untuk animasi scale/move |

**Cara tambah Behavior:**
1. Select object di layout
2. Di panel kanan, klik **"Add/edit"** pada Behaviors
3. Pilih behavior yang diinginkan
4. Klik Add

---

### D. Checklist Instance Variables

#### Screen Pages:
- [ ] screenpage1 → correctAnswer: `""`
- [ ] screenpage2 → correctAnswer: `"depan"`
- [ ] screenpage3 → correctAnswer: `"kanan"`
- [ ] screenpage4 → correctAnswer: `"???"`
- [ ] screenpage5 → correctAnswer: `"???"`
- [ ] screenpage6 → correctAnswer: `"???"`
- [ ] screenpage7 → correctAnswer: `"???"`
- [ ] screenpage8 → correctAnswer: `"???"`

#### Tombol Arah:
- [ ] kanan → direction: `"kanan"`
- [ ] kiri → direction: `"kiri"`
- [ ] depan → direction: `"depan"`
- [ ] belakang → direction: `"belakang"`

---

## 🎯 LANGKAH 2: Pahami Struktur Layout

### Viewport Game:
```
Resolusi: 1280 × 720 px (atau sesuai project)
Center: X = 640, Y = 360
```

### Layer Structure:
| Layer | Isi | Fungsi |
|-------|-----|--------|
| Dialog | Screens, Dialog, Pola buttons | Konten utama |
| Notifications | Feedback popups | Overlay notifikasi |
| Layer 0 | (Reserved) | Background |
| Pola | (Reserved) | Tombol arah |

---

## 🎯 LANGKAH 2: Penyesuaian Screen Pages

### Kondisi Saat Ini (dari Layout JSON):
Screen pages tersebar di berbagai posisi:
```
screenpage1: (-498, 1968)   ← Jauh di luar viewport!
screenpage2: (947, 1944)
screenpage3: (2452, 1940)
screenpage4: (-303, -982)
... dst
```

### Yang Harus Dilakukan di Construct 3:

#### Opsi A: Pindahkan Semua ke Center (RECOMMENDED)
1. Buka **Lay_Level2_T4** di Construct 3
2. Select **screenpage1_level_2_t4**
3. Di Properties panel, set:
   - **X:** 640 (center horizontal)
   - **Y:** 360 (center vertical)
4. Ulangi untuk screenpage2 - screenpage8
5. Set **Initially Visible:** ❌ No (kecuali screen 1)

```
Target Posisi Semua Screen:
┌─────────────────────────────────────┐
│           Viewport 1280×720         │
│                                     │
│     ┌───────────────────────┐       │
│     │                       │       │
│     │    Screen Page N      │       │
│     │    (640, 360)         │       │
│     │    1266 × 707         │       │
│     │                       │       │
│     └───────────────────────┘       │
│                                     │
└─────────────────────────────────────┘
```

#### Opsi B: Biarkan Posisi, Gunakan Scroll To
- Tidak perlu pindah posisi
- Camera akan scroll ke setiap screen
- Lebih kompleks di Event Sheet

**➡️ REKOMENDASI: Gunakan Opsi A (lebih simpel)**

---

## 🎯 LANGKAH 3: Penyesuaian Tombol Arah (Pola)

### Kondisi Saat Ini:
Tombol arah posisinya negatif (di luar viewport):
```
kanan_level_2_t4:    (-572, -225)
kiri_level_2_t4:     (-243, -211)
belakang_level_2_t4: (-894, -223)
depan_level_2_t4:    (100, -222)
```

### Target Posisi (Berdasarkan Screenshot):
Tombol arah seharusnya di **bawah layar**, berjejer horizontal:

```
┌─────────────────────────────────────┐
│           Viewport 1280×720         │
│                                     │
│         [Screen Content]            │
│                                     │
│  ┌───────┐┌───────┐┌───────┐┌───────┐
│  │ Kanan ││ Kiri  ││ Depan ││Belakang│
│  │  →    ││   ←   ││   ↑   ││   ↓   │
│  └───────┘└───────┘└───────┘└───────┘
│     X≈250    X≈450    X≈650    X≈850  
│              Y ≈ 650 (semua)         
└─────────────────────────────────────┘
```

### Yang Harus Dilakukan di Construct 3:

1. Select **kanan_level_2_t4**
   - Set X: **250**
   - Set Y: **650**

2. Select **kiri_level_2_t4**
   - Set X: **450**
   - Set Y: **650**

3. Select **depan_level_2_t4**
   - Set X: **650**
   - Set Y: **650**

4. Select **belakang_level_2_t4**
   - Set X: **850**
   - Set Y: **650**

5. Set semua **Initially Visible:** ❌ No

---

## 🎯 LANGKAH 4: Penyesuaian Notifications

### Kondisi Saat Ini:
Notifications berada di koordinat negatif:
```
jikaBenar_level_2_t4:  (-512, 517)
jikaSalah_level_2_t4:  (-545, 707)
finish_level_2_t4:     (-512, 303)
motivasi_level_2_t4:   (-543, 965)
```

### Target Posisi:
Semua notifications harus di **tengah viewport** saat muncul:

```
Target: X = 640, Y = 360 (center)
Size: 286 × 174 px
```

### Yang Harus Dilakukan di Construct 3:

1. Select **jikaBenar_level_2_t4**
   - Set X: **640**, Y: **360**
   - Set Initially Visible: ❌ No

2. Select **jikaSalah_level_2_t4**
   - Set X: **640**, Y: **360**
   - Set Initially Visible: ❌ No

3. Select **finish_level_2_t4**
   - Set X: **640**, Y: **360**
   - Set Initially Visible: ❌ No

4. Select **motivasi_level_2_t4**
   - Set X: **640**, Y: **360**
   - Set Initially Visible: ❌ No

---

## 🎯 LANGKAH 5: Penyesuaian Dialog

### Kondisi Saat Ini:
```
dialog_level_2_t4: (640, 364.5) ✅ Sudah benar!
```

### Yang Harus Dilakukan:
- ✅ Posisi sudah benar (center)
- Set **Initially Visible:** ✅ Yes (muncul pertama)

---

## 📋 CHECKLIST PENYESUAIAN

### Screen Pages:
- [ ] screenpage1 → (640, 360), Visible: Yes
- [ ] screenpage2 → (640, 360), Visible: No
- [ ] screenpage3 → (640, 360), Visible: No
- [ ] screenpage4 → (640, 360), Visible: No
- [ ] screenpage5 → (640, 360), Visible: No
- [ ] screenpage6 → (640, 360), Visible: No
- [ ] screenpage7 → (640, 360), Visible: No
- [ ] screenpage8 → (640, 360), Visible: No

### Tombol Arah:
- [ ] kanan → (250, 650), Visible: No
- [ ] kiri → (450, 650), Visible: No
- [ ] depan → (650, 650), Visible: No
- [ ] belakang → (850, 650), Visible: No

### Notifications:
- [ ] jikaBenar → (640, 360), Visible: No
- [ ] jikaSalah → (640, 360), Visible: No
- [ ] finish → (640, 360), Visible: No
- [ ] motivasi → (640, 360), Visible: No

### Dialog:
- [ ] dialog → (640, 364.5), Visible: Yes ✅

---

## 🔄 FLOW SETELAH PENYESUAIAN

```
[Layout Start]
     │
     ▼
┌─────────────────┐
│ dialog VISIBLE  │  ← "AYO IKUTI POLA YANG AKU BUAT!"
│ screens HIDDEN  │
│ buttons HIDDEN  │
│ notif HIDDEN    │
└─────────────────┘
     │
     ▼ (Klik Dialog)
┌─────────────────┐
│ dialog HIDDEN   │
│ screen1 VISIBLE │  ← Numi muncul
│ buttons VISIBLE │  ← 4 tombol arah muncul
│ notif HIDDEN    │
└─────────────────┘
     │
     ▼ (Klik Tombol)
┌─────────────────┐
│ Cek Jawaban     │
│ Benar → notif   │
│ Salah → notif   │
└─────────────────┘
     │
     ▼ (Next Screen atau Win)
```

---

## ⚠️ CATATAN PENTING

1. **Backup Dulu!**
   - Sebelum edit, pastikan sudah commit/backup project

2. **Viewport vs Layout Size**
   - Layout size: 2560 × 1440 (besar)
   - Viewport: 1280 × 720 (yang terlihat)
   - Posisikan semua di area viewport!

3. **Z-Order**
   - Pastikan notifications di atas screens
   - Dialog di paling atas saat muncul

4. **Initially Visible**
   - Hanya dialog yang visible di awal
   - Semua lainnya di-hide, akan di-show via Event Sheet

---

## 📅 UPDATE LOG

| Tanggal | Aktivitas | Status |
|---------|-----------|--------|
| 3 Jan 2026 | Dokumentasi mekanisme | ✅ |
| - | Penyesuaian screens | ⏳ |
| - | Penyesuaian buttons | ⏳ |
| - | Penyesuaian notifications | ⏳ |
| - | Testing layout | ⏳ |

---

**Dibuat:** 3 Januari 2026  
**Untuk:** Level 2 Tingkat 4 - Pola Arah  
**Developer:** Tim NUMERI
