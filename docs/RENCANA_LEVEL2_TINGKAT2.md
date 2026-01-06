# 📋 RENCANA PENGEMBANGAN LEVEL 2 TINGKAT 2
**Game NUMERI - Quiz Pengenalan Bentuk Geometri**

---

## 🎯 KONSEP LEVEL

**Tema:** Quiz Visual - Pilih Bentuk yang Benar  
**Target Pembelajaran:** Mengenali dan memilih bentuk geometri yang sesuai dengan pertanyaan  
**Format:** Multiple Choice Quiz dengan visual feedback  
**Durasi:** Tidak ada timer (focus pada akurasi)

### Visual Design (Berdasarkan Assets)
- Setting: Background quiz dengan area pertanyaan dan pilihan
- Dialog: 2 popup dialog untuk intro dan instruksi
- Soal: Display pertanyaan dengan visual bentuk target
- Pilihan: 3 tombol pilihan (1 benar, 2 salah)
- Feedback: Notifikasi instant untuk setiap jawaban

---

## 📐 STRUKTUR LEVEL

### Layout Properties
- **Resolusi:** 286 x 174 px (compact quiz format)
- **Projection:** Perspective
- **Event Sheet:** ES_Level2_T2

### Layer Organization
1. **Layer 0** (Main Game Layer)
   - Background (bg_level_2_t2)
   - Dialog popups (dialog_level_2_t2_1, dialog_level_2_t2_2)
   - Soal display (soal_persegi_level_2_t2)
   - Pilihan jawaban (bener, salah2, salah3)
   - Petunjuk (PETUNJUKPERSEGI_level_2_t2)
   - Notifications (5 sprites)

2. **Layer 1** (Reserved)
   - Empty - untuk elemen tambahan

3. **Layer 2** (Reserved)
   - Empty - untuk elemen tambahan

4. **Layer 3** (Reserved)
   - Empty - untuk elemen tambahan

---

## ✅ STATUS PENGEMBANGAN

### SELESAI ✓ (30 Desember 2025)

#### Komponen Wajib
- [x] Event Sheet (ES_Level2_T2.json) - **✅ COMPLETE (6 groups implemented)**
- [x] Layout (Lay_Level2_T2.json) - **✅ SETUP & FIXED (bg visibility corrected)**
- [x] Background
- [x] Dialog System (2 sprite)
- [x] Sistem Notifikasi (5 sprite)

#### ASSETS - PERSEGI (Quiz Pertama)

**Dialog & Instruksi - 2 Sprite:**
- [x] dialog_level_2_t2_1 (intro dialog)
- [x] dialog_level_2_t2_2 (instruction dialog)

**Soal - 1 Sprite:**
- [x] soal_persegi_level_2_t2 (pertanyaan untuk bentuk persegi)

**Pilihan Jawaban - 3 Sprite:**
- [x] bener_level_2_t2 (jawaban benar - persegi)
- [x] salah2_level_2_t2 (distractor 1)
- [x] salah3_level_2_t2 (distractor 2)

**Petunjuk - 1 Sprite:**
- [x] PETUNJUKPERSEGI_level_2_t2 (hint/guide)

