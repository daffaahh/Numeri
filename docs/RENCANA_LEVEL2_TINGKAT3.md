# 📋 RENCANA PENGEMBANGAN LEVEL 2 TINGKAT 3
**Game NUMERI - Menyusun Rumah dari Bentuk Geometri**

---

## 🎯 KONSEP LEVEL

**Tema:** Konstruksi Rumah - Assembly Challenge  
**Target Pembelajaran:** Memahami komposisi bentuk geometri dalam membangun struktur  
**Format:** Drag & Drop Assembly/Construction  
**Durasi:** Tanpa timer (focus pada akurasi & kreativitas)

### Visual Design (Berdasarkan Assets)
- Setting: Area konstruksi rumah dengan target zones
- Komponen: 9 bagian rumah berbentuk geometri berbeda
- Target: Outline rumah lengkap sebagai referensi
- Maskot: Numa & Numi sebagai guide characters
- Feedback: Notifikasi untuk setiap penempatan benar/salah

---

## 📐 STRUKTUR LEVEL

### Layout Properties
- **Resolusi:** TBD (sesuai kebutuhan area konstruksi)
- **Projection:** Perspective
- **Event Sheet:** ES_Level2_T3

### Layer Organization (Planning)
1. **Layer 0** (Background)
   - Background (bg_level_2_t3)
   - Overlay hitam (bghitam_level_2_t3)
   - Judul level (judul_level_2_t3)
   - Rumah selesai referensi (rumahselesaidisusun_level_2_t3)

2. **Target Layer**
   - Target zones untuk setiap komponen (target_level_2_t3)
   - Drop indicators

3. **Items Layer** (Komponen yang bisa di-drag)
   - 9 komponen rumah geometri
   - Scattered di area sebelum assembly

4. **Maskot Layer**
   - Numa (numa_level_2_t3)
   - Numi (numi_level_2_t3)
   - Dialog bubbles

5. **Notifications Layer**
   - 4 sprite feedback
   - Pop-ups & messages

---

## ✅ STATUS PENGEMBANGAN

### SELESAI ✓

#### Komponen Wajib (Commit: f718ee6)
- [x] Event Sheet (ES_Level2_T3.json) - **~70% SELESAI**
- [x] Layout (Lay_Level2_T3.json) - **SELESAI**
- [x] Background & Frame
- [x] Judul level
- [x] Sistem Notifikasi (4 sprite)
- [x] Maskot (2 karakter)

#### Setup Komponen (Commit: a8c55ac - 31 Des 2025)
- [x] **DragDrop Behavior** - Semua 9 komponen sudah ada
- [x] **BoundToLayout Behavior** - Semua 9 komponen sudah ada
- [x] **Instance Variables** - 6 variabel per komponen (54 total):
  - [x] componentType - Tipe komponen (string)
  - [x] X_origin - Posisi awal X untuk reset (number)
  - [x] Y_origin - Posisi awal Y untuk reset (number)
  - [x] X_target - Posisi target X yang benar (number)
  - [x] Y_target - Posisi target Y yang benar (number)
  - [x] isPlaced - Status sudah terpasang atau belum (boolean)
- [x] **Deskripsi Variabel** - Semua 54 variabel sudah ada deskripsi bahasa Indonesia
- [x] **Bug Fix** - atas_stiga isPlaced type diperbaiki ke boolean

#### Event Sheet Logic (Commit: 3027b80 - 3 Jan 2026)
- [x] **Event Variables** - 4 variabel: componentsPlaced, totalComponents, gameActive, showReference
- [x] **Group 1: System Initialization** - On Start of Layout
  - [x] Set visibility semua objek (bg, dialog, notifications, maskot)
  - [x] Reset event variables (componentsPlaced=0, gameActive=0)
  - [x] Save posisi X_origin & Y_origin untuk 9 komponen
  - [x] Reset isPlaced=0 untuk semua komponen
- [x] **Group 2: Dialog Flow** - Klik dialog → mulai game ✅
- [x] **Group 3: Drop Validation** - Cek posisi saat drop ✅
- [x] **Group 4: Win Condition** - Cek 9 komponen terpasang → go to T4 ✅
- [ ] **Group 5: Reset/Retry** - Reset komponen yang salah ⏳
- [ ] **Group 6: Navigation** - Go to RoadMap ⏳

#### Layout Fix - Z-Order & Drop Positions (Commit: fd31d86 - 6 Jan 2026)
- [x] **Z-Order Fix** - Dinding dipindahkan ke urutan pertama agar tidak menindih pintu/jendela/kunci
- [x] **Drop Position Update** - Semua 9 komponen posisi target sudah diupdate:

