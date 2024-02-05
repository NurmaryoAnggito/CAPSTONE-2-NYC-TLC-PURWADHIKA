
# CAPSTONE-2-NYC-TLC-PURWADHIKA-NURMARYO-ANGGITO


Capstone untuk modul 2 JCDS 2204 study case NYC TLC
Capstone 2 ini sebagai project modul dengan topik **Data Analytics** pada batch JCDS 2204 jakarta


## LATAR BELAKANG
Sebagai Data Analyst internal di perusahaan LPEP provider(taxi fleet owner). Analisis data NYC TLC bertujuan untuk memberikan kontribusi pada proses pengambilan keputusan untuk meningkatkan layanan kepada pelanggan dan juga meingkatkan pendapatan untuk perusahaan dan kesejahteraan pengemudi taksi. Proses analisis dilakukan dengan beberapa tahap yaitu, 
- melakukan data cleaning
- kemudian mencari problem yang dapat dihasilkan dari dataset 
- selanjutnya membuat visualisasi sesuai dataset 
- memberikan saran yang dapat dipresentasikan kepada penyedia layanan taksi.

## PROBLEMS
- Bagaimana meningkatkan efektifitas distribusi armada taksi berdasarkan waktu?. untuk meningkatkan pendapatan pengemudi dan perusahaan.
- Metode pembayaran apa yang paling banyak digunakan?
- Bagaimana gambaran distribusi transaksi perjalanan berdasarkan lokasi?
- Bagaimana meningkatkan pendapatan tip driver? 
# GOALS
Untuk meningkatkan pendapatan perusahaan dan kesejahteraan pengemudi dengan meningkatkan efektifitas dan efisiensi dalam penyebaran armada taksi

- Analisis Berbasis Waktu:
    - Meneliti pola perjalanan taksi berdasarkan waktu, mengidentifikasi jam sibuk dan hari dalam seminggu dengan permintaan tinggi. Menyarankan strategi untuk mengelola penempatan armada secara efektif selama periode tertentu.
- Analisis Tipe Pembayaran:
    - Menyelidiki jenis pembayaran yang berbeda secara keseluruhan. Mengidentifikasi aspek untuk perbaikan dalam proses pembayaran.
- Analisis Berbasis Lokasi:
    - Mengeksplorasi distribusi penjemputan dan penurunan taksi di berbagai lokasi (PULocationID dan DOLocationID), mengidentifikasi area lalu lintas tinggi dan mengoptimalkan alokasi sumber daya.
- Analisis Tip 
    - Analisis katergori trip seperti apa yang memiliki potensi tips yang tinggI.
## DATA UNDERSTANDING DAN PREPARATION
- Menggunakan dataset utama 'NYC TLC Trip Record' dan dataset tambahan untuk detail zona dan lokasi di kota New York 'taxi_zones'.
- convert datatype lpep_pickup_datetime dan lpep_dropoff_datetime dari object menjadi datetime
- Menghapus kolom ehail_fee, kolom ehail_fee di drop karena value null semua degan asumsi tidak ada yang memakai aplikasi ehail
- Menghapus null value data yang memiliki trip distance 0, akan dihapus karena dianggap transaksi gagal atau tidak jadi mengantar dan cek trip distance terjauh
    - karena jumlah proporsi null value pada data hanya dibawah 10 % atau sekitar 6.3% maka data tersebut akan saya drop
    - trip_type akan di drop karena proporsi sangat kecil
- mengecek duplikat (tidak ada duplikat)
- membuat kolom trip duration column dalam menit
- filter pickup time
    - filter datatime pickup time hanya bulan januari 2023 karena data mayoritas ada di bulan januari 2023, hanya ada 4 data yang diluar januari 2023
    - - karena ada 1 data outlier pada kolom trip_distance dengan nilai yang sangat jauh (diatas 1500) sedangkan data memiliki nilai 
rata2/mean = 2.58 dan nilai median = 1.8 maka data tersebut bisa di hilangkan
- hilangkan nilai negatif karena tipe pembayaran dispute atau ada masalah dalam proses pembayaran. Tentang cara pembayaran, harga, atau masalah lainnya
- saya menambahkan dataframe external untuk menjelaskan lokasi, kareana dalam dataframe awal data lokasi yaitu 'PULocationID' yang berbentuk angka yand tidak ada nama lokasi. 
    - melakukan merge dataframe utama yang sudah di clean/proses dengan dataframe zones untuk mendapatkan detail lokasi setiap perjalanan
    - merge antara zones.OBJECTID dengan Data_Clean.PULocationID (lokasi pickup) dan Data_Clean.DOLocationID (lokasi dropoff)
- setelah itu di cek untuk menemukan anomali pada data
    - terdapat 54 data dengan kolom 'OBJECTID, Shape_Leng, the_geom, Shape_Area, zone, LocationID, dan borough' memiliki nilai null karena kolom 'PULocationID' memiliki nilai yang tidak ada pada dataframe zone sehingga nilai kolom-kolom tersebut bernilai null.
    - saya berasumsi data tersebut melakukan pickup di luar kota New York.
    - sehingga saya akan melakukan drop pada data tersebut.
- data yang sudah bersih = 60505 data dari data awal = 68211 data jadi total pengurangan data adalah 11.3%


