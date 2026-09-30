# Data Tugas 1

## Dataset yang Dipilih

| Item | Isi |
|---|---|
| Nama dataset | Indonesia News |
| Sumber | [Kaggle — azizainunnajib/indonesia-news](https://www.kaggle.com/datasets/azizainunnajib/indonesia-news) |
| Lisensi/ketentuan pakai | [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/): boleh digunakan dan diadaptasi untuk tujuan nonkomersial dengan atribusi kepada pembuat dataset. |
| Ukuran | Sekitar 2,16 GB (3 file CSV), sehingga memenuhi syarat minimal 500 MB. |
| Periode data | Dataset memuat arsip berita hingga 31 Mei 2020. File `tempo010619310520.csv` menunjukkan periode 1 Juni 2019–31 Mei 2020; rentang tanggal penuh seluruh file akan diverifikasi pada tahap profiling. |
| Unit analisis | Satu baris mewakili satu artikel berita dari CNN Indonesia atau Tempo. |

## Berkas Dataset

Metadata Kaggle mencantumkan tiga file berikut:

| Nama file | Ukuran perkiraan | Keterangan |
|---|---:|---|
| `cnn.csv` | 842,40 MB | Kumpulan artikel CNN Indonesia. |
| `tempo.csv` | 1,07 GB | Kumpulan artikel Tempo. |
| `tempo010619310520.csv` | 247,96 MB | Artikel Tempo untuk periode 1 Juni 2019–31 Mei 2020. |

Ukuran dan jumlah baris akan diperiksa kembali setelah file diunduh karena ukuran yang ditampilkan Kaggle dapat berbeda antara arsip unduhan dan file hasil ekstraksi.

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
2. Klik **Download**, lalu ekstrak arsip ke folder `data/raw/indonesia-news/`.
3. Pertahankan nama dan isi file mentah tanpa perubahan.
4. Catat checksum setiap file setelah pengunduhan, misalnya di PowerShell dengan `Get-FileHash data/raw/indonesia-news/*.csv -Algorithm SHA256`.
5. Atur variabel `DATA_PATH` pada `notebooks/01_data_profiling.ipynb` agar menunjuk ke file yang dianalisis, misalnya `data/raw/indonesia-news/cnn.csv`.

## Aturan Penyimpanan

- Jangan commit dataset mentah atau hasil olahan berukuran besar ke Git.
- File pada `data/raw/` adalah data asli dan tidak boleh diubah.
- Simpan hasil transformasi yang dapat direproduksi pada `data/processed/`.
