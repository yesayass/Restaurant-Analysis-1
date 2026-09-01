# Restaurant-Analysis-1
Analysis Sales Restaurant 2026


# Analisis Peringkat Restoran

## Daftar Isi

*[Studi Kasus](#studi kasus)
* [Deskripsi Kumpulan Data](#deskripsi-dataset)
* [Diagram ER](#diagram er)
* [Pembersihan Data](#pembersihan data)
* [Analisis Data](#analisis data)
* [Dasbor](#dasbor)

## Studi Kasus
Peringkat restoran di Meksiko oleh konsumen sebenarnya mulai tahun 2012, termasuk informasi tambahan tentang setiap restoran dan masakannya, serta setiap konsumen dan preferensinya.
## Deskripsi Kumpulan Data
Kumpulan data kami terdiri dari pengamatan berikut yang meliputi:

#### Konsumen
- **Consumer_ID** - Pengidentifikasi unik untuk setiap konsumen
- **Kota** - Kota tempat tinggal konsumen
- **Negara Bagian** - refleksi tempat tinggal konsumen
- **Negara** - Negara tempat tinggal konsumen
- **Lintang** - Lintang tempat tinggal konsumen
- **Bujur** - Bujur tempat tinggal konsumen
- **Perokok** - Apakah konsumen merokok atau tidak
- **Drink_Level** - Apakah konsumen adalah peminum yang menyerah, santai, atau suka bersosialisasi
- **Metode_Transportasi** - Apakah konsumen melakukan transportasi dengan berjalan kaki, dengan angkutan umum, atau dengan mobil
- **Marital_Status** - Status perkawinan konsumen (lajang atau menikah)
- **Anak-anak** - Apakah konsumen memiliki anak atau anak yang menjadi tanggungan/mandiri
- **Usia** - Usia konsumen
- **Pekerjaan** - Pekerjaan konsumen (pelajar, bekerja, atau menganggur)
- **Anggaran** - Anggaran konsumen (rendah, sedang, tinggi)

#### Preferensi_Konsumen
- **Consumer_ID** - Pengidentifikasi unik untuk setiap konsumen
- **Masakan_Pilihan** - Jenis makanan yang disukai konsumen

#### Peringkat
- **Consumer_ID** - Pengidentifikasi unik untuk setiap konsumen
- **Restaurant_ID** - Pengidentifikasi unik untuk setiap restoran
- **Peringkat_Keseluruhan** - Peringkat keseluruhan konsumen untuk restoran tersebut (0=Tidak Memuaskan, 1=Memuaskan, 2=Sangat Memuaskan)
- **Food_Rating** - Penilaian makanan oleh konsumen untuk restoran tersebut (0=Tidak Memuaskan, 1=Memuaskan, 2=Sangat Memuaskan)
- **Service_Rating** - Peringkat layanan konsumen untuk restoran (0=Tidak Memuaskan, 1=Memuaskan, 2=Sangat Memuaskan)

#### Restoran
- **Restaurant_ID** - Pengidentifikasi unik untuk setiap restoran
- **Nama** - Nama restoran
- **Kota** - Kota restoran
- **Negara Bagian** - Keadaan restoran
- **Negara** - Negara restoran
- **Kode_Zip** - Kode pos restoran
- **Lintang** - Garis lintang restoran
- **Bujur** - Garis bujur restoran
- **Layanan_Alkohol** - Apakah restoran tidak menyajikan alkohol, anggur & bir, atau bar lengkap
- **Boleh_merokok** - Dibolehkan merokok, termasuk di bar atau di bagian merokok
- **Harga** - Harga restoran (rendah, sedang, tinggi)
- **Waralaba** - Apakah restoran tersebut merupakan waralaba
- **Area** - Apakah restoran berada di area terbuka atau tertutup
- **Parkir** - Apakah restoran menawarkan tempat parkir apa pun (tidak ada, ya, umum, valet)

#### Restoran_Masakan
- **Restaurant_ID** - Pengidentifikasi unik untuk setiap restoran
- **Masakan** - Jenis makanan yang disajikan restoran		

## Diagram ER

## Pembersihan Data
### Langkah-langkah mengimpor data ke folder
1. Dapatkan data -> Lainnya -> Semua -> Folder -> Konversi -> Jalur menuju ke folder dataset -> Klik ok
2. Klik pada transformasi data -> Gandakan file -> Klik Biner untuk memperluas kumpulan data (Ulangi kumpulan untuk jumlah kumpulan data)
3. Bidang Terhitung

#### Kelompok Usia
```
Kelompok Umur = 
BERALIH(
    BENA(),
    konsumen[Usia] <= 18, "Anak-anak dan Remaja",
    konsumen[Usia] <= 30, "Dewasa Muda",
    konsumen[Usia] <= 45, "Dewasa",
    konsumen[Usia] <= 60, "Dewasa Paruh Baya",
    "Senior"
)
```
#### Kategori Peringkat Layanan
```
Kategori_Perangkat Layanan = SWITCH(
    BENA(),
    peringkat[Service_Rating] = 0, "Tidak Memuaskan",
    peringkat[Service_Rating] = 1, "Memuaskan",
    "Sangat Memuaskan"
)
```
#### Kategori Peringkat Keseluruhan
```
Keseluruhan_Rating_Category = SWITCH(
    BENA(),
    peringkat[Peringkat_K
eseluruhan] = 0,"Tidak Memuaskan",
    peringkat[Peringkat_Keseluruhan] = 1, "Memuaskan",
"Sangat Memuaskan"
)
```
#### Kategori Peringkat Makanan
```
Kategori_Peringkat Makanan = SWITCH(
    BENA(),
    peringkat[Food_Rating] = 0, "Tidak Memuaskan",
    peringkat[Food_Rating] = 1, "Memuaskan",
    "Sangat Memuaskan"
)
```

## Analisis Data
### Wawasan Lokal:
- Bagaimana distribusi konsumen menurut kota dan negara bagian?

    Sebagian besar penduduknya berasal dari San Luis Potosí, San Luis Potosí, sedangkan kelompok terbesar kedua berasal dari Cuernavaca, Morelos.

- Bagaimana distribusi usia konsumen berbeda-beda di setiap negara bagian?

    Di ketiga negara bagian tersebut, kaum muda di bawah usia 30 tahun merupakan mayoritas penduduk. Di dua negara bagian, San Luis Potosí dan Morelos, demografi terbesar kedua terdiri dari lansia, berusia di atas 60 tahun.

- Berapa persentase konsumen perokok atau bukan perokok di setiap kota?

    Mayoritas konsumen di keempat kota tersebut adalah bukan perokok, dan Jiutepec memiliki 100% populasi non-perokok. Di kota Cuernavaca, 25% populasinya adalah perokok.

- Mungkinkah umum ketersediaan parkir di restoran di berbagai kota?
    
    Mayoritas restoran di seluruh kota tidak memiliki fasilitas parkir, sementara beberapa restoran menyediakan tempat parkir. Di San Luis Potosí dan Cuernavaca, dua restoran menawarkan parkir valet, sementara parkir umum tersedia di San Luis Potosí, Ciudad Victoria, dan Cuernavaca.

### Wawasan Bersantap:
- Bagaimana korelasi ketersediaan parkir dengan tingkat harga restoran?
    
    Dari 16 restoran mahal, 16 memiliki tempat parkir, 3 menawarkan parkir valet, 1 menyediakan parkir umum, dan 5 tidak memiliki opsi parkir. Restoran dengan harga menengah dan rendah tidak menawarkan parkir valet; Namun, ada yang menyediakan tempat parkir umum atau menyediakan tempat parkir, sementara ada pula yang tidak menyediakan tempat parkir sama sekali.

- Bagaimana distribusi restoran menurut negara bagian?

    San Luis Potosí memiliki 84 restoran, sedangkan Morelos dan Tamaulipas masing-masing memiliki 23 restoran.
- Bagaimana restoran waralaba dibandingkan dengan non-waralaba dalam hal penilaian konsumen?

    Mayoritas restoran tersebut merupakan restoran non-waralaba, dan semuanya terbagi rata dalam tiga kategori penilaian: tidak memuaskan, memuaskan, dan sangat memuaskan. Sebagian kecil restoran merupakan waralaba, dan mereka juga didistribusikan secara merata di tiga kategori pemeringkatan yang sama.

- Masakan apa yang disukai konsumen berdasarkan profil demografi mereka?

    Masakan Meksiko adalah yang paling disukai, disusul masakan Amerika.


### Wawasan Perhotelan:
- Bagaimana jenis layanan alkohol yang ditawarkan berbeda-beda menurut restoran di setiap kota?

    Di gabungan empat kota—Jiutepec, San Luis Potosí, Cuernavaca, dan Ciudad Victoria—66,92% restoran tidak menawarkan alkohol, 6,93% menawarkan bar lengkap, dan 26,15% menawarkan anggur dan bir.

- Metode transportasi apa yang paling umum digunakan konsumen?

    61% konsumen menggunakan transportasi umum, 27% menggunakan ponsel, dan 11% berjalan kaki.

- Bagaimana kehadiran layanan alkohol mempengaruhi penilaian konsumen?

    Di antara bukan peminum, 303 menilai pengalaman mereka sangat memuaskan, 289 memuaskan, dan 170 tidak memuaskan. Untuk konsumen wine dan bir, penilaiannya adalah 146 sangat memuaskan, 105 memuaskan, dan 68 tidak memuaskan. Pada bar penuh, 37 dinilai sangat memuaskan, 27 memuaskan, dan 16 kurang memuaskan.

- Berapa persentase restoran yang mengizinkan merokok di setiap negara bagian?

    Sekitar 73% restoran menerapkan kebijakan bebas rokok, sementara hanya 1,5% di San Luis Potosí dan Morelo yang mengizinkan merokok di bagian bar. Sekitar 7% restoran mengizinkan merokok secara keseluruhan, dan sekitar 18,46% menawarkan area khusus merokok.

### Perilaku Wawasan:
- Apa pekerjaan umum konsumen di berbagai negara bagian?

    Di San Luis Potosí, 93% penduduknya terdiri dari pelaj
ah, danbersantai terdiri dari individu yang bekerja dan menganggur. Di Morelos, populasinya terbagi rata antara pekerja dan pelajar. Di Tamaulipas, 94% populasi
adalah pelajar, sedangkan 6% sisanya bekerja.

- Bagaimana perbedaan kadar minuman (berhemat, santai, sosial) di berbagai negara bagian?

    Di San Luis Potosí, hampir 40% penduduknya adalah peminum sosial, 36% adalah peminum biasa, dan 23% adalah peminum alkohol. Di Morelos, 45% adalah orang berpantang, 41% adalah peminum biasa, dan 12% adalah peminum sosial. Di Tamaulipas, 52% adalah orang berpantang, 31% adalah peminum biasa, dan 15% adalah peminum sosial.

- Bagaimana hubungan status perkawinan dengan kebiasaan merokok atau minum?

    Di antara 88 konsumen lajang, semuanya bukan perokok, dengan nilai yang menurun masing-masing sebagai peminum alkoholik, peminum biasa, dan peminum sosial. Di antara mereka yang menikah dan bukan perokok, 2 orang adalah orang yang berpantang dan 5 orang adalah peminum sosial. Selain itu, 23 konsumen lajang merokok dengan nilai-nilai yang digabungkan, dan mereka adalah peminum sosial dan peminum biasa. Terakhir, 2 orang perokok yang sudah menikah juga merupakan peminum sosial.

- Apakah ada hubungan antara pekerjaan konsumen dan tingkat anggaran mereka?

    Di antara siswa tersebut, 67 orang memiliki anggaran sedang, 33 orang memiliki anggaran rendah, dan 4 orang memiliki anggaran tinggi. Selain itu, 15 orang yang bekerja dan 1 orang yang menganggur memiliki anggaran menengah.

### Tinjauan Wawasan: 
- Apa saja 5 restoran teratas berdasarkan peringkat makanan?

    5 restoran teratas dengan kepuasan pelanggan - peringkat makanan yang tinggi adalah Tortas Locas Hipocampo dan Puesto de Tacos, di mana sebagian besar konsumen merasa sangat puas. Cafeteria y Restaurante El Pacífico memiliki 9 konsumen yang menilai sangat memuaskan, sedangkan Gorditas Doa Gloria mendapat 10. La Cantina Restaurante dinilai sangat memuaskan oleh 11 konsumen, dengan sisa suara dibagi antara memuaskan dan tidak memuaskan.

- Apa saja 5 restoran teratas berdasarkan peringkat layanan?

    5 restoran terbaik dengan kepuasan pelanggan tinggi untuk peringkat layanan adalah Tortas Locas Hipocampo, dimana sebagian besar konsumen merasa puas. Puesto de Tacos telah menerima 12 peringkat konsumen yang puas. Cafeteria y Restaurante El Pacífico juga mendapat penilaian memuaskan dari 12 konsumen, sedangkan Gorditas Doña Gloria mendapatkan angka yang sama. La Cantina Restaurante dinilai memuaskan oleh 7 konsumen, dengan sisa suara dibagi antara sangat memuaskan dan tidak memuaskan.

- Apa saja 5 restoran teratas berdasarkan peringkat keseluruhan?

    Lima restoran teratas dengan peringkat kepuasan pelanggan tinggi adalah Tortas Locas Hipocampo, yang sebagian besar konsumennya sangat puas, dan Puesto de Tacos, yang telah menerima 30 peringkat konsumen sangat puas. Cafeteria y Restaurante El Pacífico menyusul dengan 24 konsumen yang memberikan penilaian sangat memuaskan, sementara La Cantina Restaurante memberikan 28 penilaian sangat puas. Melengkapi daftarnya, Restaurant la Chalita telah mengumpulkan 20 peringkat kepuasan tinggi dari para pelanggannya.
  
## Dashboard:
<img width="1329" height="735" alt="Screenshot Dashboard PBI" src="https://github.com/user-attachments/assets/6f24273d-0e40-4d4c-bf00-60b608568e95" />

## Link Power BI
- Link Dashboard Power BI <a href="https://github.com/yesayass/Restaurant-Analysis-1/blob/main/Restaurant%20Ratings%20Analysis.pbix">View Dashboard
