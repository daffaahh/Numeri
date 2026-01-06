# 📋 RENCANA PENGEMBANGAN LEVEL 2 TINGKAT 4
**Game NUMERI - Navigasi Arah & Pola**

---

## 🎯 KONSEP LEVEL

**Tema:** Ikuti Pola Arah - "Ayo Ikuti Pola Yang Aku Buat!"  
**Target Pembelajaran:** Memahami konsep arah (depan, belakang, kiri, kanan) berdasarkan orientasi karakter  
**Format:** Klik/Tap Quiz - Tebak arah yang ditunjukkan maskot  
**Durasi:** ⏱️ **ADA TIMER** - 2 menit (02:00 countdown)

### Visual Design (Berdasarkan Screenshot)
- **Setting:** Ruang kelas dengan maskot Numi di tengah
- **Maskot:** Numi menghadap ke arah tertentu (depan/belakang/kiri/kanan)
- **Panel Info:** Di kanan layar ada panel kecil "Sekarang Aku Menghadap [Arah]"
- **Tombol Arah:** 4 tombol di bagian bawah layar dengan icon panah + label
  - 🔴 **Belakang** - Panah ke bawah (merah)
  - 🟢 **Kanan** - Panah ke kanan (hijau)
  - 🟡 **Kiri** - Panah ke kiri (kuning)
  - 🔵 **Depan** - Panah ke atas (biru)
- **Timer:** Di kiri atas (02:00)
- **Feedback:** Notifikasi untuk benar/salah

---

## 📐 STRUKTUR LEVEL

### Layout Properties
- **Resolusi:** 2560 x 1440 px (large canvas untuk multiple screens)
- **Projection:** Perspective
- **Event Sheet:** ES_Level2_T4

### Layer Organization
1. **Layer "Dialog"** - Dialog intro + Screens + Pola buttons
2. **Layer "Notifications"** - Feedback popups
3. **Layer "Layer 0"** - Reserved
4. **Layer "Pola"** - Reserved untuk tombol arah

---

## ✅ STATUS PENGEMBANGAN

### SELESAI ✓

#### Komponen Wajib
- [x] Event Sheet (ES_Level2_T4.json) - **LENGKAP dengan 6 Group**
- [x] Layout (Lay_Level2_T4.json) - **SETUP LENGKAP**
- [x] Dialog (1 sprite)
- [x] Sistem Notifikasi (4 sprite)
- [x] Screen Pages (8 halaman)
- [x] Tombol Arah/Pola (4 tombol)

#### ASSETS - DIALOG (1 Item)
- [x] dialog_level_2_t4 (instruksi awal)

#### ASSETS - NOTIFICATIONS (4 Items)
- [x] jikaBenar_level_2_t4 (correct answer feedback)
- [x] jikaSalah_level_2_t4 (wrong answer feedback)  
- [x] finish_level_2_t4 (level complete screen) - **Fade behavior disabled**
- [x] motivasi_level_2_t4 (motivation message)

#### ASSETS - POLA/ARAH (4 Items)
- [x] depan_level_2_t4 (tombol arah depan/forward)
- [x] belakang_level_2_t4 (tombol arah belakang/backward)
- [x] kiri_level_2_t4 (tombol arah kiri/left)
- [x] kanan_level_2_t4 (tombol arah kanan/right)

#### ASSETS - SCREEN PAGES (8 Items)
- [x] screenpage1_level_2_t4 (halaman intro)
- [x] screenpage2_level_2_t4 (halaman soal 1 - jawaban: DEPAN)
- [x] screenpage3_level_2_t4 (halaman soal 2 - jawaban: KANAN)
- [x] screenpage4_level_2_t4 (halaman soal 3 - jawaban: DEPAN)
- [x] screenpage5_level_2_t4 (halaman soal 4 - jawaban: KANAN)
- [x] screenpage6_level_2_t4 (halaman soal 5 - jawaban: DEPAN)
- [x] screenpage7_level_2_t4 (halaman soal 6 - jawaban: KANAN)
- [x] screenpage8_level_2_t4 (halaman soal 7 - jawaban: DEPAN)

