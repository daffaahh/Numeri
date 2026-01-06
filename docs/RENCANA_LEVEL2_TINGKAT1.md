# 📋 RENCANA PENGEMBANGAN LEVEL 2 TINGKAT 1
**Game NUMERI - Pengenalan Bentuk Geometri**

---

## 🎯 KONSEP LEVEL

**Tema:** Tata Kelas Antariksa - Mengelompokkan Bentuk Geometri  
**Target Pembelajaran:** Mengenali dan mengelompokkan benda-benda berdasarkan bentuk geometri dasar  
**Durasi:** 02:00 (2 menit per sesi)

### Visual Design (Berdasarkan Gambar)
- Setting: Ruang kelas dengan papan tulis bertuliskan "TATA KELAS ANTARIKSA"
- Background: Kelas dengan meja-meja, tanaman, jam dinding, dan dekorasi antariksa
- Timer: Ditampilkan di kiri atas (02:00)
- Layout: 3 kotak penampung di bagian bawah, objek tersebar di ruang kelas

---

## 📐 STRUKTUR LEVEL

### Layout Properties
- **Resolusi:** 2560 x 1440 px
- **Projection:** Perspective
- **Event Sheet:** ES_Level2_T1

### Layer Organization
1. **Layer 0** (Background)
   - Background kelas (bg_level2_t1)
   - Frame penuh (full_level2_t1)
   - Judul level (judul_level2_t1)

2. **Notifications** (Feedback Layer)
   - Pop-up berhasil
   - Pop-up gagal
   - Pop-up info/instruksi

3. **Items_Group_1** (Objek yang bisa di-drag - Group 1)
   - 9 objek berbentuk lingkaran, persegi, segitiga
   - Tersebar di area kelas

4. **Hamper** (Zona Drop - Kotak Penampung)
   - 3 kotak penampung untuk setiap bentuk
   - Posisi tetap di bawah

5. **Time** (Timer Display)
   - Container waktu
   - Display angka countdown

---

## ✅ STATUS PENGEMBANGAN

### SELESAI ✓ (Commit: feat/Level2_T1_Group1)

#### Komponen Wajib
- [x] Event Sheet (ES_Level2_T1.json) - **KOSONG, perlu isi logika**
- [x] Layout (Lay_Level2_T1.json) - **SUDAH SETUP**
- [x] Background & Frame
- [x] Judul level
- [x] Sistem Notifikasi (3 sprite)
- [x] Sistem Timer (2 sprite)

#### GROUP 1: Bentuk Dasar (Lingkaran, Persegi, Segitiga)

**Hamper - 3 Kotak:**
- [x] kotak_lingkaran_t1 (327x314 px)
- [x] kotak_persegi_t1 (327x314 px)
- [x] kotak_segitiga_t1 (327x314 px)

**Items Lingkaran - 3 Objek:**
- [x] ling_bola_level2_t1 (184x184 px)
- [x] ling_cermin_level2_t1 (184x184 px)
- [x] ling_jam_level2_t1 (184x184 px)

**Items Persegi - 3 Objek:**
- [x] persegi_buku_level2_t1 (140x140 px)
- [x] persegi_jendela_level2_t1 (140x140 px)
- [x] persegi_whiteboard_level2_t1 (140x140 px)

**Items Segitiga - 3 Objek:**
- [x] segitiga_level2_t1 (140x140 px)
- [x] segitiga_penggariskuning_level2_t1 (120x120 px)
- [x] segitiga_penggarispink_level2_t1 (140x140 px)

---

### PENDING ⏳ (Belum di-commit)

#### GROUP 2: Segi Empat Kompleks
**Hamper - 3 Kotak:**
- [ ] belah_ketupat_t1
- [ ] persegi_panjang_t1
- [ ] trapesium_t1

**Items:**
- [ ] Perlu dibuat objek-objek yang berbentuk belah ketupat
- [ ] Perlu dibuat objek-objek yang berbentuk persegi panjang
- [ ] Perlu dibuat objek-objek yang berbentuk trapesium
- [ ] Masing-masing bentuk minimal 3 objek

#### GROUP 3: Bentuk Kompleks
**Hamper - 3 Kotak:**
- [ ] jajar_t1 (jajar genjang)
- [ ] layang_t1 (layang-layang)
- [ ] segilima_t1