| Komponen | X_target | Y_target |
|----------|----------|----------|
| dinding | 573 | 429 |
| pintu | 588 | 433 |
| jendela | 503 | 413 |
| kunci | 613 | 442 |
| tangga | 588 | 506.307028 |
| atap_segitiga | 573 | 264.5 |
| atap_pg | 532 | 278 |
| polygon | 603 | 274 |
| layang | 657.038737 | 369.291166 |

#### ASSETS - KOMPONEN RUMAH (9 Items)

**Atap - 2 Komponen:**
- [x] atap_pg_level_2_t3 (atap persegi/datar)
- [x] atas_stiga_level_2_t3 (atap segitiga/runcing)

**Dinding & Struktur - 3 Komponen:**
- [x] dinding_level_2_t3 (dinding utama)
- [x] pintu_level_2_t3 (pintu - bentuk persegi panjang)
- [x] tangga_level_2_t3 (tangga)

**Detail & Aksesori - 4 Komponen:**
- [x] jendela_level_2_t3 (jendela)
- [x] kunci_level_2_t3 (kunci pintu)
- [x] layang_level_2_t3 (bentuk layang-layang - dekorasi?)
- [x] polygon_level_2_t3 (bentuk segilima/polygon - dekorasi?)

**Referensi:**
- [x] rumahselesaidisusun_level_2_t3 (gambar rumah lengkap sebagai guide)

**Target:**
- [x] target_level_2_t3 (zona drop indicator)

**Maskot - 2 Karakter:**
- [x] numa_level_2_t3 (karakter maskot 1)
- [x] numi_level_2_t3 (karakter maskot 2)

**Notifications - 4 Sprite:**
- [x] benar_level_2_t3 (correct placement feedback)
- [x] berhasil_level_2_t3 (success screen)
- [x] cobalagi_level_2_t3 (try again message)
- [x] tap2_sering_level_2_t3 (tap frequently reminder/hint)

**UI Elements:**
- [x] bg_level_2_t3 (background)
- [x] bghitam_level_2_t3 (dark overlay)
- [x] dialog_level_2_t3 (dialog popup)
- [x] judul_level_2_t3 (title)

---

## 🎮 GAMEPLAY MECHANIC

### Flow Permainan
1. **Start:**
   - Show dialog_level_2_t3 (instruksi)
   - Show rumahselesaidisusun_level_2_t3 (referensi)
   - Show all komponen scattered
   - Maskot memberikan petunjuk

2. **Assembly Phase:**
   - Player drag komponen rumah
   - Drop ke target zone yang sesuai
   - Validasi: Cek apakah komponen di posisi benar
   - Feedback:
     * **Benar:** Show benar_level_2_t3 → Lock komponen
     * **Salah:** Show tap2_sering_level_2_t3 atau cobalagi_level_2_t3 → Return ke posisi awal

3. **Component Order (Suggested):**
   - Step 1: Dinding (foundation)
   - Step 2: Pintu
   - Step 3: Jendela
   - Step 4: Tangga
   - Step 5: Atap persegi (base)
   - Step 6: Atap segitiga (top)
   - Step 7-9: Dekorasi (kunci, layang-layang, polygon)

4. **Win Condition:**
   - Semua 9 komponen terpasang dengan benar
   - Rumah terbentuk sempurna
   - Show berhasil_level_2_t3
   - Maskot memberikan pujian
   - Go to RoadMap

5. **Lose/Retry Condition:**
   - Tidak ada lose condition (player bisa retry tanpa batas)
   - Jika salah → Show cobalagi_level_2_t3 → Retry

### Interaksi yang Dibutuhkan
- **Drag & Drop** - Untuk memindahkan komponen
- **Snap to Grid/Position** - Untuk alignment yang rapi
- **Collision Detection** - Untuk validasi posisi
- **Component Order Validation** - Beberapa komponen harus dipasang dulu
- **Z-Order Management** - Layering komponen yang benar
- **Progress Tracking** - Monitor komponen yang sudah terpasang

---

## 🔧 EVENT SHEET - YANG PERLU DIBUAT

### 1. System Events
```
On Start of Layout:
  - Show dialog_level_2_t3 (instruksi)
  - Show rumahselesaidisusun_level_2_t3 (referensi, semi-transparent)
  - Randomize/scatter posisi komponen
  - Set componentsPlaced = 0
  - Show maskot dengan dialog pembuka
```