**Notifications - 5 Sprite:**
- [x] jikaBenar_level_2_t2 (correct answer feedback)
- [x] jikaSalahpilih_level_2_t2 (wrong answer feedback)
- [x] jikaWaktuHabis_level_2_t2 (time's up - optional)
- [x] finish_level_2_t2 (level complete)
- [x] motivasi_level_2_t2 (motivation message)

---

### PENDING ⏳ (Belum dibuat)

#### SOAL & PILIHAN - SEGITIGA
**Soal:**
- [ ] soal_segitiga_level_2_t2 (pertanyaan segitiga)

**Pilihan:**
- [ ] bener_segitiga_level_2_t2 (jawaban benar)
- [ ] salah2_segitiga_level_2_t2 (distractor 1)
- [ ] salah3_segitiga_level_2_t2 (distractor 2)

#### SOAL & PILIHAN - LINGKARAN
**Soal:**
- [ ] soal_lingkaran_level_2_t2 (pertanyaan lingkaran)

**Pilihan:**
- [ ] bener_lingkaran_level_2_t2 (jawaban benar)
- [ ] salah2_lingkaran_level_2_t2 (distractor 1)
- [ ] salah3_lingkaran_level_2_t2 (distractor 2)

#### SOAL & PILIHAN - BENTUK KOMPLEKS (Optional)
- [ ] Belah ketupat, trapesium, jajar genjang, dll
- [ ] Masing-masing butuh 1 soal + 3 pilihan

---

## 🎮 GAMEPLAY MECHANIC

### Flow Permainan
1. **Start:**
   - Show dialog_level_2_t2_1 (intro)
   - Player click untuk lanjut
   - Show dialog_level_2_t2_2 (instruksi)

2. **Quiz Loop:**
   - Show soal (pertanyaan dengan visual)
   - Show 3 pilihan jawaban
   - Player click salah satu pilihan
   - Validasi jawaban:
     * **Benar:** Show jikaBenar → Next question
     * **Salah:** Show jikaSalahpilih → Retry atau lanjut

3. **Question Progression:**
   - Soal 1: Persegi
   - Soal 2: Segitiga (jika sudah dibuat)
   - Soal 3: Lingkaran (jika sudah dibuat)
   - Dst...

4. **Win Condition:**
   - Semua soal terjawab dengan benar
   - Show finish_level_2_t2
   - Show motivasi_level_2_t2
   - Go to RoadMap

5. **Lose Condition (Optional):**
   - Jika ada timer: waktu habis
   - Show jikaWaktuHabis_level_2_t2
   - Retry atau back to RoadMap

### Interaksi yang Dibutuhkan
- **Click Detection** - Untuk memilih jawaban
- **Answer Validation** - Untuk cek benar/salah
- **State Management** - Track soal ke berapa
- **Notification System** - Feedback visual
- **Score/Progress Tracking** - Monitor kemajuan (optional)

---

## 🔧 EVENT SHEET - YANG PERLU DIBUAT

### 1. System Events
```
On Start of Layout:
  - Show dialog_level_2_t2_1 (intro)
  - Hide all soal & pilihan
  - Hide all notifications
  - Set currentQuestion = 1
  - Set score = 0
```

### 2. Dialog Flow
```
On Click dialog_level_2_t2_1:
  - Hide dialog_level_2_t2_1
  - Show dialog_level_2_t2_2 (instruksi)
  
On Click dialog_level_2_t2_2:
  - Hide dialog_level_2_t2_2
  - Call ShowQuestion(currentQuestion)
```

### 3. Question Display Logic
```
Function: ShowQuestion(questionNumber)
  If questionNumber = 1:
    - Show soal_persegi_level_2_t2
    - Show bener_level_2_t2
    - Show salah2_level_2_t2
    - Show salah3_level_2_t2
  
  If questionNumber = 2:
    - Show soal_segitiga_level_2_t2
    - Show pilihan segitiga
  
  If questionNumber = 3:
    - Show soal_lingkaran_level_2_t2
    - Show pilihan lingkaran
```

### 4. Answer Validation
```
On Click bener_level_2_t2 (atau pilihan benar lainnya):
  - Hide all pilihan
  - Show jikaBenar_level_2_t2
  - Add score
  - Wait 1.5 seconds
  - Hide jikaBenar_level_2_t2
  - currentQuestion++
  - If currentQuestion > totalQuestions:
      Call ShowFinish()
  - Else:
      Call ShowQuestion(currentQuestion)

On Click salah2/salah3 (pilihan salah):
  - Show jikaSalahpilih_level_2_t2
  - Wait 1 second
  - Hide jikaSalahpilih_level_2_t2
  - (Optional: Allow retry atau auto-lanjut)
```

### 5. Finish & Navigation
```
Function: ShowFinish()
  - Hide all soal & pilihan
  - Show finish_level_2_t2
  - Wait 2 seconds
  - Show motivasi_level_2_t2
  - Wait 2 seconds
  - Go to Lay_RoadMap
```

### 6. Timer System (Optional)
```
Every 1 second (if timer enabled):
  - Subtract 1 from timer
  - Update timer display
  
If timer = 0:
  - Stop quiz
  - Show jikaWaktuHabis_level_2_t2
  - Wait 2 seconds
  - Go to RoadMap
```

---

## 📊 VARIABLES YANG DIBUTUHKAN

### Layout Variables (Local)
```javascript
currentQuestion = 1      // Soal ke berapa (1-3 atau lebih)
score = 0                // Jumlah jawaban benar
totalQuestions = 1       // Total soal (mulai dari 1 untuk persegi)
timer = 60               // Optional: 60 detik (jika pakai timer)
quizActive = false       // Status quiz sedang berjalan
```

**⚠️ CATATAN:** Tidak menggunakan Global Variables - semua lokal per layout.

---

## 🎨 VISUAL FEEDBACK

### Animasi yang Direkomendasikan
1. **Pilihan Hover:** Scale 1.1x atau brightness increase
2. **Click Feedback:** Quick scale down → bounce back
3. **Correct Answer:** Green glow + checkmark animation
4. **Wrong Answer:** Red flash + shake animation
5. **Notifications:** Fade in dengan slide dari atas
6. **Dialog Transition:** Fade out → Fade in next dialog

---

## 📝 CHECKLIST TAHAP PENGEMBANGAN

### FASE 1: Single Question (Persegi) ✅ COMPLETE
- [x] Setup layout & layers
- [x] Import semua assets untuk persegi
- [x] Posisikan objek di layout
- [x] **Setup click detection untuk pilihan** ✅
- [x] **Implement dialog flow logic** ✅
- [x] **Implement answer validation** ✅
- [x] **Setup notification system** ✅
- [x] **Test single question flow** ✅
- [x] **Fix background visibility bug** ✅
- [x] **Add is-visible conditions to prevent false triggers** ✅
- [x] **Setup navigation: T1 → T2 → T3** ✅

### FASE 2: Multiple Questions
- [ ] Buat soal & pilihan untuk segitiga
- [ ] Buat soal & pilihan untuk lingkaran
- [ ] Implement question progression logic
- [ ] Update totalQuestions variable
- [ ] Test question transitions

### FASE 3: Timer & Score (Optional)
- [ ] Add timer system
- [ ] Add score display
- [ ] Implement time's up condition
- [ ] Test timer functionality

### FASE 4: Polish & Integration
- [ ] Add sound effects (click, correct, wrong)
- [ ] Add animations
- [ ] Add particle effects untuk correct answer
- [ ] Optimize performance
- [ ] Final testing
- [ ] Integration dengan RoadMap

---

## 🎯 PRIORITAS KERJA IMMEDIATE

### URGENT - ✅ SELESAI:
1. **Implementasi Event Sheet ES_Level2_T2** ✅
   - ✅ Dialog flow (intro → instruksi → quiz)
   - ✅ Click detection untuk 3 pilihan
   - ✅ Answer validation (benar/salah)
   - ✅ Notification system
   - ✅ Fix boolean comparison (1/0 instead of "true"/"false")
   - ✅ Add is-visible conditions to prevent overlap triggers

2. **Test Single Question Flow** ✅
   - ✅ Dialog berfungsi dengan benar
   - ✅ Validasi jawaban benar/salah berfungsi
   - ✅ Notifikasi muncul dengan benar
   - ✅ Navigation ke T3 setelah selesai

### MEDIUM - Bisa Nanti:
1. Buat soal untuk bentuk lain (segitiga, lingkaran)
2. Implement question progression
3. Add timer (optional)
4. Polish visual & animations

---

## 🔄 GAME FLOW DIAGRAM

```
[START]
   ↓
[Show Dialog 1 - Intro] → Player baca
   ↓
[Click to Continue]
   ↓
[Show Dialog 2 - Instruksi] → Player baca
   ↓
[Click to Start]
   ↓
[Show Question + 3 Choices]
   ↓
[Player Click Choice] ←→ [Validate Answer]
   ↓                        ↓
   ├── Correct → [Show Success] → [Next Question]
   │                                   ↓
   │                         More Questions? → [YES: Loop back]
   │                                   ↓
   │                         [NO: All Done!]
   │                                   ↓
   └── Wrong → [Show Error] → [Retry/Continue?]
                    ↓
            [Continue Quiz]
                    ↓
            [All Questions Done?] → [Show Finish + Motivasi]
                                           ↓
                                    [Go to RoadMap]
```

---

## 📚 REFERENSI NAMING CONVENTION

### Pattern Soal:
- `soal_{bentuk}_level_2_t2`
- Contoh: `soal_persegi_level_2_t2`

### Pattern Pilihan Benar:
- `bener_{bentuk}_level_2_t2` atau `bener_level_2_t2`
- Contoh: `bener_level_2_t2`

### Pattern Pilihan Salah:
- `salah{n}_{bentuk}_level_2_t2` atau `salah{n}_level_2_t2`
- Contoh: `salah2_level_2_t2`, `salah3_level_2_t2`

### Pattern Notifications:
- `{kondisi}_level_2_t2`
- Contoh: `jikaBenar_level_2_t2`, `jikaSalahpilih_level_2_t2`

---

## 🚀 NEXT STEPS

1. **SELESAI:** ✅ Implementasi logika quiz di `ES_Level2_T2.json`
2. **SELESAI:** ✅ Test & debug single question flow
3. **OPTIONAL - FASE 2:** Tambah soal untuk bentuk lain (segitiga, lingkaran)
4. **OPTIONAL - FASE 3:** Add timer & score system
5. **POLISH:** Sound effects & animations
6. **FOCUS NEXT:** Level 2 Tingkat 3 (Assembly/Construction)

---

## 📌 CATATAN PENTING

⚠️ **JANGAN LUPA:**
- Event Sheet masih kosong, ini prioritas #1
- **TIDAK menggunakan Global Variables** - semua lokal per layout
- Quiz format berbeda dari T1 (drag & drop) - ini click-based
- Feedback harus instant dan jelas
- Hindari penalti yang terlalu keras untuk jawaban salah
- Focus pada pembelajaran, bukan kesulitan

✨ **TIPS DEVELOPMENT:**
- Buat function reusable untuk show/hide objects
- Gunakan array atau dictionary untuk soal (jika perlu)
- Test setiap validasi jawaban secara menyeluruh
- Pastikan tidak ada "stuck state" dalam quiz flow
- Sound effect penting untuk engagement

💡 **PERBEDAAN DENGAN T1:**
- T1: Drag & Drop (spatial reasoning)
- T2: Quiz (recognition & selection)
- T3: Assembly/Construction (planned)

**Dibuat:** 29 Desember 2025  
**Last Update:** 30 Desember 2025 - FASE 1 COMPLETE ✅
**Status:** ✅ PLAYABLE - Single Question Quiz Fully Functional
**Developer:** Tim NUMERI

---

## 🎉 IMPLEMENTATION SUMMARY (30 Des 2025)

### Event Sheet Structure (ES_Level2_T2.json)
**6 Groups Implemented:**
1. ✅ **Step 1 - System Initialization** (12 actions)
   - Setup initial visibility for all objects
   - Only bg + dialog_1 visible on start

2. ✅ **Step 2 - Dialog Flow** (2 events)
   - Dialog 1 → Dialog 2 → Quiz display
   - Mouse click detection with is-visible condition
   - Wait delays to prevent overlap

3. ✅ **Step 3 - Quiz Display** (empty - logic in Step 2)
   - Reserved for optional features

4. ✅ **Step 4 - Answer Validation** (3 events)
   - Correct answer: show jikaBenar → finish
   - Wrong answers: show jikaSalahpilih → retry
   - Instance variable `isCorrect` comparison (1/0)
   - is-visible conditions prevent false triggers

5. ✅ **Step 5 - Finish & Navigation** (1 event)
   - Click finish → motivasi (3s) → auto navigate to T3
   - is-visible condition ensures proper timing

6. ⏳ **Step 6 - Helper Functions** (empty - optional)
   - Reserved for shuffle, hints, timer

### Key Fixes Applied:
- ✅ Background visibility corrected in layout
- ✅ Boolean values changed from "true"/"false" to 1/0
- ✅ is-visible conditions added to all click events
- ✅ Navigation chain: T1 → T2 → T3

### Tested & Working:
- ✅ Dialog progression
- ✅ Answer validation (correct/wrong)
- ✅ Notification system
- ✅ Level completion flow
- ✅ Navigation to next level