**Items:**
- [ ] Perlu dibuat objek-objek yang berbentuk jajar genjang
- [ ] Perlu dibuat objek-objek yang berbentuk layang-layang
- [ ] Perlu dibuat objek-objek yang berbentuk segilima
- [ ] Masing-masing bentuk minimal 3 objek

---

## 🎮 GAMEPLAY MECHANIC

### Flow Permainan
1. **Start:**
   - Tampilkan pop-up info dengan instruksi
   - Timer mulai countdown dari 02:00
   - Semua objek tersebar random di kelas

2. **Gameplay:**
   - Player drag objek ke kotak yang sesuai
   - Validasi: Cek apakah bentuk cocok dengan kotak
   - Feedback: Tampilkan notifikasi berhasil/gagal

3. **Win Condition:**
   - Semua objek berhasil dikelompokkan dengan benar
   - Sebelum waktu habis
   - Tampilkan pop-up berhasil

4. **Lose Condition:**
   - Waktu habis sebelum selesai
   - Tampilkan pop-up gagal

### Interaksi yang Dibutuhkan
- **Drag & Drop** - Untuk memindahkan objek
- **Collision Detection** - Untuk deteksi objek masuk kotak
- **Shape Validation** - Untuk cek kecocokan bentuk
- **Timer Countdown** - Untuk batasan waktu
- **Score/Progress Tracking** - Untuk monitor kemajuan

---

## 🔧 EVENT SHEET - YANG PERLU DIBUAT

### 1. System Events
```
On Start of Layout:
  - Show info_level2_t1
  - Initialize timer = 120 (2 menit)
  - Randomize posisi items
  - Set initial score = 0
```

### 2. Drag & Drop Mechanics
```
On Item touched:
  - Enable drag mode
  
On Item dropped:
  - Check collision with hamper
  - If collision:
      - Validate bentuk
      - If correct:
          - Lock item di hamper
          - Add score
          - Show berhasil notification (brief)
      - Else:
          - Return to original position
          - Show gagal notification (brief)
```

### 3. Shape Validation Logic
```
Function: ValidateBentuk(item, hamper)
  - If item contains "ling" AND hamper = "kotak_lingkaran":
      Return TRUE
  - If item contains "persegi" AND hamper = "kotak_persegi":
      Return TRUE
  - If item contains "segitiga" AND hamper = "kotak_segitiga":
      Return TRUE
  - Else:
      Return FALSE
```

### 4. Timer System
```
Every 1 second:
  - Subtract 1 from timer
  - Update waktu_level2 display
  
If timer = 0:
  - Stop game
  - Show gagal_level2_t1
  - Wait 2 seconds
  - Go to RoadMap layout
```

### 5. Win Condition
```
On score = total_items:
  - Stop timer
  - Show berhasil_level2_t1
  - Wait 3 seconds
  - Go to Lay_Level2_T2 (Quiz level)
```

### 6. Notification Management
```
Function: ShowNotification(type)
  - Hide all notifications
  - Show notification[type]
  - Set opacity to 0
  - Tween: Fade in (0.3s)
  - Wait 1.5 seconds
  - Tween: Fade out (0.3s)
```

---

## 📊 VARIABLES YANG DIBUTUHKAN

### Layout Variables (Local)
```javascript
timer = 120                  // 2 menit dalam detik
score = 0                    // Jumlah objek yang benar
totalItems_Group1 = 9        // Total objek Group 1
totalItems_Group2 = 9        // Total objek Group 2 (nanti)
totalItems_Group3 = 9        // Total objek Group 3 (nanti)
currentGroup = 1             // Group mana yang aktif
gameActive = false           // Status game
levelCompleted = false       // Track completion status (local only)
```

**⚠️ CATATAN:** Tidak menggunakan Global Variables - semua variabel bersifat lokal per layout.

---

## 🎨 VISUAL FEEDBACK

### Animasi yang Direkomendasikan
1. **Item Hover:** Scale 1.1x saat mouse hover
2. **Item Drag:** Sedikit transparansi (opacity 0.8)
3. **Correct Drop:** Tween smooth ke posisi final + particle effect
4. **Wrong Drop:** Shake animation + return to origin
5. **Notifications:** Fade in/out dengan scale bounce
6. **Timer Warning:** Blink merah saat < 30 detik