### 2. Drag & Drop Mechanics
```
Setup Behaviors:
  - Add DragDrop behavior ke semua 9 komponen
  - Add BoundToLayout behavior
  - Set initial enabled = true

On Item Touched:
  - Enable drag mode
  - Bring to front (Z-order)
  
On Item Dropped:
  - Check collision with target zone
  - Validate position & snap
  - If correct:
      - Snap to exact position
      - Lock item (disable drag)
      - Show benar_level_2_t3
      - componentsPlaced++
      - Check win condition
  - Else:
      - Return to original position
      - Show tap2_sering_level_2_t3 atau cobalagi_level_2_t3
```

### 3. Position Validation
```
Function: ValidateComponentPosition(component, targetZone)
  - Check overlap dengan target zone yang sesuai
  - Check apakah prerequisites terpenuhi (misal: dinding harus dipasang sebelum jendela)
  - Return TRUE/FALSE
  
Function: SnapToPosition(component)
  - Set component.X = targetZone.X
  - Set component.Y = targetZone.Y
  - Set component.Angle = 0 (jika perlu)
  - Set Z-order sesuai layer
```

### 4. Component-Target Mapping
```
Mapping (Instance Variables):
- dinding_level_2_t3 → targetZone_dinding
- pintu_level_2_t3 → targetZone_pintu
- jendela_level_2_t3 → targetZone_jendela
- tangga_level_2_t3 → targetZone_tangga
- atap_pg_level_2_t3 → targetZone_atapPersegi
- atas_stiga_level_2_t3 → targetZone_atapSegitiga
- kunci_level_2_t3 → targetZone_kunci
- layang_level_2_t3 → targetZone_layang
- polygon_level_2_t3 → targetZone_polygon
```

### 5. Win Condition
```
If componentsPlaced = 9:
  - Disable all drag behaviors
  - Hide rumahselesaidisusun_level_2_t3 (referensi)
  - Show berhasil_level_2_t3
  - Maskot memberikan pujian
  - Wait 3 seconds
  - Go to Lay_RoadMap
```

### 6. Maskot Dialog System
```
Function: ShowMaskotDialog(message)
  - Show dialog_level_2_t3 dengan text
  - Position near Numa/Numi
  - Auto-hide after 3 seconds atau on click

Trigger moments:
- On start: "Mari kita bangun rumah!"
- On first correct: "Bagus! Lanjutkan!"
- On wrong placement: "Coba lihat lagi contohnya ya~"
- On halfway (4-5 komponen): "Sudah setengah jalan!"
- On finish: "Hebat! Rumahnya sempurna!"
```

---

## 📊 VARIABLES YANG DIBUTUHKAN

### Layout Variables (Local)
```javascript
componentsPlaced = 0     // Jumlah komponen yang sudah terpasang benar
totalComponents = 9      // Total komponen rumah
houseComplete = false    // Status rumah sudah selesai
showReference = true     // Toggle tampilan referensi rumah
```

### Instance Variables (Per Component)
```javascript
componentType = ""       // Jenis komponen (dinding, pintu, dll)
X_origin = 0             // Posisi awal X untuk reset
Y_origin = 0             // Posisi awal Y untuk reset
X_target = 0             // Posisi target X yang benar
Y_target = 0             // Posisi target Y yang benar
isPlaced = false         // Status sudah terpasang atau belum
orderPriority = 0        // Urutan prioritas pemasangan (1-9)
```

**⚠️ CATATAN:** Tidak menggunakan Global Variables - semua lokal per layout.

---

## 🎨 VISUAL FEEDBACK

### Animasi yang Direkomendasikan
1. **Component Hover:** Glow effect atau scale 1.05x
2. **Component Drag:** Semi-transparent (opacity 0.8)
3. **Correct Placement:** 
   - Snap smooth dengan tween
   - Green flash
   - Particle effect (sparkles)
   - Scale bounce (1.0 → 1.1 → 1.0)
4. **Wrong Placement:** 
   - Red flash
   - Shake animation
   - Smooth return to origin
5. **Reference House:** 
   - Semi-transparent (opacity 0.4)
   - Toggle on/off dengan button
   - Outline highlight
6. **Maskot Dialog:** 
   - Slide in dari samping
   - Bounce animation
   - Fade out after delivery

---

## 📝 CHECKLIST TAHAP PENGEMBANGAN

