# 📋 EVENT SHEET PLAN - LEVEL 2 TINGKAT 3
**Game Assembly: Menyusun Rumah dari Bentuk Geometri**

---

## 🎯 OVERVIEW

**Gameplay:** Drag & Drop 9 komponen rumah ke posisi yang benar  
**Win Condition:** Semua 9 komponen terpasang dengan benar  
**Event Sheet:** ES_Level2_T3.json  

---

## 📊 VARIABLES YANG DIBUTUHKAN

### Layout Variables (Local)
```javascript
componentsPlaced = 0       // Jumlah komponen yang sudah terpasang benar (number)
totalComponents = 9        // Total komponen rumah (number)
gameActive = false         // Status game sedang berjalan (boolean)
showReference = true       // Toggle tampilan referensi rumah (boolean)
currentHint = ""           // Hint saat ini untuk maskot (string)
```

### Instance Variables (Sudah Ada - Per Component)
✅ Sudah di-setup di semua 9 komponen:
- `componentType` (string) - Tipe komponen (dinding, pintu, dll)
- `X_origin` (number) - Posisi awal X untuk reset
- `Y_origin` (number) - Posisi awal Y untuk reset
- `X_target` (number) - Posisi target X yang benar
- `Y_target` (number) - Posisi target Y yang benar
- `isPlaced` (boolean) - Status sudah terpasang atau belum

---

## 🗂️ GROUP STRUCTURE

### GROUP 1: System Initialization
**Tujuan:** Setup awal layout, hide notifications, set initial state

**Events:**
1. **On Start of Layout**
   - Hide semua notifications (benar, berhasil, cobalagi, tap2_sering)
   - Hide rumahselesaidisusun_level_2_t3 (referensi - akan ditampilkan setelah dialog)
   - Show bg_level_2_t3
   - Show judul_level_2_t3
   - Show dialog_level_2_t3 (instruksi pembuka)
   - Show maskot (numa & numi)
   - Set componentsPlaced = 0
   - Set totalComponents = 9
   - Set gameActive = false
   - Set showReference = true

2. **Save Original Positions**
   - For each komponen (dinding, pintu, jendela, dll):
     - Set X_origin = Self.X
     - Set Y_origin = Self.Y
     - Set isPlaced = false
   - **Note:** Posisi target (X_target, Y_target) sudah di-set manual di layout

---

### GROUP 2: Game Start
**Tujuan:** Mulai game setelah dialog intro

**Events:**
1. **On Click Dialog (Start Game)**
   - Condition: Click/Touch pada dialog_level_2_t3
   - Actions:
     - Hide dialog_level_2_t3
     - Show rumahselesaidisusun_level_2_t3 (referensi rumah)
     - Set opacity rumahselesaidisusun = 50 (semi-transparent)
     - Set gameActive = true
     - Enable DragDrop untuk semua 9 komponen
     - Show hint pertama di maskot: "Mari kita bangun rumah! Lihat contohnya ya~"

---

### GROUP 3: Drag & Drop Mechanics
**Tujuan:** Handle drag & drop behavior untuk setiap komponen

**Sub-group: Komponen - dinding_level_2_t3**

1. **On Drag Start**
   - Condition: dinding_level_2_t3 - On drag start
   - Actions:
     - Bring to front (set Z-order to top)
     - Set opacity = 80 (semi-transparent saat di-drag)

2. **On Drop - Correct Position**
   - Conditions:
     - dinding_level_2_t3 - On drop
     - dinding_level_2_t3 - Is overlapping target_level_2_t3
     - dinding_level_2_t3.isPlaced = false
   - Actions:
     - Set position to (X_target, Y_target) - smooth snap
     - Set opacity = 100 (solid)
     - Set isPlaced = true
     - Disable DragDrop behavior
     - Add 1 to componentsPlaced
     - Show benar_level_2_t3 (flash 1 detik)
     - Call function: CheckWinCondition

3. **On Drop - Wrong Position**
   - Conditions:
     - dinding_level_2_t3 - On drop
     - NEGATE: Is overlapping target_level_2_t3
   - Actions:
     - Set position to (X_origin, Y_origin) - return ke awal
     - Set opacity = 100
     - Show tap2_sering_level_2_t3 atau cobalagi_level_2_t3 (flash 1 detik)
     - Maskot hint: "Hmm, coba lihat contohnya lagi ya~"

