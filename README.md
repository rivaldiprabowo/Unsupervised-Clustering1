# Unsupervised Learning Clustering
## Melbourne Property Clustering
### By: Muhamamd Rivaldi Prabowo

![Melbourne](https://user-images.githubusercontent.com/99151517/162689756-e6ce8b9c-4648-44aa-8e3e-487062744573.jpg)

## Latar Belakang dan Pernyataan Masalah
<p align='justify' style="font-weight: bold;">
Pandemi Covid-19 yang terjadi di seluruh dunia telah berdampak pada semua sektor kehidupan dan industri, salah satunya adalah di sektor industri property. Berdasarkan website <a href="https://www.abc.net.au/news/2022-03-24/six-ways-pandemic-reshaped-australias-housing-market-corelogic/100933182#:~:text=According%20to%20CoreLogic's%20Home%20Value,by%20%24173%2C805%2C%20to%20be%20%24728%2C034.)">(sumber informasi)</a> pada saat awal pandemi dari awal April hingga September 2020 harga property di Australia rata-rata turun hingga 2,1% akan tetapi pada awal Oktober 2020 hingga Februari 2022 harga rumah melonjak naik hingga 24.6% dan juga terdapat lonjakan dari jumlah pembeli property selama rentang tersebut. Hal ini juga tidak terlepas dari kebijakan Bank Sentral Australia yang memberlakukan relaksasi bunga bank selama rentang waktu 2020 hingga 2024 serta berbagai stimulus lainnya. 

Berdasarkan peningkatan gairah pasar property di Australia seperti yang telah dijelaskan sebelumnya, sebuah perusahaan agen property yang telah beroperasi di berbagai *Capital City* di Australia, seperti Sydney, Brisbane, Adelaide, dan Perth akan membuka kantor barunya di Melbourne sebagai salah satu *Capital City* di Australia. Pihak management perusahaan tersebut menilai bahwa pasar property Kota Melbourne memiliki potensi yang sangat bagus di masa depan. Hal ini berdasarkan kepada keadaan Kota Melbourne yang telah bebas dari *lockdown*, peningkatan konsumsi masyarakat, peningkatan sektor ekonomi, dan banyaknya lapangan pekerjaan yang dibuka [(sumber informasi)](https://propertyupdate.com.au/property-investment-melbourne/#is-it-the-right-time-to-get-into-the-melbourne-property-market).

Akan tetapi perusahaan tersebut masih belum mengetahui peta keadaan property pada Kota Melbourne, apalagi dengan keadaan peningkatan harga property yang sangat bervariasi di setiap daerah di Melbourne, karena terdapat *local supply and demand* [(sumber informasi)](https://propertyupdate.com.au/property-investment-melbourne/#is-it-the-right-time-to-get-into-the-melbourne-property-market). Perusahaan tersebut juga berencana akan membuat paket-paket jenis property yang akan digunakan dalam strategi pemasaran kepada para calon pembeli property. Oleh karena itu, mereka menyewa konsultan data scientist agar dapat menganalisa keadaan pasar property di Kota Melbourne secara lebih tepat dan holistik, selain itu data scientist juga dapat membuat jenis-jenis paket property berdasarkan pengelompokan klsuter. Pengelompokan kluster dari property ini bertujuan untuk membantu pihak perusahaan dalam memasarkan dan menjual property. Pihak perusahaan juga dapat dengan mudah mengetahui segmentasi pasar property berdasarkan hasil dari pengelompokan kluster. Keuntungan lain dari pengelompokan kluster ini adalah pihak perusahaan akan dengan mudah menjelaskan kepada para calon pembeli spesifikasi dari setiap kluster, sehingga para pembeli tidak kebingungan dalam mencari property yang sesuai dengan keinginan dan kemampuan finansialnya. Selain itu persebaran kluster property dalam kota ini akan dengan mudah menjadi bahan analisis lanjutan bagi perusahaan ini.

Dataset yang digunakan dalam project ini berasal dari website Kaggle [(Kaggle)](https://www.kaggle.com/dansbecker/melbourne-housing-snapshot).
  </p>
  
## Pemahaman Kondisi Property dan Analisis Bisnis Proses pada Kota Melbourne
<p align='justify' style="font-weight: bold;">
Asumsi dan interpretasi dari keadaan pasar property Kota Melbourne:            

* Pada Kota Melbourne, sepertinya property **dapat dijual secara langsung ataupun dapat dijual melalui pelelangan kota.**
* Kita dapat mengetahui property yang dijual berdasarkan informasi dari kolom method dan secara umum property dibagi menjadi **property yang telah terjual (S-Sold)** dan **masih belum terjual (SP,PI,SA,VB).**
* Date menunjukkan tanggal penjualan dari property dan dapat diinterpretasikan sebagai berikut:
    * Date pada Method S (Sold) menunjukan tanggal penjualan property dan property tersebut tidak dijual kembali atau dengan kata lain pembeli property membeli property dan tidak menjualnya kembali.
    * Date pada Method SP,PI,SA,VB menunjukan tanggal penjualan property sebelum property tersebut dijual kembali atau dengan kata lain pembeli property membeli property kemudian menjualnya kembali melalui berbagai Method.
  
Dalam memahami kondisi property pada dataset ini dan juga dalam memudahkan dalam proses *data cleansing*, saya akan membaginya ke dalam beberapa kelompok berdasarkan keadaan pasar property Kota Melbourne, kesamaan tipe data dan hubungan antar kolom, berikut adalah kelompok-kelompoknya:
1. Status Penjualan: Method.
2. Tanggal dan harga jual: Price, Date.
3. Lokasi: Suburb, Address, Regionname, Lattitude, Longtitude, Postcode, Distance.
4. Spesifikasi rumah: Rooms, Type, Bedroom2, Bathroom, Car, Landsize, Building Area, Year Built.
5. Other data: SellerG, Property count, Council Area.

Secara umum bisnis proses pada pasar property adalah:
1. Perusahaan agen property menerima penawaran dari penduduk setempat yang ingin menjual propertynya dengan cepat, karena Perusahaan agen property dapat memasarkan property ke masyarakat luas maupun ke suatu instansi.
2. Perusahaan property lalu mendapatkan semua data property yang dijual menggunakan jasanya.
3. Perusahaan property lalu memasarkan property yang dijual tersebut dan terjadilah kontak dengan para calon pembeli.
4. Perusahaan property berusaha agar harga property yang dijual cukup kompetitif tetapi mereka juga harus mendapatkan profit maksimal.
5. Penjualan property di Kota Melbourne dapat melalui iklan langsung, melalui agen property, atau melalui proses pelelangan (auction).

Berdasarkan penjelasan bisnis proses diatas, kita bisa menyimpulkan bahwa perusahaan agen property hanya tertarik terhadap property yang masih bisa dibeli atau `Available` dan tidak mungkin tertarik kepada property yang sudah terjual `Sold`, sehingga **dalam proses analisis dan pengelompokan kluster, saya hanya akan menggunakan data property yang `Available`.**
</p>

## Hasil Modelling dan Analisis Property pada Kota Melbourne
<p align='justify' style="font-weight: bold;">
  
1. **Data yang digunakan** pada proses analisis dan pemodelan hanya menggunakan data property yang sekiranya **dapat dijual dan dapat di akuisisi oleh pihak Perusahaan Property (Method: SP,PI,SA,VB)**. Karena berdasarkan bisnis proses, perusahaan agen property hanya tertarik pada property yang akan dijual oleh masyarakat, sehingga hanya **Property dengan kategori `Available`** saja yang digunakan untuk proses analisis dan modelling.
  
2. Dalam pemodelan Unsupervised Clustering, saya menggunakan **11 kolom dan 3929 baris data** yang relevan terhadap pemodelan.
  ![Dataframe Model](https://user-images.githubusercontent.com/99151517/162691793-a06eb8c9-ebc8-4f7f-ae14-45d2ce32cd93.JPG)
  
3. Terdapat dua jenis Pre-Processing untuk mencari nilai PCA terbaik:
    * **Pre-processing (Semua dengan Proses Scaling)**, pada jenis Pre-Processing ini semua data numerik melewati proses scaling. Algoritma PCA digunakan untuk melihat berapa banyak informasi yang tersimpan pada proses ini dan proses ini menyimpan informasi pada 2 komponen pertama sebesar **63.43 %**.
    * **Pre-processing (Beberapa dengan Proses Scaling)**, pada jenis Pre-Processing ini hanya kolom Price saja yang melewati proses scaling. Algoritma PCA digunakan untuk melihat berapa banyak informasi yang tersimpan pada proses ini dan proses ini menyimpan informasi pada 2 komponen pertama sebesar **99.68 %**.
   Proses PCA menggunakan Pre-Processing kedua dipilih karena menyimpan informasi yang paling banyak (99.68%)
  
4. Algoritma yang digunakan pada proses Unsupervised Learning adalah **K-Means Clustering**.
  
5. Berdasarkan algoritma K-Means Clusering, **jumlah cluster optimum adalah 5 Cluster** dengan **silhouette score 0.63**.
  ![Clustering](https://user-images.githubusercontent.com/99151517/162692036-da86df87-ed60-4410-9481-cb34fd73cbb6.JPG)
  ![Silhouette score](https://user-images.githubusercontent.com/99151517/162692045-0a663a53-6808-4558-9ae0-bd0a01f19e00.JPG)
  
6. Feature Engineering digunakan untuk memudahkan dalam proses analisa hasil model. Feature Engineering yang digunakan berupa kategorisasi data numerik. Hasil dari feature engineering ini adalah kolom `RangePrice`, `CategorizedRooms`, `CategorizedLandsize`, `CategorizedBuildingArea`, dan `CityDistance`.
  
7. Penjualan property terbanyak ada pada rentang bulan **Maret-September** atau pada musim **Fall-Winter**.
  ![Month](https://user-images.githubusercontent.com/99151517/162692365-7ec79499-b70e-4cf2-a046-f96ab9a9c9ed.JPG)
  ![Season](https://user-images.githubusercontent.com/99151517/162692363-44f3b337-b884-4b6d-b51d-5f8b1b98d5eb.JPG)
  
8. Property yang dapat diperjual belikan paling banyak terdapat pada region Southern Metropolitan, kedua berada pada Northern Metropolitan, ketiga pada Western Metropolitan, dan keempat pada Eastern Metropolitan.
  ![Region](https://user-images.githubusercontent.com/99151517/162692568-baf1c12a-f016-4b28-9241-e4d46c07cb32.JPG)
  
9. Dalam proses mengenali karakteristik dari setiap cluster, pertama dilakukan analisis secara umum dan sederhana berdasarkan statistik deskriptif pada setiap cluster.
  
  ![Deskriptif](https://user-images.githubusercontent.com/99151517/162693202-29e8c957-a292-479c-948a-347441870050.JPG)
  
10. Analisis Multivariate dilakukan untuk lebih mengetahui bagaimana karakteristik dari setiap cluster.
  ![BuildingArea](https://user-images.githubusercontent.com/99151517/162693362-4f7383be-d56e-4d40-ac0d-f5ebc164df2f.JPG)
  ![Distance](https://user-images.githubusercontent.com/99151517/162693369-0a2bca44-1cf5-42d1-a758-685f15fe7a48.JPG)
  ![Landsize](https://user-images.githubusercontent.com/99151517/162693372-677c1dab-66da-45b6-a351-5398b754d0f0.JPG)
  
11. Berikut adalah hasil analisis singkat mengenai karakteristik dari masing-masing cluster:
    1. **Cluster 1**: Dominasi oleh property perumahan dengan harga yang lumayan tinggi, jumlah ruangan yang cukup banyak dengan luas bangunan yang cukup besar dan luas tanah yang luas. Cluster ini cocok untuk para warga kota dengan kemampuan ekonomi menengah keatas.
  ![Cluster 1 All](https://user-images.githubusercontent.com/99151517/162693483-174a078c-ee5b-4933-9e6d-5338cee68d29.JPG)
  
    2. **Cluster 2**: Dominasi oleh duplex atau apartment dengan harga murah, jumlah ruangan yang sedikit dengan luas tanah dan bangunan yang kecil namun sangat dekat dengan CBD. Cluster ini cocok untuk para warga kota dengan kemampuan ekonomi menengah kebawah atau para pekerja kantoran.
  ![Cluster 2 All](https://user-images.githubusercontent.com/99151517/162693498-502d64d4-0764-46bf-a3b1-c9ea133ab4de.JPG)
  
    3. **Cluster 3**: Dominasi oleh pemukiman warga dengan harga yang sangat mahal (mansion atau villa mewah). Mayoritas cluster ini memiliki jumlah ruangan yang banyak dengan luas tanah yang besar dan luas bangunan sangat besar. Cluster ini cocok untuk para warga kota dengan kemampuan ekonomi kelas atas hingga kaya raya.
  ![Cluster 3 All](https://user-images.githubusercontent.com/99151517/162693517-57487a82-b0d7-48b9-b4e6-27339f642278.JPG)
  
    4. **Cluster 4**: Dominasi oleh property berupa perumahan dengan harga yang sedang, jumlah ruangan yang sedang dengan luas tanah dan bangunan yang tidak terlalu besar hingga sedang. Cluster ini cocok untuk para warga kota dengan kemampuan ekonomi menengah, hingga menengah kebawah.
  ![Cluster 4 All](https://user-images.githubusercontent.com/99151517/162693528-29f3644e-7e3e-4511-9644-00a72bb77a77.JPG)
  
    5. **Cluster 5**: Dominasi oleh pemukiman warga dengan harga yang sangat mahal (villa atau cottage mewah). Mayoritas cluster ini memiliki jumlah ruangan yang banyak dengan luas tanah dan luas bangunan yang sangat besar. Mayoritas jarak pada cluster ini cukup jauh dengan pusat kota. Cluster ini cocok untuk para warga kota dengan kemampuan ekonomi kelas atas hingga kaya raya.
  ![Cluster 5 All](https://user-images.githubusercontent.com/99151517/162693547-5642e3de-609e-4ac9-bcbb-5681fe57260a.JPG)
  
12. Tableau Public digunakan untuk menganalisis dan memvisualisasikan persebaran setiap Cluster dan property berdasarkan persebaran geografis. Dashboard Tableau tersebut dapat dilihat pada link berikut [**(Tableau Visualization)**](https://public.tableau.com/app/profile/muh.rivaldi.prabowo/viz/MelbourneAvailablePropertyGeospatialInformationDashboard/GeographicalInfromation?publish=yes)
  
13. Analisa dan modelling menggunakan Unsupervised Learning: Clustering sangat membantu perusahaan agen property dalam mengenali keadaan sebenarnya dari pasar property Kota Melbourne, mulai dari property mana saja yang dapat dijual pada Kota Melbourne, kapan transaksi jual beli property banyak terjadi, mengenali karakteristik dari setiap kluster property, segmentasi calon pembeli property berdasarkan kluster property, hingga mengetahui persebaran setiap property pada Kota Melbourne.
  </p>
  
## Rekomendasi untuk Perusahaan Property
<p align='justify' style="font-weight: bold;">
  
1. Lakukan proses marketing dan pemasaran yang gencar terutama pada rentang bulan Maret-September dimana pada bulan-bulan tersebut banyak terjadi transaksi jual-beli property.
  
2. Batasi daerah pemasaran dan operasi berdasarkan jumlah property yang dijual pada region tertentu. Saya menyarankan gencarkan bagian pemasaran pada region Southern Metropolitan, Northern Metropolitan, Western Metropolitan, dan terakhir pada Eastern Metropolitan.
  
3. Sesuaikan rekomendasi property kepada customer berdasarkan profil dari customer lalu sesuaikan dengan Cluster property yang ada, contoh:
    * **Customer dengan kemampuan ekonomi menengah keatas dan ingin memiliki property dapat diarahkan untuk melihat property Cluster 1.**
    * **Customer dengan kemampuan ekonomi menengah kebawah atau para pekerja kantoran yang ingin memiliki property dekat dengan kantornya dapat diarahkan untuk melihat property Cluster 2.**
    * **Customer dengan kemampuan ekonomi kelas atas hingga kaya raya dan ingin memiliki perumahan mewah bertingkat dan dekat dengan kota dapat diarahkan untuk melihat property Cluster 3.**
    * **Customer dengan kemampuan ekonomi menengah dan ingin memiliki perumahan sederhana dapat diarahkan untuk melihat property Cluster 4.**
    * **Customer dengan kemampuan ekonomi kelas atas hingga kaya raya dan ingin memiliki property mewah namun jauh dari hiruk-pikuk perkotaan dapat diarahkan untuk melihat property Cluster 5.**
  
4. Dahsboard pada Tableau Public dapat digunakan untuk menyeleksi spesifikasi pada setiap property.
  
5. Perusahaan Property juga harus jeli dalam mengakuisisi property yang akan dijual, contohnya:
    * Property dengan yang baru saja ditawar oleh perusahaan property lain (Method Vendor Bid) pada pelelangan dapat diambil oleh kita dengan cara menawar property pada harga lebih tinggi jika memang propertynya bagus untuk dijual kembali.
    * Selalu update mengenai property mana yang masuk ke dalam pelelangan (Method Property In), jika property menarik maka boleh ditawar dengan harga tinggi.
    * Perbanyak pemasaran dan iklan mengenai keuntungan menjual property pada perusahaan ini dibandingkan di perusahaan lain, sehingga masyarakat yang akan menjual property akan tertarik memakai jasa perusahaan ini.
    </p>