---

## 📝 CHECKLIST TAHAP PENGEMBANGAN

### FASE 1: Group 1 - Basic Shapes 🔄
- [x] Setup layout & layers
- [x] Import semua assets Group 1
- [x] Posisikan objek di layout
- [x] **Setup Behaviors (DragDrop + BoundToLayout) - Step 1** ✓
- [x] **Setup Instance Variables (bentuk + bentukYangDiterima) - Step 2** ✓
- [x] **Setup Layout Variables & On Start Event - Step 3** ✓
- [x] **Implement timer countdown - Step 4** ✓
- [x] **Implement drag & drop event logic - Step 5** ✓
- [x] **Implement score system & item management - Step 6** ✓
- [x] **Implement win/lose conditions & wrong drop feedback - Step 7** ✓
- [x] **Testing & debugging** ✓ - **TESTED & WORKING!** 🎮
- [x] **Navigation update: T1 → T2 → T3** ✓ (30 Des 2025)

### FASE 2: Group 2 - Complex Quadrilaterals (NEXT)
- [ ] Buat hamper untuk 3 bentuk baru
- [ ] Buat 9 items berbentuk belah ketupat, persegi panjang, trapesium
- [ ] Import assets
- [ ] Update validation logic
- [ ] Testing

### FASE 3: Group 3 - Advanced Shapes
- [ ] Buat hamper untuk 3 bentuk kompleks
- [ ] Buat 9 items berbentuk jajar genjang, layang-layang, segilima
- [ ] Import assets
- [ ] Update validation logic
- [ ] Testing

### FASE 4: Polish & Integration
- [ ] Add sound effects (success, fail, timer)
- [ ] Add background music
- [ ] Add particle effects
- [ ] Optimize performance
- [ ] Final testing semua groups
- [ ] Integration dengan RoadMap

---

## 🎯 PRIORITAS KERJA IMMEDIATE

### URGENT - Perlu Dikerjakan Sekarang:
1. ~~**Implementasi Event Sheet ES_Level2_T1**~~ ⚠️ ✅ DONE (Step 5-7)
   - ~~Step 4-7: Timer countdown, drag & drop, validation, win/lose~~
   - ~~Ini blocker untuk gameplay~~

2. ~~**Tambahkan Behaviors ke Items:**~~ ✓ DONE (Commit: c07e771)
   - ~~Drag & Drop behavior~~
   - ~~Bound to Layout behavior~~

3. ~~**Tambahkan Instance Variables:**~~ ✓ DONE (Commit: c07e771)
   - ~~Setiap item perlu variable "bentuk" (lingkaran/persegi/segitiga)~~
   - ~~Setiap hamper perlu variable "bentukYangDiterima"~~

4. ~~**Setup Layout Variables & System Events:**~~ ✓ DONE (Commit: 7748300)
   - ~~4 Layout variables (timer, score, totalItems, gameActive)~~
   - ~~On Start of Layout event~~
   - ~~Timer Countdown event~~

---

## ✅ IMPLEMENTATION LOG - FASE 1

### **Commit c07e771** (Step 1 & 2):
- ✅ Tambahkan DragDrop + BoundToLayout behaviors pada 9 items
- ✅ Tambahkan instance variable `bentuk` pada semua items
- ✅ Tambahkan instance variable `bentukYangDiterima` pada 3 hampers

### **Commit 7748300** (Step 3 & 4):
- ✅ Layout Variables: timer (120), score (0), totalItems (9), gameActive (0)
- ✅ Event: On Start of Layout - initialize game, show info popup
- ✅ Event: On Any Click (info visible) - hide popup, start game
- ✅ Event: Every 1 second (gameActive = 1) - countdown timer, update display
- ✅ Sub-event: If timer <= 0 - stop game, show gagal popup, go to RoadMap
- ✅ Created: waktu_text_level2 text object for timer display

