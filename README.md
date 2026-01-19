# README — Install & Remove Conda (Miniforge) + SageMath (Ubuntu)

Panduan ini memasang **Conda (Miniforge)** lalu **SageMath** dari **conda-forge**, dan juga cara menghapusnya. Referensi utama: dokumentasi instalasi SageMath via conda-forge dan panduan uninstall Miniforge/Conda. ([SageMath Documentation][1])

---

## 1) Install Conda (Miniforge)

### 1.1. Install dependensi kecil

```bash
sudo apt update
sudo apt install -y curl bzip2 ca-certificates
```

### 1.2. Download & jalankan installer Miniforge

```bash
cd ~
curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
bash Miniforge3-$(uname)-$(uname -m).sh
```

Saat installer bertanya:

* ketik `yes` untuk license
* lokasi install: Enter (default biasanya `~/miniforge3`)
* “initialize conda?” → pilih `yes`

### 1.3. Reload terminal & cek conda

Tutup terminal, buka lagi, lalu:

```bash
conda --version
```

Kalau masih `conda: command not found`, jalankan:

```bash
source ~/miniforge3/etc/profile.d/conda.sh
conda --version
```

---

## 2) Install SageMath

SageMath bisa diinstall dari channel **conda-forge**. ([SageMath Documentation][1])

### Opsi A (sesuai kemauan kamu): install di **base** (cukup `conda activate`)

```bash
conda activate
conda install -c conda-forge sage
```

Cek:

```bash
sage --version
sage
```

### Opsi B (lebih aman, tapi opsional): env terpisah

Kalau suatu saat kamu berubah pikiran (lebih aman dari konflik):

```bash
conda create -n sage sage
conda activate sage
sage --version
```

(Dicantumkan sebagai praktik umum di panduan instalasi Sage dari conda-forge.) ([SageMath Documentation][1])

---

## 3) Cara menjalankan script Sage (CTF kamu)

Kalau file kamu `solve.py` berisi `GF(...)` / `PolynomialRing(...)`, jalankan lewat Sage:

```bash
sage -python solve.py
```

Kalau file kamu `.sage`:

```bash
sage solve.sage
```

---

## 4) Menghapus SageMath

### Jika Sage diinstall di **base**

```bash
conda activate
conda remove sage
```

(`conda remove` adalah cara resmi untuk menghapus paket dari environment tertentu.) ([Conda Documentation][2])

### Jika Sage diinstall di env terpisah (mis. env bernama `sage`)

Hapus seluruh environment:

```bash
conda deactivate
conda env remove -n sage
```

(Perintah resmi untuk menghapus environment.) ([Conda Documentation][3])

---

## 5) Menghapus Conda (Miniforge) sepenuhnya

Panduan umumnya: hapus folder instalasi + undo perubahan `conda init` + bersihkan file/folder config. ([GitHub][4])

### 5.1. Matikan conda dulu

```bash
conda deactivate
```

### 5.2. Undo perubahan shell init (opsional tapi disarankan)

```bash
conda init --reverse --all
```

([Conda Documentation][5])

### 5.3. Hapus folder instalasi Miniforge

**Hati-hati** pastikan path-nya benar.

```bash
rm -rf ~/miniforge3
```

(Ini cara yang disarankan untuk uninstall conda di Linux: hapus direktori instalasinya.) ([Conda Documentation][5])

### 5.4. Bersihkan sisa file config (opsional)

```bash
rm -rf ~/.conda ~/.continuum
rm -f ~/.condarc
```

([Conda Documentation][5])

> Kalau kamu dulu install bukan di `~/miniforge3` (mis. `~/miniconda3` atau `~/anaconda3`), hapus folder yang sesuai.

---


