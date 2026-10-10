# Panduan Komprehensif Kustomisasi Visualisasi Data dengan Matplotlib

Dokumen ini merupakan panduan teknis, konseptual, dan cheatsheet sintaks lengkap untuk kustomisasi visualisasi data menggunakan pustaka **Matplotlib** di Python, yang dirancang untuk mendukung pengerjaan praktikum pada mata kuliah **Visualisasi Data**.

---

## 📑 Daftar Isi
1. [Prinsip Desain Visual & Anti-Chartjunk](#1-prinsip-desain-visual--anti-chartjunk)
2. [Hierarki Objek Matplotlib (Figure & Axes)](#2-hierarki-objek-matplotlib-figure--axes)
3. [Cheatsheet Elemen Kustomisasi Grafik](#3-cheatsheet-elemen-kustomisasi-grafik)
   - [3.1 Judul dan Label Sumbu](#31-judul-dan-label-sumbu)
   - [3.2 Legenda (Legend)](#32-legenda-legend)
   - [3.3 Grid dan Skala Sumbu](#33-grid-dan-skala-sumbu)
   - [3.4 Spines (Garis Tepi Kotak Grafik)](#34-spines-garis-tepi-kotak-grafik)
   - [3.5 Anotasi Teks dan Panah (Direct Labeling)](#35-anotasi-teks-dan-panah-direct-labeling)
4. [Tata Letak Multi-Plot (Subplot Grid 2D)](#4-tata-letak-multi-plot-subplot-grid-2d)
5. [Teori Warna dan Palet Kustom (HEX)](#5-teori-warna-dan-palet-kustom-hex)
6. [Gaya Visual Bawaan (Matplotlib Styles)](#6-gaya-visual-bawaan-matplotlib-styles)
7. [Matriks Pemecahan Masalah (Troubleshooting)](#7-matriks-pemecahan-masalah-troubleshooting)

---

## 1. Prinsip Desain Visual & Anti-Chartjunk

Grafik yang baik adalah grafik yang mampu **"berbicara sendiri"** (*self-explanatory*) kepada pembaca tanpa memerlukan penjelasan verbal tambahan.

### A. Rasio Data-ke-Tinta (*Data-to-Ink Ratio*)
Dipelopori oleh **Edward Tufte**, prinsip ini menyatakan bahwa proporsi tinta (piksel visual) yang digunakan untuk menampilkan substansi data harus dimaksimalkan:
$$\text{Data-to-Ink Ratio} = \frac{\text{Tinta Data}}{\text{Total Tinta Visual}}$$
- **Tinta Data:** Batang histogram, garis tren, titik sebaran, label data.
- **Tinta Non-Data:** Garis grid tebal hitam, efek bayangan 3D, dekorasi border ganda, ornamen latar belakang.
- **Tujuan:** Kurangi tinta non-data yang tidak menambah nilai analisis informasi.

### B. Menghindari *Chartjunk*
*Chartjunk* adalah segala elemen visual dekoratif yang berlebihan dan tidak membawa makna statistik, yang justru mengalihkan perhatian pembaca dari substansi data.
- ❌ **Hindari:** Grafik batang 3D, latar belakang bermotif/bergambar, penggunaan lebih dari 5 warna acak pada grafik kategori tunggal.
- ✔️ **Terapkan:** Desain minimalis (*flat design*), garis grid semi-transparan (`alpha=0.2–0.4`), penyembunyian batas tepi atas dan kanan (*despine*).

---

## 2. Hierarki Objek Matplotlib (Figure & Axes)

Matplotlib mengadopsi pendekatan berorientasi objek (*Object-Oriented API*) yang memisahkan kanvas utama dan bidang gambar:

```text
Figure (Kanvas Induk)
 └── Axes (Bidang Koordinat Data)
      ├── Title (Judul)
      ├── XAxis / YAxis (Sumbu & Ticks)
      ├── Spines (Garis Kotak)
      ├── Legend (Legenda)
      └── Data Elements (Bars, Lines, Scatters, Patches)
```

**Praktik Terbaik:** Gunakan selalu antarmuka *Object-Oriented* (`fig, ax = plt.subplots()`) alih-alih `plt.plot()` prosedural agar modifikasi setiap elemen bersifat terisolasi dan presisi.

---

## 3. Cheatsheet Elemen Kustomisasi Grafik

### 3.1 Judul dan Label Sumbu
Judul harus berorientasi pada pesan (*action title*), dan sumbu wajib mencantumkan satuan data jika relevan:

```python
# Judul utama figur
ax.set_title("Tingkat Keselamatan Berdasarkan Jenis Kelamin", fontsize=12, fontweight="bold", pad=12)

# Label sumbu X dan Y beserta satuan
ax.set_xlabel("Kelas Tiket Penumpang (pclass)", fontsize=10, labelpad=8)
ax.set_ylabel("Proporsi Selamat (%)", fontsize=10, labelpad=8)
```

### 3.2 Legenda (Legend)
Legenda wajib disertakan jika grafik menampilkan lebih dari satu kelompok kategori atau seri data:

```python
# Legenda otomatis mengambil label='...' dari plot
ax.legend(
    title="Jenis Kelamin",
    loc="upper right",          # Posisi: 'upper left', 'upper right', 'lower left', 'center'
    frameon=True,               # Menampilkan kotak bingkai legenda
    facecolor="white",          # Warna latar kotak
    edgecolor="#e0e0e0",        # Garis tepi halus
    fontsize=9
)
```

### 3.3 Grid dan Skala Sumbu
Grid membantu pembaca mengestimasi nilai tanpa membebani mata:

```python
# Grid halus horizontal dengan transparansi rendah
ax.grid(axis="y", linestyle="--", linewidth=0.8, alpha=0.35)

# Mengunci batas rentang sumbu agar komparasi adil
ax.set_ylim(0, 1.0)             # Rentang 0 sampai 100%
ax.set_xlim(0, 80)              # Rentang usia 0 sampai 80 tahun

# Garis referensi pembanding (misal: rata-rata keseluruhan)
ax.axhline(0.41, color="#D9381E", linestyle="--", linewidth=1.8, label="Rata-rata Total (41%)")
ax.axvline(29.7, color="#004D40", linestyle=":", linewidth=1.8, label="Rata-rata Usia (29.7 th)")
```

### 3.4 Spines (Garis Tepi Kotak Grafik)
Menghilangkan garis tepi atas dan kanan (*despine*) memberikan tampilan modern dan bersih:

```python
# Menyembunyikan border atas dan kanan
ax.spines["top"].set_visible(False)
ax.spines["right"].set_visible(False)

# Mengubah warna atau ketebalan border bawah dan kiri
ax.spines["left"].set_color("#666666")
ax.spines["bottom"].set_color("#666666")
```

### 3.5 Anotasi Teks dan Panah (Direct Labeling)
Anotasi langsung di atas elemen grafik menghilangkan kebutuhan menatap sumbu bolak-balik:

```python
# 1. Anotasi pada batang Bar Chart
for bar in bars:
    height = bar.get_height()
    ax.text(
        bar.get_x() + bar.get_width() / 2,   # Posisi X tengah batang
        height + 0.02,                       # Posisi Y sedikit di atas puncak
        f"{height:.1%}",                     # Format persentase 1 desimal
        ha="center", va="bottom",
        fontweight="bold", fontsize=9.5
    )

# 2. Anotasi dengan panah penunjuk (Outlier / Highlight)
ax.annotate(
    "Tarif VIP Tertinggi ($512.33)\nUsia: 35 th",
    xy=(35, 512.33),                         # Titik target yang ditunjuk
    xytext=(20, 420),                        # Titik letak teks label
    arrowprops=dict(facecolor="#0B5D7A", edgecolor="none", arrowstyle="->", lw=1.5),
    fontsize=9, fontweight="bold", color="#0B5D7A"
)
```

---

## 4. Tata Letak Multi-Plot (Subplot Grid 2D)

Ketika menyusun beberapa grafik dalam satu kanvas matriks (misal 2 baris × 2 kolom):

```python
fig, axes = plt.subplots(2, 2, figsize=(10, 7))

# Matriks axes berupa array 2 Dimensi:
# axes[0, 0] -> Baris 0, Kolom 0 (Kiri Atas)
# axes[0, 1] -> Baris 0, Kolom 1 (Kanan Atas)
# axes[1, 0] -> Baris 1, Kolom 0 (Kiri Bawah)
# axes[1, 1] -> Baris 1, Kolom 1 (Kanan Bawah)

axes[0, 0].plot(...)
axes[0, 1].bar(...)
axes[1, 0].scatter(...)
axes[1, 1].hist(...)

# Wajib: merapikan jarak antar subplot agar tidak bertumpuk
plt.tight_layout()
plt.show()
```

---

## 5. Teori Warna dan Palet Kustom (HEX)

Warna dalam visualisasi data berfungsi untuk **menyampaikan informasi**, bukan sekadar hiasan.

### A. Tiga Jenis Palet Data
1. **Kategorikal (*Qualitative*):** Untuk membedakan grup tanpa urutan implisit (contoh: Laki-laki vs Perempuan, Pelabuhan Asal). Gunakan warna dengan *hue* (corak) yang kontras.
2. **Sekuensial (*Sequential*):** Untuk data numerik berurutan dari rendah ke tinggi (contoh: Tarif $0 ke $500). Gunakan gradasi saturasi dari terang ke gelap.
3. **Divergen (*Diverging*):** Untuk data dengan titik tengah kritis (contoh: Surplus vs Defisit). Gunakan dua warna kontras yang bertemu di titik netral netral abu-abu/putih.

### B. Palet Brand Praktikum (*Course Branding*)
```python
palet_course = ["#0B5D7A", "#16849E", "#E8834A"]
# #0B5D7A : Deep Ocean Navy (Warna primer tegas)
# #16849E : Mediterranean Teal (Warna sekunder stabil)
# #E8834A : Coral Amber (Warna kontras/aksen hangat)
```

### C. Palet Kustom Bertema Sendiri (*Nordic Sea Breeze*)
```python
palet_nordic = ["#1D3557", "#457B9D", "#A8DADC", "#E63946"]
# #1D3557 : Deep Navy
# #457B9D : Slate Blue
# #A8DADC : Soft Ice
# #E63946 : Vivid Coral (Highlight)
```

---

## 6. Gaya Visual Bawaan (Matplotlib Styles)

Matplotlib menyediakan preset gaya visual siap pakai:

```python
# Menampilkan semua tema yang tersedia
print(plt.style.available)

# Menggunakan tema secara global (mempengaruhi seluruh notebook):
plt.style.use("seaborn-v0_8-whitegrid")

# Menggunakan tema secara lokal dengan Context Manager (Sangat Direkomendasikan!):
with plt.style.context("ggplot"):
    fig, ax = plt.subplots()
    ax.bar(...)
    plt.show()

# Mereset kembali ke gaya default:
plt.style.use("default")
```

---

## 7. Matriks Pemecahan Masalah (Troubleshooting)

| Gejala Masalah | Penyebab Umum | Solusi Perbaikan |
| :--- | :--- | :--- |
| **Legenda tidak muncul** | Parameter `label=` tidak disematkan pada pemanggilan fungsi plot, atau `ax.legend()` lupa dipanggil. | Tambahkan `label="Nama Seri"` pada setiap `ax.bar()`/`ax.plot()` dan panggil `ax.legend()` sebelum `plt.show()`. |
| **Error `IndexError: too many indices for array` atau `TypeError: 'Axes' object is not subscriptable`** | Kesalahan akses dimensi pada grid subplot (misal mengakses `axes[0]` pada grid 2x2, atau `axes[0,0]` pada grid 1x2). | Periksa bentuk grid: jika 2x2 gunakan `axes[row, col]`, jika 1x2 atau 1x3 gunakan `axes[col]`. |
| **Gaya tema "menempel" ke semua sel berikutnya** | `plt.style.use()` mengubah konfigurasi global runtime `matplotlib.rcParams`. | Jalankan `plt.style.use("default")` di akhir sel, atau gunakan `with plt.style.context('nama_style'):`. |
| **Label sumbu / judul terpotong atau saling bertumpuk** | Kanvas terlalu sempit atau margin subplot tidak disesuaikan. | Perbesar ukuran figur `figsize=(width, height)` dan selalu tambahkan `plt.tight_layout()` sebelum `plt.show()`. |
| **Warna kategori sulit dibedakan saat dicetak abu-abu (*grayscale*)** | Pemilihan warna hanya berbeda corak (*hue*) tetapi memiliki kecerahan (*luminance*) yang sama persis. | Gunakan palet yang memiliki variasi tingkat terang-gelap (*lightness contrast*) atau tambahkan pola penanda (*markers/hatches*). |

---

*Disusun untuk Praktikum Visualisasi Data — Modul Pertemuan 6 (Kustomisasi Matplotlib).*
