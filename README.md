# Unsupervised Learning Clustering
## Melbourne Property Clustering
### By: Muhamamd Rivaldi Prabowo

![Melbourne](https://user-images.githubusercontent.com/99151517/162689756-e6ce8b9c-4648-44aa-8e3e-487062744573.jpg)

## Latar Belakang dan Pernyataan Masalah
<p align='justify' style="font-weight: bold;">
Pandemi Covid-19 yang terjadi di seluruh dunia telah berdampak pada semua sektor kehidupan dan industri, salah satunya adalah di sektor industri property. Berdasarkan website <a href="https://www.abc.net.au/news/2022-03-24/six-ways-pandemic-reshaped-australias-housing-market-corelogic/100933182#:~:text=According%20to%20CoreLogic's%20Home%20Value,by%20%24173%2C805%2C%20to%20be%20%24728%2C034.)">sumber informasi</a> pada saat awal pandemi dari awal April hingga September 2020 harga property di Australia rata-rata turun hingga 2,1% akan tetapi pada awal Oktober 2020 hingga Februari 2022 harga rumah melonjak naik hingga 24.6% dan juga terdapat lonjakan dari jumlah pembeli property selama rentang tersebut. Hal ini juga tidak terlepas dari kebijakan Bank Sentral Australia yang memberlakukan relaksasi bunga bank selama rentang waktu 2020 hingga 2024 serta berbagai stimulus lainnya. 

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
