# Movie Analytics: laporan Power BI IMDB Top 1000

Proyek belajar sekaligus etalase **Power BI**: 4 halaman laporan (Genre & Year, Rating, Director Analysis, Dashboard) di atas model data dengan tabel jembatan **Movie Genre** untuk relasi banyak-ke-banyak antara film dan genre. Tiap halaman memakai satu keluarga visual: column, bar, dan line; scatter; matriks; lalu kartu KPI di dashboard penutup.


## Dataset

`imdb_top_1000`: **999 film** dari daftar IMDB Top 1000, dirilis **1920–2020**. Kolom utama: Series_Title, Released_Year, Certificate, Runtime, Genre, IMDB_Rating, Meta_score, Director, Star1–Star4, No_of_Votes, dan Gross.

### Model data

| Tabel | Baris | Fungsi |
|---|---|---|
| `imdb_top_1000` | 999 | Tabel fakta film (dengan `MovieID` MOV001 dst.) |
| `Genre` | 21 | Daftar genre unik (`GenreID` GEN001 dst.) |
| `Movie Genre` | 2.538 | Tabel jembatan `MovieID` ↔ `GenreID`, karena satu film bisa punya beberapa genre |
| `Category` | 3 | Daftar field: Genre, Released_Year, Director |
| `imdb_top_10001` | 1.000 | Salinan mentah dataset (Runtime masih teks seperti "153 min") |

Kolom `Genre` asli berisi beberapa genre dalam satu sel ("Action, Crime, Drama"). Tabel jembatan memecahnya, sehingga hitungan per genre menjumlah lebih dari 999 (total 2.538 pasangan film-genre).

**Kualitas data:** `Gross` kosong di 169 film dan `Meta_score` di 157 film. Ada beberapa teks yang rusak encoding-nya (contoh "SÃ¼leyman" untuk "Süleyman").

## 1. Genre & Year: column, bar, dan line chart

![Genre dan tahun](chart/Movie%20Analytics-1.png)

**Temuan utama:**

- **Drama** menguasai daftar: 723 dari 999 film (sekitar 72%), jauh di atas Comedy (233), Crime (209), Adventure (195), dan Action (189).
- Rata-rata rating antar genre nyaris sama, hanya berkisar **7,89 (Horror) sampai 8,01 (War)**. Semua film di daftar ini sudah berating minimal 7,6, sehingga sumbu bar chart dipotong mulai 7,6 agar bedanya terlihat. 
- Jumlah film per tahun naik tajam setelah 1990: puncaknya **2014 dengan 32 film**. Per dekade, 2010-an (242) dan 2000-an (237) terbanyak. Tahun 2020 hanya 6 film, jadi garis turun di ujung kanan lebih karena data 2020 belum lengkap.
- Rata-rata rating per tahun lebih tinggi dan lebih fluktuatif di era awal (sedikit film per tahun), lalu mengecil dan stabil sekitar 7,9 di era modern.

## 2. Rating: tiga scatter chart

![Rating dan variabel lain](chart/Movie%20Analytics-2.png)

**Temuan utama:**

- **Rating vs jumlah vote** punya korelasi sedang (r = 0,50): film berating tinggi cenderung lebih banyak ditonton dan dinilai. Film dengan vote terbanyak adalah *The Shawshank Redemption* (2,34 juta vote, rating 9,3).
- **Rating vs Runtime** korelasinya lemah (r = 0,24): film lebih panjang sedikit lebih tinggi ratingnya, tetapi pola itu tidak kuat. Film terpanjang adalah *Gangs of Wasseypur* (321 menit).
- **Rating vs Gross** hampir tidak berkorelasi (r = 0,10, dihitung pada 830 film yang punya data Gross). Rating tinggi tidak menjamin pendapatan besar. Film dengan Gross tertinggi adalah *Star Wars: Episode VII* ($936,7 juta) yang ratingnya "hanya" 7,9.

## 3. Director Analysis: matriks per sutradara

![Matriks sutradara](chart/Movie%20Analytics-3.png)

**Temuan utama:**

- Matriks memuat **548 sutradara** dengan kolom jumlah film, rata-rata rating, median Gross, total vote, dan rata-rata durasi. Gambar di atas hanya 15 teratas berdasarkan jumlah film.
- Sutradara dengan film terbanyak: **Alfred Hitchcock (14)**, **Steven Spielberg (13)**, dan **Hayao Miyazaki (11)**.
- Di antara sutradara dengan minimal 3 film, rata-rata rating tertinggi dipegang **Christopher Nolan (8,46)**, lalu Peter Jackson dan Francis Ford Coppola (masing-masing 8,40). Nolan juga punya total vote terbanyak (11,6 juta) di antara semuanya.
- Jika dijumlahkan, film Spielberg menghasilkan Gross terbesar (sekitar $2,48 miliar). Angka ini dihitung terpisah dari data karena matriks aslinya menampilkan median, bukan total.

## 4. Dashboard: ringkasan

![Dashboard](chart/Movie%20Analytics-4.png)

**Temuan utama:**

- Lima kartu KPI di atas: **999** film, rata-rata rating **7,95**, total **273 juta** vote, rata-rata durasi **123 menit**, dan total Gross **$56,4 miliar**.
- Histogram rating menunjukkan distribusi menurun tajam: puncaknya di 7,7 (157 film), hanya **53 film** berating 8,5 ke atas, dan hanya 5 film di atas 8,9 (9,0: 3 film, 9,2: 1 film, 9,3: 1 film).
- Ringkasan lini masa dan genre di bawahnya mengulang temuan halaman 1, sehingga dasbor bisa dipakai sendiri tanpa membuka halaman lain.


