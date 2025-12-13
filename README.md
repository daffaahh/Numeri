# 🎮 Project NUMERI - Collaboration & Git Guide

Dokumen ini berisi panduan kolaborasi tim development game **NUMERI**. Wajib dibaca dan dipatuhi agar project tidak rusak (*corrupt*) saat kerja bareng.

---

## 🌳 1. Strategi Branching: "Developer Branch"

Kita menggunakan sistem **Branch per Developer**. Setiap orang memiliki "kamar kerja" sendiri yang permanen.

### 📜 Aturan Utama:
1.  **Branch `main` adalah SUCI.** Isinya adalah versi game yang stabil/bisa dimainkan. Jangan pernah push langsung ke `main` kecuali darurat.
2.  **Branch Developer:** Gunakan nama branch sesuai namamu.
    * `dev-budi`
    * `dev-siti`
    * `dev-joko`

### ⚠️ Bahaya Konflik File Induk (.c3proj)
Construct 3 memiliki file `project.c3proj` yang berubah setiap kali kamu menambah Layout/Event Sheet/Asset baru.
* **RISIKO:** Jika Budi menambah Layout A dan Siti menambah Layout B, lalu kalian tidak saling update selama seminggu, file `.c3proj` akan bentrok parah saat digabung.
* **SOLUSI: ATURAN 24 JAM.** Jangan biarkan codinganmu mengendap di branch sendiri lebih dari 24 jam. Selesaikan tugas kecil, lalu setor (Merge) ke Main.

---

## 🛠 2. Setup Project

* **Format Save:** Project **HARUS** disimpan sebagai **"Save as project folder"**.
    * ❌ Dilarang: Save as single file (`.c3p`).
* **Ignored Files:** Pastikan file `.gitignore` sudah ada di root folder untuk memblokir file sampah:
    * `*.uistate.json` (Settingan editor lokal)
    * `*.autosave` & `*.backup`

---

## 🚧 3. Pembagian Modul (Rules of Engagement)

Agar aman, kita menerapkan sistem **Kavling Wilayah**:

### A. Event Sheet (Logika)
Jangan menumpuk logika di satu tempat. Gunakan **Include Event Sheet**.
* ✅ `ES_Global` (Hanya Lead yang boleh sentuh)
* ✅ `ES_MainMenu_Budi` (Hanya Budi yang boleh edit)
* ✅ `ES_RoadMap_Siti` (Hanya Siti yang boleh edit)

### B. Layout & Layer
* Jika sedang mengerjakan Layout A, jangan iseng menggeser objek di Layout B milik temanmu.
* Wajib Pake Layerin jangan suka numpuk, tidak scalable

### C. Menambah Aset/File Baru
* Jika kamu menambah **Global Variable**, **Plugin**, atau **Family** baru, **WAJIB BILANG DI GRUP CHAT**. Hal ini mengubah file induk secara drastis.

---

## 🔄 4. Rutinitas Harian (Daily Workflow)

Ikuti urutan ini setiap hari agar selamat dari konflik.

### ☀️ PAGI (Sebelum Mulai Coding)
Tujuannya: Mengambil update terbaru dari teman agar file project-mu tidak *outdated*.

1.  **Switch ke Main & Pull:**
    `git checkout main`
    `git pull origin main`
2.  **Update Branch Kamu:**
    `git checkout dev-namamu`
    `git merge main` (Menggabungkan update teman ke branch-mu)
3.  **Buka Construct 3:** Sekarang aman untuk mulai kerja.

### 🌙 SORE (Setelah Selesai / Fitur Jadi)
Tujuannya: Menyetor pekerjaanmu ke `main` agar teman lain kebagian update-mu.

1.  **Save Project.**
2.  **Cek Perubahan:** Lihat Git Client. Jika ada file layout temanmu berubah padahal kamu tidak menyentuhnya, **Discard/Revert** file itu.
3.  **Commit & Push:**
    `git add .`
    `git commit -m "Menambahkan fitur X"`
    `git push origin dev-namamu`
4.  **SETOR KE MAIN (Merge/Pull Request):**
    * Buka GitHub/GitLab.
    * Buat **Pull Request** dari `dev-namamu` ke `main`.
    * *Opsional:* Kabari tim untuk merge.

---

## 🚑 5. Penanganan Konflik (Emergency)

Jika terjadi **Merge Conflict** (biasanya di file `.json` atau `.c3proj`):

1.  **Jangan Panik.**
2.  **DILARANG** mengedit syntax JSON secara manual (kecuali paham strukturnya).
3.  **Pilih Salah Satu Versi (Resolve):**
    * Pilih *"Accept Yours"* (Pakai versimu) ATAU *"Accept Theirs"* (Pakai versi server).
4.  **Re-Create Manual:**
    * Jika kamu pilih "Accept Theirs", berarti codingan barumu hari itu hilang.
    * Buka Construct 3, lalu buat ulang logika yang hilang tersebut secara manual. Ini lebih aman daripada project rusak total.

---