### **Commit f58c41b** (Step 5):
- ✅ **Step 5:** Drag & Drop Events untuk 9 items (WITHOUT SCORE)
  - 3 Groups untuk organisasi event yang rapih:
    * Group "Drag & Drop - Persegi" (3 events)
    * Group "Drag & Drop - Segitiga" (3 events)
    * Group "Drag & Drop - Lingkaran" (3 events)
  - Event per item:
    * Condition 1: On Drop (behavior DragDrop)
    * Condition 2: Is overlapping hamper yang sesuai
    * Action: Set enabled → disabled (item stuck, tidak bisa di-drag lagi)
  - Validasi via collision detection:
    * persegi items (jendela, buku, whiteboard) → kotak_persegi_t1
    * segitiga items (segitiga, penggaris kuning, penggaris pink) → kotak_segitiga_t1
    * lingkaran items (bola, cermin, jam) → kotak_lingkaran_t1

**Total Events Created:** 9 events dalam 3 Groups
**Files Modified:** ES_Level2_T1.json

### **NEXT COMMIT** (Step 6 - B, C, D):
- ✅ **Step 6B:** Save Initial Positions (18 actions added to On Start event)
  - Setiap item (9 total) menyimpan posisi awal:
    * Set X_origin = Self.X
    * Set Y_origin = Self.Y
  - Digunakan untuk return to origin saat wrong drop

- ✅ **Step 6C:** Update Correct Drop Events (9 events modified)
  - Tambah 2 actions per event:
    * Add to eventvar score → value: 1
    * Destroy (item hilang setelah drop benar)
  - Existing action dipertahankan: Set enabled disabled

- ✅ **Step 6D:** Wrong Drop Events (9 new events created)
  - Event untuk setiap item:
    * Condition 1: On Drop
    * Condition 2: (INVERTED) Is overlapping hamper yang benar
    * Action: Set position to (Self.X_origin, Self.Y_origin)
  - Ditambahkan di dalam group yang sama dengan correct drop

**Total Events Now:** 27 events (3 system + 18 drag drop + 6 placeholder for win/lose)
**Score System:** Internal tracking (tidak ditampilkan ke user)
**Files Modified:** ES_Level2_T1.json
**Status:** Ready for Step 7 (Win/Lose Conditions)

### **Commit 2f36153** (Step 7 - E, F, G):
- ✅ **Step 7E:** Win Condition Event (NEW EVENT)
  - Event baru (sid: 234567890123506)
  - Condition: Compare eventvar score = totalItems (9)
  - Actions:
    * Set gameActive = 0
    * Set visible berhasil_level2_t1 = visible
    * Wait 3 seconds
    * Go to layout **Lay_Level2_T2** (✅ Updated 30 Des 2025)
  - **Purpose:** Mengakhiri game dengan feedback positif saat semua item benar

- ✅ **Step 7F:** Lose Condition Sub-event (TIMER TIMEOUT)
  - Sub-event baru (sid: 234567890123500) di bawah timer countdown
  - Parent Event: Every 1 second (gameActive = 1)
  - Condition: Compare eventvar timer <= 0
  - Actions:
    * Set gameActive = 0
    * Set visible info_level2_t1 = invisible
    * Set visible gagal_level2_t1 = visible
    * Wait 2 seconds
    * Go to layout Lay_RoadMap
  - **Purpose:** Mengakhiri game dengan feedback negatif saat waktu habis

- ✅ **Step 7G:** Wrong Drop Feedback (INSTANT NOTIFICATION)
  - **Modified:** Semua 9 wrong drop events (dari Step 6D)
  - **Added 27 actions total** (3 actions × 9 events):
    * Set visible gagal_level2_t1 = visible
    * Wait 0.5 seconds
    * Set visible gagal_level2_t1 = invisible
    * (existing) Set position to origin
  - **Purpose:** Memberikan feedback visual instant kepada pemain saat salah drop
  - **UX Improvement:** Pemain langsung tahu kesalahannya tanpa bingung

**Gameplay Flow Lengkap:**
1. Start → Info popup muncul
2. Click → gameActive=1, timer countdown dimulai
3. Drag & Drop:
   - ✅ Benar: score+1, item hilang (destroy)
   - ❌ Salah: notif gagal 0.5s, item kembali ke posisi awal
4. Kondisi Akhir:
   - 🏆 Menang (score=9): Notif berhasil → Wait 3s → RoadMap
   - ⏰ Kalah (timer=0): Notif gagal → Wait 2s → RoadMap