#### EVENT SHEET LOGIC (100%) ✅
- [x] **Group 1: System Initialization** - Hide semua, show dialog
- [x] **Group 2: Dialog Flow** - Klik dialog → show screenpage1 (intro) dengan introShown flag
- [x] **Group 3: Answer Validation** - 5 Events:
  - EVENT A: Klik screenpage1 → mulai game (show screenpage2)
  - EVENT B: Klik DEPAN → cek jawaban (benar di screen 2,4,6,8)
  - EVENT C: Klik KANAN → cek jawaban (benar di screen 3,5,7)
  - EVENT D: Klik BELAKANG → selalu salah
  - EVENT E: Klik KIRI → selalu salah
- [x] **Group 4: Timer System** - Countdown setiap detik
- [x] **Group 5: Win Condition** - Klik finish → go to Lay_RoadMap (dengan is-visible check)
- [x] **Group 6: Notifications Management** - Auto-hide dengan trigger-once

---

### BELUM SELESAI ⏳

#### Polish & Enhancement
- [ ] **Sound Effects** - Tambah suara untuk benar/salah
- [ ] **Animations** - Tambah animasi feedback
- [ ] **Lose Condition** - Timer habis → show gagal (optional)
- [ ] **motivasi_level_2_t4** - Belum digunakan dalam flow saat ini

---

## 🎮 GAMEPLAY MECHANIC

### Flow Permainan
1. **Start:**
   - Show dialog_level_2_t4 "AYO IKUTI POLA YANG AKU BUAT!"
   - Hide semua screen & notifications
   - Player klik dialog untuk mulai
   - **Start Timer** (02:00 = 120 detik)

2. **Quiz Flow (Per Screen):**
   - Show screenpage[N] dengan maskot Numi menghadap ke arah tertentu
   - Show instruksi "Ayo, lihat aku ya!"
   - Show panel info "Sekarang Aku Menghadap [Arah]"
   - Show 4 tombol arah di bawah
   - Player klik tombol arah yang sesuai
   - Validasi jawaban:
     * **Benar:** Show jikaBenar → Next screen
     * **Salah:** Show jikaSalah → Bisa retry

3. **Screen Progression:**
   - Screen 1 → Screen 2 → ... → Screen 8
   - Setiap screen: Numi menghadap ke arah berbeda
   - Progress tracking: currentScreen = 1-8

4. **Win Condition:**
   - Semua 8 soal dijawab benar SEBELUM waktu habis
   - Show finish_level_2_t4
   - Show motivasi_level_2_t4
   - Go to RoadMap

5. **Lose Condition (NEW):**
   - Timer mencapai 00:00
   - Show notifikasi gagal
   - Retry atau kembali ke RoadMap

### Interaksi yang Dibutuhkan
- **Click Detection** - Untuk memilih arah
- **Answer Validation** - Untuk cek benar/salah
- **Screen Management** - Show/hide screens
- **State Management** - Track screen ke berapa
- **Notification System** - Feedback visual
- **Timer System** - Countdown 2 menit ⏱️

---

## 🔧 EVENT SHEET - YANG PERLU DIBUAT

### 1. Variables
```javascript
// Event Variables (IMPLEMENTED)
currentScreen = 1        // Screen saat ini (1-8)
totalScreens = 8         // Total screen
correctAnswers = 0       // Jumlah jawaban benar
gameActive = 0           // Status game berjalan (0=false, 1=true)
timer = 120              // Timer dalam detik (2 menit)
notifShowing = 0         // Status notifikasi sedang tampil
introShown = 0           // Flag untuk mencegah skip intro

// Jawaban Benar Per Screen (CONFIRMED):
// Screen 1 = INTRO (klik untuk mulai)
// Screen 2 = DEPAN ✅
// Screen 3 = KANAN ✅
// Screen 4 = DEPAN ✅
// Screen 5 = KANAN ✅
// Screen 6 = DEPAN ✅
// Screen 7 = KANAN ✅
// Screen 8 = DEPAN ✅
```

### 2. System Initialization
```
On Start of Layout:
  - Set currentScreen = 1
  - Set correctAnswers = 0
  - Set gameActive = false
  - Show dialog_level_2_t4
  - Hide ALL screenpage (1-8)
  - Hide ALL notifications
  - Hide tombol arah (depan, belakang, kiri, kanan)
```

### 3. Dialog Flow
```
On Click dialog_level_2_t4:
  - Hide dialog_level_2_t4
  - Set gameActive = true
  - Call ShowScreen(1)
```

### 4. Screen Display Function
```
Function: ShowScreen(screenNumber)
  - Hide semua screenpage
  - Show screenpage[screenNumber]
  - Show tombol arah (4 buttons)
  - Position tombol di tempat yang sama
```

