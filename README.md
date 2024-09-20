# Klasterisasi Negara Penerima Bantuan oleh organisasi HELP Internasional menggunakan Algoritma K-Means

HELP International adalah LSM kemanusiaan internasional yang berkomitmen untuk memerangi kemiskinan dan menyediakan fasilitas serta bantuan dasar bagi masyarakat di negaranegara terbelakang saat terjadi bencana dan bencana alam. Saat ini, lembaga tersebut telah berhasil mengumpulkan sekitar $10 juta dan berencana untuk memberikan bantuan kepada negara yang membutuhkan. Proyek ini bertujuan untuk membantu CEO HELP Internasional untuk memutuskan 10 negara yang memiliki kondisi social ekonomi dan kesehatan ‘terburuk’ sehingga layak diberikan bantuan.

## DAFTAR ISI
1. [DATASET](#dataset)
2. [EXPLANATORY DATA ANALYSIS](#explanatory-data-analysisi)
3. [DATA PREPROCESSING](#data-preprocessing)
4. [MODELLING](#modelling)
5. [CONCLUSION](#conclusion)

## DATASET
[Dataset](https://github.com/latifatuzikra-suhairi/HELP-international/blob/main/Data_Negara_HELP.csv) terdiri dari 167 negara dengan 9 feature, yaitu:
1. `kematian anak`, angka kematian anak dibawah usia 5 tahun per 1000 kelahiran
2. `ekspor`, angka ekspor barang dan jasa perkapita
3. `impor`, angka impor barang dan jasa perkapita
4. `kesehatan`, total pengeluaran kesehatan perkapita
5. `pendapatan`, jumlah penghasilan bersih perorang
6. `inflasi`, tingkat pertumbuhan tahunan dari total GDP
7. `harapan hidup`, jumlah tahun rata rata seorang anak yang baru lahir akan hidup jika pola kematian tetap sama
8. `jumlah fertiliti`, jumlah anak yang akan lahir dari setiap wanita jika tingkat kseuburan usia saat ini sama.
9. `GDP perkapita`, total GDP dibagi dengan total populasi

## EXPLANATORY DATA ANALYSIS
1. Analisis Univariate
   Untuk melihat sebaran data dan nilai dominan tiap feature data berada di range berapa.

   [Analysis Univariate](https://raw.githubusercontent.com/latifatuzikra-suhairi/HELP-international/main/static/Univariate_Analysis.png)

   **Insight:** 
    a. Kematian_anak. Dari 167 negara, angka kematian anak dominan berada di range 0-25. 
    b. Ekspor. Dari 167 negara, nilai ekspor dominan berada di range 25-37,5. 
    c. Kesehatan. Dari 167 negara, pengeluaran untuk biaya kesehatan dominan berada di 4-6. 
    d. Impor. Dari 167 negara, nilai impor dominan berada di angka 25-37,5. 
    e. Pendapatan. Dari 167 negara, nilai penghasilan bersih perorang dominan berada di 012500. 
    f. Inflasi. Dari 167 negara, nilai inflasi dominan berada di angka 0-2.8 
    g. Harapan_hidup. Dari 167 negara, nilai harapan_hidup anak-anak disuatu negara dominan berada di angka 70,0-73,3 dan 76,6-82. 
    h. Jumlah_fertiliti. Dari 167 negara, nilai jumlah anak yang hidup di suatu negara dominan berada di angka 2-2,8. 
    i. GDPperkapita. Dari 167 negara, nilai GDPperkapita dominan berada di range 0-5000. 
   
2. Analisis Bivariate
   Untuk melihat hubungan antara dua feature: `GDPperkapita` dan `pendapatan`.
   
   [Analysis Bivariate](https://raw.githubusercontent.com/latifatuzikra-suhairi/HELP-international/main/static/Bivariate_Analysis.png)

   **Insight:**
    Semakin tinggi GDPperkapita akan berbanding lurus dengan kenaikan pendapatan. Hal ini dikarenakan GDPperkapita, dalam ilmu ekonomi, menjadi variabel penentu untuk tingkat laju konsumsi masyarakat yang sangat dipengaruhi oleh pendapatan/pemasukan seseorang. 
     
3. Analisis Multivariate
   Untuk melihat hubungan antara satu feature dengan beberapa feature lainnya. Disini dianalisis feature kesehatan dengan harapan hidup, jumlah fertiliti, kematian anak.

   [Analysis Multivariate](https://raw.githubusercontent.com/latifatuzikra-suhairi/HELP-international/main/static/Multivariate_Analysis.png)

   **Insight:**
   1. Kesehatan – harapan_hidup. Sekilas terlihat bahwa kesehatan tidak terlalu berdampak kepada harapan_hidup karena banyak factor external yang tidak terekam di dalam data yang dimiliki.
   2. Kesehatan – jumlah_fertiliti. Dominannya, ketika pengeluaran untuk kesehatan kecil, jumlah_fertiliti juga akan kecil. Namun, tentunya ada beberapa factor eksternal lainnya yang berpengaruh.
   3. Kesehatan – kematian_anak. Ketika pengeluaran untuk biaya kesehatan kecil-menengah, tingkat kematian anak cenderung kecil. Namun, tentu ada factor eksternal lain yang berpengaruh.
   4. Kematian_anak – jumlah_fertiliti. Berbanding lurus, ketika kematian_anak kecil maka jumlah fertiliti juga kecil.
   5. Kematian_anak – harapan_hidup. Ketika jumlah kematian_anak kecil, angka harapan_hidup akan tinggi
   6. arapan_hidup – jumlah_fertiliti. Jumlah anak yang akan lahir dari setiap wanita yang memiliki jumlah_fertiliti besar cenderung memiliki harapan_hidup yang menengah. Jika memiliki jumlah fetiliti sedikit, maka akan memiliki angka harapan_hidup yang tinggi.

  Dari analisis diatas, dapat dilihat hubungan antar feature:

  [Feature Relation](https://raw.githubusercontent.com/latifatuzikra-suhairi/HELP-international/main/static/Feature_Relation.png)

  **Penjelasan:**
  - Ketika suatu negara memiliki selisih nilai ekspor dan impor yang bernilai negative, artinya negara harus menyediakan uang banyak untuk membayar barang impor tersebut. Jika terlalu banyak impor, nilai inflasi akan tinggi. Akibat penggunaan uang untuk barang impor, biaya konsumsi pemerintah akan bertambah dan berdampak pada nilai GDP yang semakin kecil. GDP sendiri didapatkan dari biaya konsumsi sisa + investment + pengeluaran pemerintah + (biaya ekspor – biaya impor). Secara tidak langsung juga berdampak pada GDPpercapita = GDP/total populasi negara. Ketika nilai GDPperkapita rendah, tentu akan berdampak lurus pada pendapatan seseorang. Ketika seseorang memiliki pendapatan yang rendah, mereka akan enggan untuk mengeluarkan uang untuk biaya kesehatan. Ketika biaya kesehatan yang dikeluarkan kecil, maka akan berdampak pada harapan_hidup, kematian_anak, dan jumlah_fertiliti.
  - Negara dengan kondisi ekonomi buruk, cenderung memiliki nilai selisih ekspor-impor yang rendah (negative). Ketika nilai selisih ekspor-impor negative tentu akan berpengaruh pada nilai inflasi yang menaik. Inflasi yang menaik akan mempengaruhi GDPperkapita dan sejalan juga mempengaruhi pendapatan perkapita menjadi rendah di negara tersebut. Ketika pendapatan seseorang rendah, maka pengeluaran untuk biaya kesehatan pun juga rendah.
  - Dari penjabaran tersebut, penulis mengambil empat feature utama yang sangat berpengaruh untuk mengetahui kondisi ekonomi dan kesehatan sebuah negara. Keempat feature ini nantinya berguna sebagai bahan pertimbangan melihat apakah negara tersebut berhak mendapat bantuan dari HELP International. Empat feature tersebut yaitu `selisih ekspor-impor, inflasi, pendapatan, dan kesehatan.`

## DATA PREPROCESSING
1. Outlier Handling
   Untuk mengatasi data pencilan/nilai outliers yang nilainya sangat jauh dari central tendency. Hal ini dilakukan agar saat melakukan clustering tidak ada data yang letak clusternya terlalu menyebar/jauh dari titik point pusat penyebarannya. Diterapkan pada 4 feature yang digunakan:
   1. Outlier handling pada feature `inflasi`

      [Outlier Inflasi](https://raw.githubusercontent.com/latifatuzikra-suhairi/HELP-international/main/static/OutlierHandling_Inflasi.png)

      nilai outliers ini akan dihapus dengan menggunakan konsep nilai lower bound dan upper bound.
      
   2. Outlier handling pada feature `kesehatan`

      [Outlier Kesehatan](https://raw.githubusercontent.com/latifatuzikra-suhairi/HELP-international/main/static/OutlierHandling_Kesehatan.png)

      nilai outliers ini akan dihapus dengan menggunakan konsep nilai lower bound dan upper bound.
      
   3. Outlier handling pada feature `pendapatan`

      [Outlier Pendapatan](https://raw.githubusercontent.com/latifatuzikra-suhairi/HELP-international/main/static/OutlierHandling_Pendapatan.png)

      nilai outliers ini akan dihapus dengan menggunakan konsep nilai lower bound dan upper bound.
      
   4. Outlier handling pada feature `selisih ekspor impor`

      [Outlier Selisih Ekspor Impor](https://raw.githubusercontent.com/latifatuzikra-suhairi/HELP-international/main/static/OutlierHandling_Ekspor_Impor.png)

      Pada kolom selisih ekspor impor terlihat banyak nilai outliers, terutama yang bernilai negative (artinya impor lebih besar dari ekspor).  Ketika sebuah negara memiliki nilai selisih ekspor-impor negative yang besar, dapat dikatakan bahwa negara tersebut berada dalam keadaan ekonomi yang  ‘buruk’.  Jika data dengan nilai outliers dihapus, tentu akan mempengaruhi pengambilan kesimpulan negara dengan kondisi ‘buruk’. Untuk itu, penulis tidak menghapus data outliers pada feature Selisih_EI.

2. Data Scaling
   Untuk membuat data numerik pada dataset memiliki rentang nilai yang sama, sehingga tidak ada lagi satu feature yang mendominasi feature lainnya. Menggunakan metode standardisasi dengan StandardScaler.
   ```python
      from sklearn.preprocessing import StandardScaler

      sc = StandardScaler()
      df_std2 = sc.fit_transform(df.astype(float))
   ```

## MODELLING
1. Clustering feature `Selisih Ekpor Impor` dan `Inflasi`
   Feature tersebut dimodelkan dengan algoritma `K-Means` dengan penentuan K optimal berdasarkan `elbow method`. Elbow method yang didapatkan:

   [Elbow 1](https://raw.githubusercontent.com/latifatuzikra-suhairi/HELP-international/main/static/Elbow_SelisihEI_Inflasi.png)

   Lingkaran merah menunjukkan jumlah optimal cluster untuk feature `Selisih Ekpor Impor` dan `Inflasi`, yakni di angka **4 klaster**

   **Hasil Clustering:**

   [Clustering 1](https://raw.githubusercontent.com/latifatuzikra-suhairi/HELP-international/main/static/Clustering_SelisihEI_Inflasi.png)

   **Penjelasan:**
   Dari visualisasi tersebut, terdapat empat cluster yaitu cluster 0, 1, 2, 3. Namun, cluster 2 tidak terlalu banyak anggota clusternya dikarenakan karena nilai outliers dari selisih_Ekspor Impor tidak dihapus (ada data yang menyimpang sangat jauh). Dengan mempertimbangkan nilai pendapatan tiap negara dan mengacu ke aturan inflasi yang dikeluarkan oleh Federal Reserve USA, batas minimum untuk inflasi adalah sebesar 2%. Sesungguhnya, jika nilai inflasi terlalu rendah, sesuai hukum permintaan dan penawaran tarif barang dan jasa menjadi sangat murah, sehingga tidak kompetitif. Cluster 3 menunjukkan inflasi yang tinggi, tetapi dibarengi dengan nilai ekspor yang lebih tinggi dibandingkan dengan cluster 0. Hal ini terlihat bahwa nilai ekspor cluster 0 jauh jika dibandingkan cluster 3. Fenomena ini membuktikan pernyataan diatas, bahwa inflasi yang terlalu rendah tidak akan baik untuk negaranya. Untuk itu, penulis mengambil cluster 0 sebagai bahan pertimbangan negara bantuan HELP International.  
   
3. Clustering feature `Pendapatan` dan `Kesehatan`
   Feature tersebut dimodelkan dengan algoritma `K-Means` dengan penentuan K optimal berdasarkan `elbow method`. Elbow method yang didapatkan:
   
   [Elbow 2](https://raw.githubusercontent.com/latifatuzikra-suhairi/HELP-international/main/static/Elbow_Pendapatan_Kesehatan.png)

   Lingkaran merah menunjukkan jumlah optimal cluster untuk feature `Pendapatan` dan `Kesehatan`, yakni di angka **6 klaster**

   **Hasil Clustering:**

   [Clustering 2](https://raw.githubusercontent.com/latifatuzikra-suhairi/HELP-international/main/static/Clustering_Pendapatan_Kesehatan.png)

   **Penjelasan:**
   Dari visualisasi tersebut, terdapat enam cluster yaitu cluster 0, 1, 2, 3, 4, 5. Logikanya, semakin kecil pendapatan seseorang, mereka akan cenderung untuk menghemat pengeluaran untuk berbelanja, salah satunya pengeluaran untuk kesehatan. Hal ini menunjukkan kejadian yang terjadi di negara ‘buruk’ social ekonomi dan kesehatannya.  Dengan alasan ini, clustering yang diambil adalah cluster 0.

## CONCLUSION
1. Ketika nilai inflasi terlalu rendah, sesuai hukum permintaan dan penawaran tarif barang dan jasa menjadi sangat murah, sehingga tidak kompetitif. Akibatnya, pendapatan pun ikut menurun mengikuti laju harga barang di masyarakat. Pendapatan yang rendah berkontribusi pada tingkat konsumsi yang rendah pula, sehingga orang akan cenderung hemat dalam berbelanja, termasuk dalam bidang kesehatan.
2. Setelah menetapkan cluster mana yang akan diambil dari kedua kelompok feature clustering tersebut, dengan berbagai pertimbangan yang telah dijelaskan sebelumnya, penulis 
menghubungkan kondisi kedua cluster tersebut. Setelah penggabungan kedua cluster, data diurutkan berdasarkan pendapatan secara ascending dan diambil 10 negara pertama. Listing tabel dibawah menjadi kelompok negara yang dianggap pantas untuk menerima bantuan pendanaan 10 Juta Dollar oleh organisasi HELP International.

[10 Negara Bantuan](https://github.com/latifatuzikra-suhairi/HELP-international/blob/main/static/10Negara.png)

Data ini juga merefleksikan dunia nyata dimana negara-negara Afrika diatas, kecuali Haiti, tergolong kelompok ekonomi negara terbelakang (Least Developed Countries, LDCs). 