**⚠️ ULANGI untuk 8 komponen lainnya:**
- pintu_level_2_t3
- jendela_level_2_t3
- tangga_level_2_t3
- atap_pg_level_2_t3
- atas_stiga_level_2_t3
- kunci_level_2_t3
- layang_level_2_t3
- polygon_level_2_t3

**Total events di group ini:** 3 events × 9 komponen = 27 events

---

### GROUP 4: Win Condition
**Tujuan:** Detect kemenangan dan navigasi ke level berikutnya

**Events:**
1. **Check Win Condition (Function)**
   - Condition: componentsPlaced = totalComponents (9)
   - Actions:
     - Set gameActive = false
     - Hide rumahselesaidisusun_level_2_t3 (referensi tidak perlu lagi)
     - Wait 0.5 seconds
     - Show berhasil_level2_t3
     - Show maskot celebration: "Hebat! Rumahnya sempurna! 🏠✨"
     - Wait 3 seconds
     - Go to Layout: Lay_RoadMap

---

### GROUP 5: Maskot Dialog System
**Tujuan:** Memberikan feedback & hints lewat maskot

**Events:**
1. **Show Hint - On Start**
   - Trigger: Game start (gameActive = true)
   - Maskot (Numa): "Mari kita bangun rumah! Drag setiap bagian ke tempat yang tepat~"

2. **Show Hint - On Progress 25%**
   - Condition: componentsPlaced = 2 atau 3
   - Maskot (Numi): "Bagus! Terus semangat ya~"

3. **Show Hint - On Progress 50%**
   - Condition: componentsPlaced = 4 atau 5
   - Maskot (Numa): "Wow, sudah setengah jalan! Kamu hebat!"

4. **Show Hint - On Progress 75%**
   - Condition: componentsPlaced = 6 atau 7
   - Maskot (Numi): "Tinggal sedikit lagi! Semangat!"

5. **Show Hint - On Wrong Placement**
   - Trigger: Komponen di-drop di posisi salah
   - Maskot: "Hmm, coba lihat gambar contohnya lagi ya~"

**⚠️ NOTE:** Dialog bisa di-trigger via instance variable atau function call

---

### GROUP 6: UI Controls
**Tujuan:** Handle toggle reference, reset, dll

**Events:**
1. **Toggle Reference House**
   - Condition: Keyboard Press "R" atau Button click (jika ada)
   - Actions:
     - Toggle visibility rumahselesaidisusun_level_2_t3
     - Set showReference = NOT showReference

2. **Reset Button** (Optional - jika ditambahkan)
   - Condition: Click reset button
   - Actions:
     - For each komponen:
       - Set position to (X_origin, Y_origin)
       - Set isPlaced = false
       - Enable DragDrop
     - Set componentsPlaced = 0
     - Hide all notifications

---

### GROUP 7: Notifications Management
**Tujuan:** Auto-hide notifications setelah beberapa detik

**Events:**
1. **Auto Hide - benar_level2_t3**
   - Condition: benar_level2_t3 is visible
   - Action: Wait 1 second → Set invisible

2. **Auto Hide - cobalagi_level2_t3**
   - Condition: cobalagi_level2_t3 is visible
   - Action: Wait 1.5 seconds → Set invisible

3. **Auto Hide - tap2_sering_level2_t3**
   - Condition: tap2_sering_level2_t3 is visible
   - Action: Wait 1.5 seconds → Set invisible

**⚠️ NOTE:** berhasil_level2_t3 TIDAK auto-hide (tunggu sebelum navigasi)

---

## 🎨 OPTIONAL ENHANCEMENTS (Fase Polish)

### GROUP 8: Animations & Effects (Optional)
1. **Particle Effect on Correct Placement**
   - Spawn particles saat komponen snap ke posisi benar
   - Flash effect atau glow

2. **Sound Effects**
   - Drag sound (on drag start)
   - Drop correct sound (snap)
   - Drop wrong sound (return to origin)
   - Win sound (all components placed)

3. **Component Hover Effect**
   - On mouse hover: Scale 1.05x atau glow effect

---

## 📋 IMPLEMENTATION CHECKLIST

### FASE CORE (PRIORITAS TINGGI)
- [ ] **Group 1:** System Initialization
  - [ ] On Start of Layout
  - [ ] Save Original Positions (9 komponen)
  
- [ ] **Group 2:** Game Start
  - [ ] Dialog click to start
  