### FASE 1: Basic Assembly ✅ SELESAI
- [x] Setup layout & layers
- [x] Import semua assets (9 komponen + UI)
- [x] **Setup Drag & Drop behaviors (9 komponen)** ✅ 31 Des 2025
- [x] **Setup BoundToLayout behaviors (9 komponen)** ✅ 31 Des 2025
- [x] **Setup instance variables (6 per komponen)** ✅ 31 Des 2025
- [x] **Tambah deskripsi variabel (bahasa Indonesia)** ✅ 31 Des 2025
- [ ] **Posisikan target zones dengan benar** ⏳ NEXT
- [ ] **Implement basic drag & drop logic** ⏳ NEXT
- [ ] **Test komponen bisa di-drag** ⏳ NEXT

### FASE 2: Validation & Snap ⏳ IN PROGRESS
- [ ] **Set nilai X_origin & Y_origin untuk semua komponen** 🎯 PRIORITAS
- [ ] **Set nilai X_target & Y_target untuk semua komponen** 🎯 PRIORITAS
- [ ] **Posisikan komponen di posisi awal (scattered)** 🎯 PRIORITAS
- [ ] Create/posisikan target zone (single zone untuk semua)
- [ ] Implement collision detection logic
- [ ] Implement snap-to-position logic
- [ ] Implement position validation
- [ ] Test snap accuracy

### FASE 3: Component Order & Rules
- [ ] Define component placement order
- [ ] Implement prerequisite checking
- [ ] Z-order management per layer
- [ ] Test assembly sequence

### FASE 4: Feedback & Polish
- [ ] Setup notification system
- [ ] Implement maskot dialog system
- [ ] Add sound effects
- [ ] Add particle effects
- [ ] Add animations
- [ ] Test complete assembly flow

### FASE 5: Integration
- [ ] Win condition integration
- [ ] RoadMap navigation
- [ ] Final testing
- [ ] Performance optimization

---

## 🎯 PRIORITAS KERJA IMMEDIATE

### URGENT - Sedang Dikerjakan (31 Des 2025):
1. **Event Sheet Implementation** ⚠️ PRIORITAS #1
   - Buat logika drag & drop dasar
   - Buat logika snap to position
   - Buat validation system
   - Buat win condition
   - **Target:** Gameplay bisa dimainkan end-to-end
   
2. **Layout Adjustments** ⚠️ PRIORITAS #2
   - Set nilai X_origin & Y_origin (posisi awal komponen)
   - Set nilai X_target & Y_target (posisi target yang benar)
   - Posisikan komponen di area scattered
   - **Bisa dilakukan manual di Construct 3 atau via JSON**

### MEDIUM - Setelah Core Logic:
1. Maskot dialog system
2. Advanced animations
3. Sound design
4. Polish & optimization

### COMPLETED ✅:
1. ~~Setup Behaviors~~ - DragDrop + BoundToLayout (a8c55ac)
2. ~~Instance Variables~~ - 6 variabel × 9 komponen (a8c55ac)
3. ~~Deskripsi Variabel~~ - Dokumentasi bahasa Indonesia (a8c55ac)

---

## 🔄 GAME FLOW DIAGRAM

```
[START]
   ↓
[Show Dialog - Instruksi] → Maskot menjelaskan
   ↓
[Show Referensi Rumah] → Semi-transparent guide
   ↓
[Show 9 Komponen Scattered]
   ↓
[Player Drag Komponen] ←→ [Drop ke Target]
   ↓                          ↓
   ├── Correct Position → [Snap & Lock] → [componentsPlaced++]
   │                            ↓
   │                     [Check: All Done?]
   │                            ↓
   │                     [NO: Continue Assembly]
   │                            ↓
   └── Wrong Position → [Show Feedback] → [Return to Origin]
                              ↓
                       [Retry Placement]
                              ↓
                    [All Components Placed?]
                              ↓
                         [YES: WIN!]
                              ↓
                    [Show Berhasil + Maskot Pujian]
                              ↓
                       [Go to RoadMap]
```

---

## 📚 REFERENSI NAMING CONVENTION

### Pattern Komponen:
- `{jenisKomponen}_level_2_t3`
- Contoh: `dinding_level_2_t3`, `pintu_level_2_t3`

### Pattern Target Zone:
- `targetZone_{jenisKomponen}` atau `target_level_2_t3` (single reusable)
- Contoh: `targetZone_dinding`, `targetZone_pintu`

### Pattern Notifications:
- `{kondisi}_level_2_t3`
- Contoh: `benar_level_2_t3`, `berhasil_level_2_t3`

---

## 🚀 NEXT STEPS

