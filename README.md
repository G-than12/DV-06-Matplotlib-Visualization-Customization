# DV-06: Kustomisasi Visualisasi Matplotlib

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg?logo=python&logoColor=white)](https://www.python.org/)
[![Matplotlib](https://img.shields.io/badge/Matplotlib-Data%20Visualization-11557c.svg?logo=python&logoColor=white)](https://matplotlib.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458.svg?logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![NumPy](https://img.shields.io/badge/NumPy-Numerical%20Computing-013243.svg?logo=numpy&logoColor=white)](https://numpy.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626.svg?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![Status](https://img.shields.io/badge/Status-Completed-success.svg)](#)

Repositori ini berisi pengerjaan **Tugas Praktikum 5 (Pertemuan 6)** pada mata kuliah **Visualisasi Data** dengan topik **Kustomisasi Visualisasi (Label, Legenda, Subplot, Tema Warna)**. Seluruh tahapan praktikum, penyempurnaan grafik, simulasi *peer review*, implementasi revisi, latihan mandiri, dan penalaran pertanyaan diskusi diimplementasikan secara terstruktur dan dapat direproduksi (*reproducible*) di Jupyter Notebook.

---

## 👤 Identitas Mahasiswa

| Atribut | Keterangan |
| :--- | :--- |
| **Nama Mahasiswa** | Gathan Hilabi |
| **NIM** | 60324059 |
| **Kelas / Program Studi** | S1 Informatika |
| **Mata Kuliah** | Visualisasi Data |
| **Pertemuan** | 6 (Enam) |
| **Bentuk Penilaian** | Tugas Praktikum 5 (Bobot 3%) |
| **Topik** | Kustomisasi Visualisasi (Label, Legenda, Subplot, Tema Warna) |
| **Nama Reviewer (Peer Review)** | Ahmad Raihan |
| **Dataset** | Titanic Dataset (`seaborn-data` public repository) |

---

## 📁 Struktur Direktori

```text
VD_06/
├── Praktikum5_GathanHilabi_60324059.ipynb   # Notebook utama praktikum (lengkap dengan seluruh output grafik)
├── Praktikum6_GathanHilabi_60324059.ipynb   # Salinan notebook format Praktikum 6 (sesuai modul Colab)
├── PANDUAN_KUSTOMISASI_MATPLOTLIB.md        # Panduan komprehensif & cheatsheet kustomisasi Matplotlib
├── titanic_bersih.csv                      # Dataset hasil pembersihan (clean data)
├── Modul_Praktikum_Pertemuan6_Visualisasi_Data.pdf # Dokumen modul acuan resmi
└── README.md                               # Dokumentasi lengkap pengerjaan praktikum
```

> 📖 **Panduan Pembelajaran:** Untuk penjelasan mendalam mengenai prinsip desain visual, teori warna, hierarki *Object-Oriented API* Matplotlib, dan cheatsheet sintaks lengkap, silakan pelajari dokumen [PANDUAN_KUSTOMISASI_MATPLOTLIB.md](PANDUAN_KUSTOMISASI_MATPLOTLIB.md).

---

## 🎯 Tujuan Praktikum

1. **Menambahkan Legenda, Grid, dan Anotasi:** Mengintegrasikan elemen pendukung grafik agar visualisasi mampu "berbicara sendiri" (*self-explanatory*) kepada audiens.
2. **Menyusun Grid Subplot Multi-Dimensi:** Menyusun tata letak visualisasi yang lebih kompleks (grid 2x2) menggunakan pengindeksan array dua dimensi `axes[baris, kolom]`.
3. **Menerapkan Palet Warna Kustom & Gaya Visual:** Menggunakan kode warna heksadesimal (`#HEX`) bergaya *course branding* yang konsisten serta memahami penerapan tema bawaan Matplotlib (`plt.style.use()`).
4. **Penyempurnaan Grafik & Peer Review:** Menerapkan prinsip desain visual Tufte (*Data-to-Ink Ratio* dan eliminasi *chartjunk*), mengevaluasi grafik bersama rekan sejawat (*peer review*), dan melakukan revisi nyata berdasarkan masukan.

---

## 🛠️ Ringkasan Alur Praktikum (Langkah 1 - 9)

1. **Langkah 1 - Menyiapkan Notebook & Memuat Ulang Data Bersih:**
   - Memuat dataset Titanic dari GitHub `seaborn-data`.
   - Menjalankan pipeline pembersihan data dari Pertemuan 3: imputasi missing value `age` dengan rata-rata, eliminasi baris kosong `embarked`, dan pembersihan duplikasi, menghasilkan **782 baris data bersih**.
2. **Langkah 2 - Membuat Grafik Berkelompok (*Grouped Bar*) dengan Legenda:**
   - Membangun *pivot table* tingkat keselamatan per kelas tiket (`pclass`) dan gender (`sex`).
   - Menyusun dua batang berdampingan dengan pergeseran offset `x - width/2` dan `x + width/2`.
   - Mengaktifkan `ax.legend(title="Jenis Kelamin")` dan grid vertikal lembut (`alpha=0.3`).
3. **Langkah 3 - Menata Grid dan Sumbu:**
   - Menampilkan rata-rata tarif tiket (*fare*) per kelas dengan garis berpenanda (*marker* `o`).
   - Menerapkan garis kisi putus-putus (`linestyle="--"`, `alpha=0.4`), penguncian batas sumbu Y (`ax.set_ylim(0, 100)`), serta menghilangkan garis tepi kotak atas dan kanan (*despine*).
4. **Langkah 4 - Membuat Grid Subplot 2x2:**
   - Menyusun 4 visualisasi data dalam satu figur 2 baris × 2 kolom:
     - `axes[0,0]`: Line chart rata-rata fare per kelas.
     - `axes[0,1]`: Bar chart tingkat selamat per jenis kelamin.
     - `axes[1,0]`: Scatter plot usia vs tarif tiket.
     - `axes[1,1]`: Histogram distribusi usia penumpang.
   - Menggunakan `plt.tight_layout()` untuk mencegah *clipping* atau overlap label.
5. **Langkah 5 - Menggunakan Palet Warna Kustom:**
   - Menerapkan palet warna bergaya *course branding* (`["#0B5D7A", "#16849E", "#E8834A"]`) pada bar chart distribusi penumpang kelas 1, 2, dan 3.
6. **Langkah 6 - Menggunakan Gaya (*Style*) Matplotlib:**
   - Memanfaatkan preset tema `seaborn-v0_8-whitegrid` dan mengembalikan ke `plt.style.use("default")` agar tidak merusak formatting sel berikutnya.
7. **Langkah 7 - Menyempurnakan Grafik dari Pertemuan 5:**
   - **Bar Chart:** Menyematkan anotasi persentase dinamis `:.1%` tepat di atas setiap batang (`ax.text()`), warna palet kustom, grid Y, dan menghapus spines (sama persis dengan kode modul).
   - **Line Chart:** Menambahkan elemen kustomisasi (warna kustom `#0B5D7A`, marker `o`, anotasi nilai tarif di atas titik, grid putus-putus, penguncian rentang sumbu Y, dan menghapus spines).
   - **Scatter Plot:** Membagi warna titik berdasarkan kategori keselamatan (oranye `#E8834A` untuk tidak selamat vs teal `#16849E` untuk selamat), legenda informatif, grid halus, dan menghapus spines.
8. **Langkah 8 - Sesi Peer Review:**
   - Pengisian lembar checklist evaluasi bersama reviewer (Ahmad Raihan) mencakup evaluasi judul, label, legenda, kontras warna, hal terbaik, dan saran perbaikan.
9. **Langkah 9 - Revisi Berdasarkan Masukan Reviewer & Ringkasan Kustomisasi:**
   - Merevisi scatter plot dengan menambahkan garis rata-rata tarif kapal (`ax.axhline`) sebagai garis acuan komparasi data.
   - Menyajikan sel ringkasan kustomisasi visual secara ringkas dan terstruktur.

---

## 💡 Dokumentasi Latihan Mandiri (Latihan 1 - 5)

| No | Latihan | Deskripsi Implementasi & Temuan Analisis |
| :---: | :--- | :--- |
| **1** | **Grouped Bar Chart Jumlah Penumpang per Pelabuhan & Kelas** | Pivot table `aggfunc="count"` dengan offset batang proporsional dan anotasi nilai pasti di atas batang (*direct data labeling*). Menunjukkan dominasi mutlak penumpang asal Southampton di Kelas 3 (296 orang), kaum elit Kelas 1 di Cherbourg (83 orang), dan arus imigran pekerja Kelas 3 di Queenstown (54 orang). |
| **2** | **Subplot 1x2 Histogram Usia (Selamat vs Tidak Selamat)** | Dibangun dengan `sharey=True` untuk komparasi frekuensi yang jujur tanpa distorsi skala. Dilengkapi garis rata-rata (`ax.axvline`) dan median usia pada masing-masing kelompok (rata-rata 28.4 th selamat vs 30.6 th tidak selamat). Mengungkap lonjakan keselamatan balita/anak-anak (0–5 th) sebagai bukti empiris protokol *"women and children first"*. |
| **3** | **Perbandingan Gaya Visual Matplotlib (`ggplot` vs `seaborn-v0_8-whitegrid`)** | Menguji coba dua tema visual menggunakan `plt.style.context()`. Gaya `ggplot` menonjolkan kanvas abu-abu bergaris putih tebal (cocok untuk presentasi layar), sedangkan `seaborn-v0_8-whitegrid` memiliki kanvas putih bersih dengan grid abu-abu tipis (dipilih sebagai yang paling optimal karena memaksimalkan *Data-Ink Ratio* dan *zero chartjunk*). |
| **4** | **Bar Chart dengan Garis Acuan Rata-rata Total (`ax.axhline`)** | Menampilkan tingkat keselamatan Kelas 1 (62.6%), Kelas 2 (47.3%), dan Kelas 3 (24.2%) berbanding garis benchmark kapal (41.0%). Dilengkapi pewarnaan bersyarat (*conditional colors*: toska di atas rata-rata vs merah karang di bawah rata-rata) serta kotak anotasi penjelas di samping garis. |
| **5** | **Set Warna Kustom Bertema Sendiri pada 2 Grafik Berbeda** | Merancang palet bertema **"Nautical Ocean Heritage"** (`#1D3557` Deep Navy, `#457B9D` Steel Blue, `#A8DADC` Iceberg Mint, `#E63946` Coral Amber). Diterapkan secara konsisten pada: (1) *Horizontal Bar Chart* tingkat keselamatan per 4 kelompok usia; serta (2) *Donut Chart* proporsi penumpang berdasarkan 3 pelabuhan keberangkatan. |

---

## 💬 Ringkasan Pertanyaan Diskusi

1. **Elemen Paling Berpengaruh terhadap Kemudahan Membaca Grafik:**
   - **Anotasi Data Langsung (*Direct Data Labeling*):** Menghilangkan beban kognitif pembaca untuk mengira-ngira nilai dari sumbu numerik vertikal.
   - **Judul Berorientasi Pesan (*Action Title*):** Memandu fokus pemikiran pembaca sejak awal mengenai kesimpulan utama yang ingin disampaikan.
2. **Masukan Peer Review yang Paling Bermanfaat:**
   - Penambahan garis rata-rata tarif kapal pada grafik scatter plot usia vs tarif sebagai garis acuan komparasi data.
3. **Risiko Desain Grafik Terlalu "Ramai" (*Chartjunk*):**
   - Menurunkan rasio *Data-to-Ink*, memicu kelebihan beban kognitif (*cognitive overload*), mengaburkan pesan utama data, membuat teks bertumpuk (*unreadable*), dan mengurangi kredibilitas profesional analisis.

---

## 🚀 Cara Menjalankan Notebook

### 1. Menjalankan Secara Lokal (Jupyter Notebook / VS Code)
Pastikan lingkungan Python telah terpasang paket data science:
```bash
pip install pandas numpy matplotlib jupyter
```
Buka file notebook:
```bash
jupyter notebook Praktikum5_GathanHilabi_60324059.ipynb
```

### 2. Menjalankan di Google Colab
1. Buka [Google Colab](https://colab.research.google.com/).
2. Pilih tab **Upload** dan unggah file `Praktikum5_GathanHilabi_60324059.ipynb` atau `Praktikum6_GathanHilabi_60324059.ipynb`.
3. Jalankan sel berurutan dengan menekan tombol **Shift + Enter**. Seluruh grafik dan data akan tampil secara instan.

---

*Repositori ini dikerjakan dengan standar akademik dan profesional tinggi sebagai pemenuhan Tugas Praktikum Mata Kuliah Visualisasi Data.*