### 5. Answer Validation
```
On Click depan_level_2_t4:
  If gameActive = true:
    - Call CheckAnswer("depan")

On Click belakang_level_2_t4:
  If gameActive = true:
    - Call CheckAnswer("belakang")

On Click kiri_level_2_t4:
  If gameActive = true:
    - Call CheckAnswer("kiri")

On Click kanan_level_2_t4:
  If gameActive = true:
    - Call CheckAnswer("kanan")

Function: CheckAnswer(selectedAnswer)
  - Get correctAnswer untuk currentScreen
  - If selectedAnswer = correctAnswer:
      - Show jikaBenar_level_2_t4
      - Wait 1 second
      - Hide jikaBenar_level_2_t4
      - correctAnswers++
      - currentScreen++
      - If currentScreen > 8:
          - Call WinGame()
      - Else:
          - Call ShowScreen(currentScreen)
  - Else:
      - Show jikaSalah_level_2_t4
      - Wait 1 second
      - Hide jikaSalah_level_2_t4
      - (Optional: retry atau lanjut)
```

### 6. Win Condition
```
Function: WinGame()
  - Set gameActive = false
  - Hide semua screenpage
  - Hide tombol arah
  - Show finish_level_2_t4
  - Wait 2 seconds
  - Show motivasi_level_2_t4
  - Wait 2 seconds
  - Go to Lay_RoadMap
```

---

## 📊 MAPPING JAWABAN (CONFIRMED ✅)

Setiap screen menunjukkan maskot Numi menghadap ke arah tertentu. Player harus menebak arah yang benar.

| Screen | Posisi Numi | Panel Info | Jawaban Benar |
|--------|-------------|------------|---------------|
| 1 | INTRO - Instruksi awal | "Ayo, lihat aku ya!" | 🎮 **KLIK UNTUK MULAI** |
| 2 | Numi menghadap DEPAN | "Sekarang Aku Menghadap Depan" | 🔵 **DEPAN** |
| 3 | Numi menghadap KANAN | "Sekarang Aku Menghadap Kanan" | 🟢 **KANAN** |
| 4 | Numi menghadap DEPAN | "Sekarang Aku Menghadap Depan" | 🔵 **DEPAN** |
| 5 | Numi menghadap KANAN | "Sekarang Aku Menghadap Kanan" | 🟢 **KANAN** |
| 6 | Numi menghadap DEPAN | "Sekarang Aku Menghadap Depan" | 🔵 **DEPAN** |
| 7 | Numi menghadap KANAN | "Sekarang Aku Menghadap Kanan" | 🟢 **KANAN** |
| 8 | Numi menghadap DEPAN | Final challenge | 🔵 **DEPAN** |

### 🎯 Tombol Arah & Handler:
```
┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐
│     →       │ │     ←       │ │     ↑       │ │     ↓       │
│   Kanan     │ │    Kiri     │ │   Depan     │ │  Belakang   │
│   (hijau)   │ │  (kuning)   │ │   (biru)    │ │   (merah)   │
│  EVENT C ✅  │ │  EVENT E ✅  │ │  EVENT B ✅  │ │  EVENT D ✅  │
│ Benar:3,5,7 │ │ Selalu Salah│ │Benar:2,4,6,8│ │ Selalu Salah│
└─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘
```

**✅ SEMUA TOMBOL SUDAH DIIMPLEMENTASI**

---

## 📐 POSISI ASSETS (Dari Layout)

### Dialog & Notifications (Layer: Dialog)
| Object | Position (X, Y) | Size (W × H) |
|--------|-----------------|--------------|
| dialog_level_2_t4 | 640, 364.5 | 1266 × 707 |
| jikaBenar_level_2_t4 | -512, 517 | 286 × 174 |
| jikaSalah_level_2_t4 | -545, 707 | 286 × 174 |
| finish_level_2_t4 | -512, 303 | 286 × 174 |
| motivasi_level_2_t4 | -543, 965 | 286 × 174 |

### Tombol Arah/Pola
| Object | Position (X, Y) | Size (W × H) |
|--------|-----------------|--------------|
| kanan_level_2_t4 | -572, -225 | 187 × 197 |
| kiri_level_2_t4 | -243, -211 | 187 × 203 |
| belakang_level_2_t4 | -894, -223 | 227 × 208 |
| depan_level_2_t4 | 100, -222 | 187 × 207 |