1. **SEKARANG:** Implementasi Event Sheet ES_Level2_T3.json 🎯
   - Logika drag & drop dasar
   - Logika snap to position & validation
   - Logika win condition & navigation
   
2. **HARI INI:** Set posisi origin & target untuk 9 komponen
   - Bisa manual di Construct 3
   - Atau via JSON editing
   
3. **BESOK:** Testing & debugging assembly flow
   - Test drag komponen
   - Test snap accuracy
   - Test win condition
   
4. **MINGGU DEPAN:** Polish & integration
   - Animations & sound effects
   - Maskot dialog
   - Full T1→T2→T3 testing

5. **SETELAH ITU:** Level 2 Tingkat 4 (Final Level)

---

## 📌 CATATAN PENTING

⚠️ **JANGAN LUPA:**
- Layout perlu direvisi dengan layer structure yang proper
- Event Sheet masih kosong, ini prioritas #2 (setelah layout)
- **TIDAK menggunakan Global Variables** - semua lokal per layout
- Target zones harus presisi untuk snap yang rapi
- Z-order sangat penting untuk assembly yang benar
- Beberapa komponen mungkin ada prerequisites (misal: dinding sebelum jendela)

✨ **TIPS DEVELOPMENT:**
- Gunakan grid untuk positioning yang konsisten
- Buat function reusable untuk validation
- Test snap accuracy dengan precision tinggi
- Pertimbangkan toleransi untuk snap (misal: ±10px)
- Reference house sebaiknya bisa di-toggle on/off
- Maskot dialog jangan mengganggu area kerja

💡 **PERBEDAAN DENGAN T1 & T2:**
- T1: Drag & Drop + Sorting (mengelompokkan)
- T2: Click + Quiz (recognition)
- **T3: Drag & Drop + Assembly (konstruksi spatial)**

🎨 **CREATIVE CONSIDERATIONS:**
- Komponen layang-layang & polygon: fungsinya apa? Dekorasi?
- Bisa tambahkan "freestyle mode" untuk kreativitas?
- Consider multiple solution (rumah bisa beda-beda style)?

**Dibuat:** 29 Desember 2025  
**Last Update:** 3 Januari 2026 - System Initialization Selesai (Commit: 3027b80)  
**Status:** ⏳ FASE 2 IN PROGRESS - Event Sheet Implementation (~55%)  
**Developer:** Tim NUMERI

---

## 📊 PROGRESS METER

```
┌────────────────────────────────────────────────────────┐
│ LEVEL 2 TINGKAT 3 - Assembly Challenge                 │
├────────────────────────────────────────────────────────┤
│                                                        │
│ Assets & Sprites     ████████████████████████  100%   │
│ Behaviors Setup      ████████████████████████  100%   │
│ Instance Variables   ████████████████████████  100%   │
│ Event Sheet Logic    ████████████               50%   │
│ Layout Positioning   ██████████                 40%   │
│ Win Condition        ██████                     25%   │
│ Polish & Animation   ████                       10%   │
│                                                        │
│ ──────────────────────────────────────────────────     │
│ TOTAL PROGRESS: ≈ 55%                                  │
└────────────────────────────────────────────────────────┘
```

### Commit History:
| Date | Hash | Description |
|------|------|-------------|
| 29 Des 2025 | `f718ee6` | Initial setup layout & assets |
| 31 Des 2025 | `a8c55ac` | Setup DragDrop & Instance Variables |
| 3 Jan 2026 | `3027b80` | WIP: System initialization & partial logic |

---

## 🏗️ ARSITEKTUR RUMAH (Reference)

```
Struktur Rumah (Top to Bottom):
┌─────────────────┐
│  Atap Segitiga  │  ← atas_stiga_level_2_t3
├─────────────────┤
│  Atap Persegi   │  ← atap_pg_level_2_t3
├─────────────────┤
│ [Layang] [Poly] │  ← Dekorasi atas
├─────────────────┤
│  [Jendela]      │  ← jendela_level_2_t3
│                 │
│    Dinding      │  ← dinding_level_2_t3
│                 │
│  [Pintu+Kunci]  │  ← pintu + kunci_level_2_t3
├─────────────────┤
│     Tangga      │  ← tangga_level_2_t3 (depan pintu)
└─────────────────┘
```

**Layer Order (Back to Front):**
1. Background
2. Dinding (base)
3. Atap persegi
4. Atap segitiga
5. Pintu
6. Jendela
7. Kunci
8. Tangga
9. Dekorasi (layang-layang, polygon)