**Total Events Now:** 29 events (3 system + 18 drag drop + 2 win/lose)
**Total Actions:** 127+ (termasuk 27 actions untuk notifikasi gagal sementara)
**Files Modified:** ES_Level2_T1.json (329 insertions, 1 deletion)
**Status:** ✅ STEP 7 COMPLETE - Full gameplay loop implemented!

### MEDIUM - Bisa Nanti:
1. Buat Group 2 & 3 items
2. Polish visual & animations
3. Sound design

---

## 🔄 GAME FLOW DIAGRAM

```
[START]
   ↓
[Show Info Popup] → Player baca instruksi
   ↓
[Click to Start]
   ↓
[Timer Starts: 2:00]
   ↓
[Player Drag Items] ←→ [Drop to Hamper]
   ↓                        ↓
   ├── Correct → [Score++] → [Check Win]
   │                              ↓
   │                         All Done? → [WIN!]
   │                              ↓
   └── Wrong → [Shake & Return]  No
                    ↓
            [Continue Playing]
                    ↓
            [Timer = 0?] → [LOSE]
```

---

## 📚 REFERENSI NAMING CONVENTION

### Pattern Items:
- `{bentuk}_{namaObjek}_level2_t1`
- Contoh: `ling_bola_level2_t1`, `persegi_buku_level2_t1`

### Pattern Hamper:
- `kotak_{bentuk}_t1`
- Contoh: `kotak_lingkaran_t1`

### Pattern Notifications:
- `{status}_level2_t1`
- Contoh: `berhasil_level2_t1`, `gagal_level2_t1`

---

## 🚀 NEXT STEPS

1. **SEKARANG:** Implementasi logika game di `ES_Level2_T1.json`
2. **MINGGU DEPAN:** Testing Group 1 sampai perfect
3. **SETELAH ITU:** Commit Group 2 dengan struktur yang sama
4. **TERAKHIR:** Commit Group 3 dan final polish

---

## 📌 CATATAN PENTING

⚠️ **JANGAN LUPA:**
- Event Sheet masih kosong, ini prioritas #1
- **TIDAK menggunakan Global Variables** - semua lokal per layout
- Setiap kali menambah group baru, update validation logic
- Test di berbagai resolusi
- Pastikan timer visible dan mudah dibaca
- Notifikasi jangan terlalu lama (max 2 detik)

✨ **TIPS DEVELOPMENT:**
- Gunakan Family untuk grouping items dengan behavior sama
- Buat function reusable untuk validation
- Comment code dengan baik
- Test setiap feature sebelum lanjut ke berikutnya
ber 2025  
**Last Update:** 30 Desember 2025 - Navigation Updated (T1 → T2 → T3)
**Status:** ✅ FASE 1 COMPLETE & INTEGRATED - Full Level Progression Chain
**Developer:** Tim NUMERI

---

## 🎉 MILESTONE: GAMEPLAY LOGIC COMPLETE!

**Commit 2f36153** menandai completion dari **core gameplay logic** Level 2 Tingkat 1!

✅ **Semua Feature Implemented:**
- Drag & Drop Mechanic (9 items)
- Collision Detection & Validation (correct/wrong drop)
- Score Tracking System (internal)
- Timer Countdown (120 seconds)
- Position Memory (return to origin)
- Win Condition (all items sorted)
- Lose Condition (timeout)
- Visual Feedback (instant notification)
- Navigation Flow (✅ T1 → T2 → T3 progression)

🎮 **Game Loop:**
```
Start → Info → Click → Play (Drag/Drop) → Win/Lose → Next Level/RoadMap
```

**Navigation Chain (30 Des 2025):**
- ✅ **Level 2 T1** (Grouping) → berhasil → **Level 2 T2** (Quiz)
- ✅ **Level 2 T2** (Quiz) → berhasil → **Level 2 T3** (Assembly)
- ⚠️ Gagal (timeout) → RoadMap (retry dari map)

📊 **Statistics:**
- Total Events: 29
- Total Actions: 127+
- Lines of Code (JSON): 1000+
- Commits: 5 (c07e771, 7748300, f58c41b, 5aff638, 2f36153)
- **Navigation Update:** 30 Des 2025 (ES_Level2_T1.json modified)

🔜 **Next Phase:** Testing Full T1 → T2 → T3 Progression