### Screen Pages
| Object | Position (X, Y) | Size |
|--------|-----------------|------|
| screenpage1 | -498, 1968 | 1266 × 707 |
| screenpage2 | 947, 1944 | 1266 × 707 |
| screenpage3 | 2452, 1940 | 1266 × 707 |
| screenpage4 | -303, -982 | 1266 × 707 |
| screenpage5 | 2864, -1007 | 1266 × 707 |
| screenpage6 | 1302, -978 | 1266 × 707 |
| screenpage7 | 3561, 623 | 1266 × 707 |
| screenpage8 | 3979, 1971 | 1266 × 707 |

**⚠️ CATATAN:** Screen pages tersebar di berbagai posisi. Perlu dipertimbangkan:
1. **Opsi A:** Pindahkan semua ke posisi yang sama, show/hide bergantian
2. **Opsi B:** Scroll/pan camera ke setiap screen
3. **Opsi C:** Biarkan posisi, set visibility per screen

---

## 📝 CHECKLIST TAHAP PENGEMBANGAN

### FASE 1: Setup & Analysis ✅ COMPLETE
- [x] Identifikasi assets yang ada
- [x] Dokumentasi struktur layout
- [x] Analisis visual setiap screenpage
- [x] Tentukan jawaban benar per screen
- [x] Decide strategi screen management (show/hide)

### FASE 2: Basic Logic ✅ COMPLETE
- [x] Implement System Initialization
- [x] Implement Dialog Flow (dengan introShown flag)
- [x] Implement Screen Navigation
- [x] Test screen switching

### FASE 3: Answer System ✅ COMPLETE
- [x] Implement Click handlers untuk 4 tombol (EVENT B,C,D,E)
- [x] Implement Answer Validation
- [x] Implement Feedback notifications (jikaBenar 1.5s, jikaSalah)
- [x] Test benar/salah flow

### FASE 4: Win & Navigation ✅ COMPLETE
- [x] Implement Win Condition (click finish → RoadMap)
- [x] Implement RoadMap navigation
- [x] Test complete flow
- [x] Fix finish_level_2_t4 visibility (disable Fade behavior)

### FASE 5: Polish ⏳ OPTIONAL
- [ ] Add animations
- [ ] Add sound effects
- [ ] Implement lose condition (timer habis)
- [ ] Final testing

---

## 🔄 GAME FLOW DIAGRAM

```
[START]
   ↓
[Show Dialog - "AYO IKUTI POLA YANG AKU BUAT!"]
   ↓
[Klik Dialog]
   ↓
[Start Timer 02:00] ←──────────────────────┐
   ↓                                        │
[Show Screen N + Numi menghadap arah]       │
   ↓                                        │
[Show Panel "Sekarang Aku Menghadap..."]    │
   ↓                                        │
[Show 4 Tombol: Kanan|Kiri|Depan|Belakang]  │
   ↓                                        │
[Player Klik Tombol Arah]                   │
   ↓                                        │
   ├── Benar → [Show jikaBenar] ────────────┤
   │              ↓                         │
   │     [currentScreen++]                  │
   │              ↓                         │
   │     [Screen > 8?] ──YES──→ [WIN!]      │
   │              │                         │
   │             NO                         │
   │              ↓                         │
   │     [Show Next Screen] ────────────────┘
   │
   └── Salah → [Show jikaSalah] → [Retry same screen]
   
[PARALLEL: Timer Countdown]
   ↓
[Timer = 0?] ──YES──→ [LOSE - Waktu Habis]
                              ↓
                      [Show Gagal]
                              ↓
                      [Go to RoadMap]

[WIN FLOW]
   ↓
[Hide Screen & Buttons]
   ↓
[Show finish_level_2_t4]
   ↓
[Show motivasi_level_2_t4]
   ↓
[Go to RoadMap]
```

---

## 💡 PERBEDAAN DENGAN LEVEL LAIN

| Level | Mekanik | Interaksi | Objective |
|-------|---------|-----------|-----------|
| T1 | Drag & Drop | Sorting | Kelompokkan bentuk |
| T2 | Click Quiz | Recognition | Pilih bentuk yang benar |
| T3 | Drag & Drop | Assembly | Susun rumah |
| **T4** | **Click Quiz** | **Navigation** | **Pilih arah yang benar** |

---

## 🎯 PRIORITAS KERJA

