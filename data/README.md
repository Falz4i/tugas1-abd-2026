# Data Tugas 1

## Dataset yang Dipilih

| Item | Isi |
|---|---|
| Nama dataset | Indonesia News |
| Sumber | [Kaggle — azizainunnajib/indonesia-news](https://www.kaggle.com/datasets/azizainunnajib/indonesia-news) |
| Lisensi/ketentuan pakai | [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/): boleh digunakan dan diadaptasi untuk tujuan nonkomersial dengan atribusi kepada pembuat dataset. |
| Ukuran | Sekitar 2,16 GB (3 file CSV), sehingga memenuhi syarat minimal 500 MB. |
| Periode data | Hasil profiling: 4 Agustus 2014–31 Mei 2020 (timestamp epoch ditafsirkan sebagai UTC). Nama file tambahan Tempo mengacu Juni 2019–Mei 2020; timestampnya kurang presisi. |
| Unit analisis | Satu baris mewakili satu artikel berita dari CNN Indonesia atau Tempo. |

## Berkas Dataset

Metadata Kaggle mencantumkan tiga file berikut:

| Nama file | Ukuran perkiraan | Keterangan |
|---|---:|---|
| `cnn.csv` | 842,40 MB | Kumpulan artikel CNN Indonesia. |
| `tempo.csv` | 1,07 GB | Kumpulan artikel Tempo. |
| `tempo010619310520.csv` | 247,96 MB | Artikel Tempo untuk periode 1 Juni 2019–31 Mei 2020. |

Ukuran dan jumlah baris akan diperiksa kembali setelah file diunduh karena ukuran yang ditampilkan Kaggle dapat berbeda antara arsip unduhan dan file hasil ekstraksi.

## Hasil verifikasi revisi 26 Oktober 2026

Pembacaan CSV ketat menghasilkan **988.814 baris**. Cleaning terbaru menghasilkan **848.028 baris**, menggantikan hasil lama 964.553 baris yang memakai kunci timestamp.

| Tahap pengeluaran baris (berurutan) | Jumlah |
|---|---:|
| Judul/isi wajib kosong | 14.313 |
| Tanggal tidak valid setelah pemeriksaan teks | 4 |
| Isi kurang dari 100 karakter setelah pemeriksaan tanggal | 7.384 |
| Duplikat sumber + judul + hash isi | 119.085 |
| Total dikeluarkan | 140.786 |

Audit menemukan 117.022 kelompok artikel Tempo lintas file. Prioritas salinan diberikan kepada `tempo.csv`; artikel dengan revisi isi tetap dipertahankan. Pencilan panjang isi berdasarkan IQR per media ditandai, tanpa clipping teks. Ambang 100 karakter adalah asumsi operasional yang perlu dievaluasi, bukan definisi universal artikel valid.

Notebook 02 menyimpan audit CSV, metadata versi, dan `indonesia_news_clean.parquet` di `data/processed/`. Notebook 03 memeriksa metadata tersebut sebelum membuat analisis ulang. Berkas antara `_news_*.parquet` dapat diregenerasi oleh notebook 02; tidak termasuk bahan commit.

## Rencana Analisis

Dataset ini akan digunakan untuk menganalisis karakteristik dan perkembangan pemberitaan Indonesia. Profiling awal akan memeriksa struktur kolom, rentang tanggal, sumber berita, nilai kosong, duplikasi artikel, dan konsistensi teks. Analisis lanjutan dapat mencakup jumlah artikel dari waktu ke waktu, perbandingan sumber berita, distribusi panjang artikel, kata atau topik yang sering muncul, serta perubahan topik sepanjang periode data.

## Tempat Mencari Dataset

Pilih dataset Indonesia yang legal digunakan, dapat didokumentasikan sumbernya, dan memenuhi batas ukuran tugas.

| Situs | Kegunaan |
|---|---|
| [Satu Data Indonesia](https://data.go.id/) | Portal data terbuka lintas instansi pemerintah Indonesia. |
| [Badan Pusat Statistik](https://www.bps.go.id/) | Statistik sosial, ekonomi, kependudukan, dan data wilayah. |
| [BMKG Data Online](https://dataonline.bmkg.go.id/) | Data cuaca, iklim, gempa bumi, dan observasi meteorologi. |
| [Hugging Face Datasets](https://huggingface.co/datasets) | Dataset publik yang dapat dicari berdasarkan topik, bahasa, atau ukuran. |
| [Kaggle Datasets](https://www.kaggle.com/datasets) | Katalog dataset publik; periksa lisensi dan dokumentasi pembuatnya. |
| [Google Dataset Search](https://datasetsearch.research.google.com/) | Mesin pencari untuk menemukan dataset dari berbagai portal. |

## Cara Memperoleh Data

1. Login ke Kaggle dan buka halaman [Indonesia News](https://www.kaggle.com/datasets/azizainunnajib/indonesia-news).
2. Klik **Download**, lalu ekstrak arsip ke folder `data/raw/archive/`.
3. Pertahankan nama dan isi file mentah tanpa perubahan.
4. Catat checksum setiap file setelah pengunduhan, misalnya di PowerShell dengan `Get-FileHash data/raw/archive/*.csv -Algorithm SHA256`.
5. Notebook `notebooks/01_data_profiling.ipynb` membaca ketiga file CSV dari folder `data/raw/archive/`.

## Aturan Penyimpanan

- Jangan commit dataset mentah atau hasil olahan berukuran besar ke Git.
- File pada `data/raw/` adalah data asli dan tidak boleh diubah.
- Simpan hasil transformasi yang dapat direproduksi pada `data/processed/`.