- [ ] **Group 3:** Drag & Drop Mechanics
  - [ ] dinding_level_2_t3 (3 events)
  - [ ] pintu_level_2_t3 (3 events)
  - [ ] jendela_level_2_t3 (3 events)
  - [ ] tangga_level_2_t3 (3 events)
  - [ ] atap_pg_level_2_t3 (3 events)
  - [ ] atas_stiga_level_2_t3 (3 events)
  - [ ] kunci_level_2_t3 (3 events)
  - [ ] layang_level_2_t3 (3 events)
  - [ ] polygon_level_2_t3 (3 events)
  
- [ ] **Group 4:** Win Condition
  - [ ] Check & navigate to RoadMap

### FASE POLISH (MEDIUM PRIORITY)
- [ ] **Group 5:** Maskot Dialog System
  - [ ] Hints pada berbagai progress points
  
- [ ] **Group 7:** Notifications Management
  - [ ] Auto-hide timers

### FASE ENHANCEMENT (LOW PRIORITY)
- [ ] **Group 6:** UI Controls (toggle reference)
- [ ] **Group 8:** Animations & Effects

---

## 🔢 EVENT COUNT ESTIMATION

| Group | Events | Complexity |
|-------|--------|------------|
| Group 1: System Init | 2-3 | Low |
| Group 2: Game Start | 1 | Low |
| Group 3: Drag & Drop | 27 (3×9) | High |
| Group 4: Win Condition | 1 | Low |
| Group 5: Maskot Dialog | 5 | Medium |
| Group 6: UI Controls | 1-2 | Low |
| Group 7: Notifications | 3 | Low |
| Group 8: Polish (Optional) | 5-10 | Medium |
| **TOTAL CORE** | **~34 events** | - |
| **TOTAL WITH POLISH** | **~47 events** | - |

---

## 🎯 SIMPLIFIED APPROACH (MINIMUM VIABLE)

Jika ingin implementasi cepat, bisa pakai 1 komponen sebagai template:

### TEMPLATE: Universal Drop Handler (Advanced)
Gunakan **single event** dengan **For Each** dan **instance variable checking**:

```
On ANY Object with DragDrop - On drop:
  - If overlapping target_level_2_t3:
      - Check distance antara posisi drop dengan X_target/Y_target
      - If distance < 50px (tolerance):
          - Snap to target
          - Set isPlaced = true
          - componentsPlaced++
      - Else:
          - Return to origin
  - Else:
      - Return to origin
```

**Keuntungan:** Cuma butuh ~10 events total (jauh lebih simple)  
**Kekurangan:** Kurang fleksibel untuk per-component rules

---

## 🚀 RECOMMENDED IMPLEMENTATION ORDER

1. ✅ **HARI 1:** Group 1 + 2 (System Init + Game Start) - 3-4 events
2. ✅ **HARI 2:** Group 3 - 1 komponen dulu (dinding) - 3 events - TEST
3. ✅ **HARI 3:** Group 3 - 8 komponen sisanya - 24 events
4. ✅ **HARI 4:** Group 4 (Win Condition) - 1 event - TEST end-to-end
5. ✅ **HARI 5:** Group 7 (Notifications) - 3 events
6. ⏳ **HARI 6:** Group 5 (Maskot) - 5 events - POLISH
7. ⏳ **HARI 7:** Testing & debugging - FULL QA

---

## 📌 CATATAN PENTING

### Target Zone Strategy
- **Single Zone:** Pakai 1 target_level_2_t3 untuk semua komponen
  - Validation pakai distance check ke X_target/Y_target
  - Lebih simple, cocok untuk beginner
  
- **Multiple Zones:** Buat 9 target zones berbeda
  - Validation pakai "Is overlapping specific target"
  - Lebih presisi, tapi lebih banyak objects

**REKOMENDASI:** Pakai **single zone** dengan **distance check**

### Snap Tolerance
- Tolerance: ±30-50px dari X_target/Y_target
- Terlalu ketat (±5px) = frustrating untuk player
- Terlalu longgar (±100px) = tidak presisi

### Performance Tips
- Disable collision checking untuk komponen yang sudah `isPlaced = true`
- Use "Pick by comparison" untuk filter komponen
- Avoid "Every tick" untuk drag logic

---

**Dibuat:** 31 Desember 2025  
**Status:** 📋 PLAN - Ready for Implementation  
**Next Step:** Implementasi Group 1 & 2 (System Init)