### IMMEDIATE:
1. **Analisis Visual Screenpage** - Lihat gambar tiap screen
2. **Tentukan Jawaban** - Mapping jawaban benar per screen
3. **Implement Event Sheet** - Logika dasar

### NEXT:
4. Polish posisi tombol arah
5. Test complete flow
6. Integrasi dengan RoadMap

---

## 📊 PROGRESS METER

```
┌────────────────────────────────────────────────────────┐
│ LEVEL 2 TINGKAT 4 - Navigasi Arah                      │
├────────────────────────────────────────────────────────┤
│                                                        │
│ Assets & Sprites     ████████████████████████  100%   │
│ Layout Setup         ████████████████████████  100%   │
│ Event Sheet Logic    ████████████████████████  100%   │
│ Answer Mapping       ████████████████████████  100%   │
│ Win Condition        ████████████████████████  100%   │
│ Polish & Animation   ░░░░░░░░░░░░░░░░░░░░░░░░   0%    │
│                                                        │
│ ──────────────────────────────────────────────────     │
│ TOTAL PROGRESS: ≈ 85% (Core Gameplay Complete)         │
└────────────────────────────────────────────────────────┘
```

---

## 📌 CATATAN PENTING

✅ **SUDAH SELESAI:**
- Event Sheet LENGKAP dengan 6 Groups
- Semua 4 tombol arah sudah ada handler (DEPAN, KANAN, BELAKANG, KIRI)
- **Timer 2 menit** sudah diimplementasi
- Jawaban benar sudah di-mapping: DEPAN (screen 2,4,6,8), KANAN (screen 3,5,7)
- BELAKANG & KIRI selalu salah
- jikaBenar tampil 1.5 detik sebelum pindah screen
- finish_level_2_t4 tampil setelah screen 8 dan navigasi ke RoadMap

⚠️ **PERLU DIPERHATIKAN:**
- Fade behavior pada finish_level_2_t4 sudah di-disable di layout
- introShown flag mencegah skip intro (screenpage1)
- is-visible check pada finish click event mencegah navigasi tidak sengaja

✨ **OPTIONAL ENHANCEMENT:**
- Tambah sound effects untuk feedback benar/salah
- Tambah animasi (shake untuk salah, bounce untuk benar)
- Implement lose condition jika timer habis
- Gunakan motivasi_level_2_t4 untuk pesan motivasi

🎨 **VISUAL DARI SCREENSHOT:**
- **Dialog:** Papan tulis dengan tulisan "AYO IKUTI POLA YANG AKU BUAT!"
- **Maskot Numi:** Karakter perempuan berhijab pink dengan baju kuning
- **Panel Info:** Kotak putih di kanan dengan gambar Numi kecil + teks arah
- **Tombol Arah:** 4 tombol warna-warni dengan panah:
  - Kanan (hijau) → | Kiri (kuning) ← | Depan (biru) ↑ | Belakang (merah) ↓
- **Timer:** Di pojok kiri atas "02:00"

---

**Dibuat:** 3 Januari 2026  
**Last Update:** 6 Januari 2026 - Core Gameplay Complete  
**Status:** ✅ FASE 4 COMPLETE - Core Gameplay Done  
**Developer:** Tim NUMERI
**Commits:** `5a81322`, `1390d7b`

---

## 📚 REFERENSI ASSETS

```
objectTypes/Level_2_T4/
├── Dialog/
│   └── dialog_level_2_t4.json
├── Notifications/
│   ├── finish_level_2_t4.json
│   ├── jikaBenar_level_2_t4.json
│   ├── jikaSalah_level_2_t4.json
│   └── motivasi_level_2_t4.json
├── Pola/
│   ├── belakang_level_2_t4.json
│   ├── depan_level_2_t4.json
│   ├── kanan_level_2_t4.json
│   └── kiri_level_2_t4.json
└── Screen/
    ├── screenpage1_level_2_t4.json
    ├── screenpage2_level_2_t4.json
    ├── screenpage3_level_2_t4.json
    ├── screenpage4_level_2_t4.json
    ├── screenpage5_level_2_t4.json
    ├── screenpage6_level_2_t4.json
    ├── screenpage7_level_2_t4.json
    └── screenpage8_level_2_t4.json
```

**Total Assets:** 17 sprites
- Dialog: 1
- Notifications: 4
- Pola/Arah: 4
- Screen Pages: 8
