# Laporan Proyek Machine Learning - News Articles Recommendation
**Disusun oleh : Muhamad Alan Dharma Saputro Setiawan**
Laporan ini disusun untuk memenuhi submission dicoding proyek kedua *recommendation system*. Proyek ini dibangun menggunakan model machine learning menggunakan content-based filtering untuk memberikan rekomendasi artikel berita dengan input *free text*.

## Project Overview
Proyek ini mendapatkan inspirasi dari upaya penelitian kontemporer dalam sistem rekomendasi berita yang dipersonalisasi, sebagaimana dibuktikan dengan referensi ilmiah yang dikutip. Dalam lanskap berita digital saat ini, banyaknya konten membutuhkan metode yang efektif untuk menyaring dan merekomendasikan artikel yang relevan kepada pengguna. Dengan memanfaatkan wawasan dan metodologi dari penelitian yang sudah ada, proyek ini bertujuan untuk mengembangkan sistem rekomendasi yang secara dinamis menyesuaikan saran berita berdasarkan masukan dan preferensi pengguna. Menggabungkan teknik-teknik seperti TF-IDF dan WordNet akan meningkatkan akurasi dan relevansi artikel yang direkomendasikan, sehingga memungkinkan pembuatan profil pengguna dan berita yang dapat menangkap preferensi individu. Sejalan dengan paradigma penelitian yang sudah ada, proyek ini berusaha untuk berkontribusi pada diskusi yang sedang berlangsung tentang sistem rekomendasi berita yang dipersonalisasi, yang pada akhirnya memberdayakan pengguna untuk menavigasi lanskap berita digital yang terus berkembang dengan efisiensi dan kepuasan yang lebih besar.

Sistem rekomendasi berbasis konten yang dihadirkan dalam proyek ini menjawab tantangan dan tren penting dalam industri berita digital. Pertama, di tengah-tengah informasi yang melimpah, sistem rekomendasi yang dipersonalisasi sangat penting untuk memandu pengguna melalui beragam konten yang tersedia. Dengan menganalisis preferensi pengguna dan karakteristik konten, sistem semacam itu dapat menyesuaikan rekomendasi berita, meningkatkan pengalaman konsumsi berita secara keseluruhan dan mendorong keterlibatan pengguna. Kedua, sistem ini membantu mempromosikan penemuan konten berkualitas di tengah penyebaran informasi yang salah. Dengan memanfaatkan teknik-teknik canggih seperti pemrosesan bahasa alami dan pembelajaran mesin, sistem ini mengidentifikasi sumber dan artikel yang memiliki reputasi baik, menumbuhkan kepercayaan pada platform berita dan berkontribusi pada ekosistem berita yang lebih sehat. Dengan terus menganalisis perilaku pengguna dan tren konten, sistem ini beradaptasi dan meningkatkan rekomendasinya untuk memenuhi kebutuhan pengguna yang terus berkembang, yang berfungsi sebagai alat yang berharga untuk meningkatkan konsumsi berita, mendorong keterlibatan, dan mempromosikan penemuan konten berkualitas di era digital.

Referensi: [M.-D. Hong, K.-J. Oh, M.-H. Ga, and G.-S. Jo, “Content-based Recommendation Based on Social Network for Personalized News Services,” Journal of Intelligence and Information Systems, vol. 19, no. 3, pp. 57–71, Sep. 2013](https://koreascience.kr/article/JAKO201330251812546.page)

## Business Understanding
### Problem Statement
- Bagaimana dapat secara efektif menyaring dan merekomendasikan artikel berita yang relevan kepada pengguna di tengah-tengah banyaknya konten yang tersedia dalam lanskap berita digital saat ini?
- Apakah kurangnya rekomendasi berita yang dipersonalisasi menyebabkan ketidakpuasan pengguna dan berkurangnya keterlibatan dengan platform berita?
### Goals
- Mengembangkan sistem rekomendasi berita berbasis konten yang menganalisis masukan dan preferensi pengguna untuk menyesuaikan saran berita secara dinamis. Meningkatkan akurasi dan relevansi rekomendasi berita dengan menggabungkan teknik-teknik canggih seperti TF-IDF dan WordNet untuk analisis teks.
- Meningkatkan kepuasan dan keterlibatan pengguna dengan memberikan rekomendasi berita yang disesuaikan dengan preferensi individu. Awalnya fokus pada penyaringan berbasis konten menggunakan data yang tersedia, memungkinkan pengguna untuk memberikan input teks bebas untuk pencarian dalam sistem rekomendasi.

### Solution Statement
- Menerapkan algoritme penyaringan berbasis konten yang menganalisis konten tekstual artikel berita untuk mengidentifikasi kesamaan dan pola. Pendekatan ini memungkinkan sistem untuk merekomendasikan artikel yang memiliki kesamaan tema atau topik dengan teks yang dimasukkan pengguna, sehingga meningkatkan relevansi rekomendasi.
- Memanfaatkan TF-IDF (Term Frequency-Inverse Document Frequency) dan WordNet untuk mengekstrak fitur-fitur utama dan informasi semantik dari artikel berita. Dengan menggabungkan teknik-teknik ini, sistem dapat lebih memahami konteks dan makna yang mendasari konten berita, sehingga menghasilkan rekomendasi yang lebih akurat.
 
## Data Understanding
Dataset yang digunakan dalam proyek ini adalah dataset "News Articles" yang diperoleh dari Kaggle. Anda dapat mengunduh dataset tersebut dari tautan berikut: [News Articles Dataset](https://www.kaggle.com/datasets/bavalpreet26/newsarticle/data).
### Variable in News Articles Dataset:
1. **Article_Id**: Pengenal unik untuk setiap artikel dalam dataset.
2. **Title**: Judul atau tajuk utama artikel berita, yang memberikan ringkasan atau deskripsi singkat tentang isinya.
3. **Author**: Nama penulis atau kontributor yang menulis artikel.
4. **Date**: Tanggal dan waktu ketika artikel diterbitkan atau terakhir diperbarui.
5. **Content**: Bagian utama artikel, yang berisi informasi, berita, atau analisis terperinci.
6. **URL**: URL web atau tautan untuk mengakses artikel lengkap secara online, biasanya dihosting di situs web publikasi.

**Top 15 Author with Most Uploaded Content**
| Author                    | Number of Articles |
|---------------------------|---------------|
| rohit kvn                 | 462           |
| besta shankar             | 340           |
| prakash upadhyaya         | 302           |
| mugdha variyar            | 261           |
| anu james                 | 254           |
| neha singh                | 239           |
| shekhar h hooli           | 228           |
| prarthna sarkar           | 189           |
| s v krishnamachari        | 164           |
| ashim sunam               | 150           |
| sushmita sen              | 139           |
| suparno sarkar            | 138           |
| sachin jose               | 134           |
| indo-asian news service   | 118           |
| johnlee varghese          | 113           |

**Rohit KVN**
![rohit](https://i.ibb.co/0h6PCcw/rohit.png)
*Word cloud* yang dihasilkan dari konten Rohit KVN menunjukkan penekanan yang kuat pada topik yang berhubungan dengan teknologi. Istilah-istilah seperti "android", "marshmallow", "google", dan "apps" menunjukkan fokus pada teknologi seluler, perangkat lunak, dan platform digital. Hal ini mengindikasikan bahwa artikel-artikel Rohit KVN kemungkinan besar mencakup perkembangan, pembaruan, dan tren di industri teknologi, terutama yang terkait dengan perangkat dan aplikasi seluler.

**Besta Shankar**
![besta](https://i.ibb.co/87NFG8F/besta.png)
Sebaliknya, *word cloud* untuk konten Besta Shankar menyoroti istilah-istilah seperti "pemerintah", "peningkatan", "pasar", "negara", dan "India". Istilah-istilah ini menunjukkan fokus pada isu-isu politik dan ekonomi, terutama yang terkait dengan kebijakan pemerintah, tren pasar, dan perkembangan nasional. Artikel-artikel Besta Shankar kemungkinan besar memberikan wawasan tentang peristiwa-peristiwa politik, kebijakan-kebijakan ekonomi, dan analisis pasar, dengan penekanan khusus pada konteks India.

**Insight** :
Secara keseluruhan, analisis ini menggarisbawahi keragaman topik yang tercakup dalam dataset, dengan penulis yang berbeda menunjukkan preferensi tematik yang berbeda berdasarkan konten yang mereka hasilkan. Memahami preferensi ini dapat membantu pembaca mengidentifikasi dan terlibat dengan artikel yang sesuai dengan minat dan kebutuhan informasi mereka.

### Analysis of 5 author content samples
| author             | top_5_words                      |
|--------------------|----------------------------------|
| nicy v.p           | [movie, film, also, nivin, malayalam] |
| ib times reporter  | [gold, price, ounce, year, reserve] |
| ken sunny          | [unit, sale, india, suv, car] |
| aditya bhat        | [game, pokemon, also, india, player] |
| arkadev ghoshal    | [said, state, also, isi, islamic] |
- **Nicy V.P:** Konten Nicy V.P sering kali berkisar pada industri film Malayalam, dengan seringnya menyebutkan film, film, dan aktor-aktor seperti Nivin. Hal ini menunjukkan fokus pada ulasan film, informasi terbaru dari industri, dan mungkin wawancara dengan aktor atau pembuat film.
- **IB Times Reporter:** Konten yang terkait dengan IB Times Reporter sering membahas topik-topik keuangan seperti harga emas, harga per ons, dan tren cadangan. Hal ini menunjukkan fokus pada berita ekonomi, analisis pasar, dan artikel terkait investasi, yang melayani pembaca yang tertarik dengan keuangan dan bisnis.
- **Ken Sunny:** Konten Ken Sunny tampaknya berpusat pada industri otomotif, khususnya di India, dengan menyebutkan penjualan unit, SUV, dan mobil. Hal ini menunjukkan fokus pada ulasan mobil, berita industri, dan berita terbaru di pasar otomotif India.
- **Aditya Bhat:** Konten Aditya Bhat sering kali mencakup diskusi tentang game, secara khusus menyebutkan game seperti Pokemon, serta tren game di India dan para pemainnya. Hal ini menunjukkan fokus pada berita, ulasan, dan pembaruan game, yang kemungkinan besar ditujukan untuk audiens penggemar game.
- **Arkadev Ghoshal:** Konten Arkadev Ghoshal sering menyebutkan negara, topik-topik Islam seperti ISI, dan kutipan-kutipan dari para pejabat. Hal ini menunjukkan fokus pada berita politik, perkembangan tingkat negara, dan mungkin analisis geopolitik, yang melayani pembaca yang tertarik dengan isu-isu terkini dan hubungan internasional.

**Insight** :
- Analisis ini mengungkapkan spesialisasi penulis yang berbeda, termasuk sinema Malayalam, keuangan, otomotif, game, dan politik.
- Konten setiap penulis mencerminkan keahlian mereka, mencakup topik-topik seperti film, harga emas, penjualan mobil, permainan Pokemon, dan perkembangan politik.
- Dataset ini menampilkan beragam topik berita, yang melayani berbagai minat dan preferensi pembaca.
- Memahami spesialisasi penulis memungkinkan rekomendasi konten yang disesuaikan berdasarkan preferensi pengguna.
- Sistem rekomendasi berita yang dipersonalisasi dapat memanfaatkan wawasan ini untuk meningkatkan keterlibatan dan kepuasan pengguna.

## Data Preparation
1. **Convert Column Names to Lowercase**: Dengan menstandarkan nama kolom menjadi huruf kecil, memastikan konsistensi dalam mengakses dan memanipulasi data. Hal ini mencegah kesalahan yang mungkin timbul dari operasi yang peka terhadap huruf besar-kecil dan membuat kode lebih mudah dibaca dan dipelihara.

2. **Cleaning Author Names**: Fungsi `clean_author_names` memastikan konsistensi dalam mengidentifikasi penulis di seluruh kumpulan data. Menghapus informasi tambahan menggunakan pola regex membantu membersihkan data yang berisik dan memastikan bahwa nama penulis direpresentasikan secara akurat. Mengubah nama menjadi huruf kecil dan menghapus spasi di depan/di belakang menghilangkan ketidakkonsistenan karena variasi dalam pemformatan. Menangani variasi dan singkatan memastikan bahwa nama penulis dicocokkan dengan benar, sehingga meningkatkan akurasi analisis berbasis penulis.

3. **Text Cleaning**:
   - **Lowercasing**: Mengubah teks menjadi huruf kecil akan menstandarkan teks, mengurangi kompleksitas data dan memastikan pemrosesan yang konsisten.
   - **Removing Punctuation and Special Characters**: Langkah ini menghilangkan noise yang tidak perlu dari teks, meningkatkan akurasi analisis selanjutnya dengan berfokus pada kata-kata yang bermakna.
   - **Tokenization**: Memecah teks menjadi kata-kata individual (token) memfasilitasi analisis lebih lanjut dan memungkinkan penghapusan stopwords dan lemmatization.
   - **Removing Stopwords**: Stopwords seperti 'dan', 'yang', dll., menambah sedikit nilai semantik dan dapat mengubah hasil analisis. Menghapusnya akan mengurangi noise dan fokus pada kata-kata yang lebih bermakna.
   - **Lemmatization**: Mengubah kata menjadi bentuk dasar atau akarnya membantu mengkonsolidasikan kata-kata yang mirip, mengurangi ukuran kosakata dan meningkatkan kemampuan model untuk menggeneralisasi berbagai variasi kata yang sama.

Teknik-teknik ini secara kolektif meningkatkan kualitas data dengan mengurangi noise, menstandarkan teks, dan meningkatkan relevansi kata untuk pemodelan. Untuk sistem rekomendasi, data teks yang lebih bersih dan terstandardisasi akan menghasilkan rekomendasi yang lebih akurat dan relevan dengan berfokus pada konten yang bermakna dan mengurangi dampak dari kata-kata yang tidak relevan.

## Modeling
| article_id | title                                                  | author           | date                | content                                                | url                                                 | similarity_score |
|------------|--------------------------------------------------------|------------------|---------------------|--------------------------------------------------------|-----------------------------------------------------|------------------|
| 664        | Fireman Box Office Controversy Producer Mil...         | Nicy V.P         | March 10, 2015 18:11 IST | Malayalam cinema industry is making headlines ...     | http://www.ibtimes.co.in/fireman-box-office-co... | 0.148865         |
| 2147       | Malayalam Cinema 2014 Top 10 Movies of the Year        | Nicy V.P         | December 18, 2014 11:40 IST | Malayalam cinema has given many reasons movie ...     | NaN                                                 | 0.144956         |
| 2176       | Tamil Film Producers Decide to Release Big Mov...       | Nicy V.P         | March 10, 2015 15:45 IST | Tamil film producers decision to release big ...     | http://www.ibtimes.co.in/tamil-film-producers-... | 0.141775         |
| 335        | Pasanga 2 Haiku movie review Live audience ...         | Prakash Upadhyaya| December 24, 2015 10:14 IST | Produced by actor Suriya Pasanga 2 -- also ...      | http://www.ibtimes.co.in/pasanga-2-haiku-movie... | 0.140491         |
| 2170       | Kerala Box Office Collection Mammootty Dulqu...        | Nicy V.P         | April 10, 2015 18:55 IST | The father and son duo of Malayalam cinema M...      | http://www.ibtimes.co.in/kerala-box-office-col... | 0.134959         |

Pada tahap ini, model sistem rekomendasi berbasis konten dikembangkan untuk memberikan rekomendasi artikel berita yang dipersonalisasi berdasarkan kemiripan konten tekstual artikel. Langkah-langkah berikut menguraikan prosesnya:
1. **TF-IDF Vectorization Parameters**:
   - **Stop Words**: Stop words adalah kata-kata umum dalam bahasa Inggris (misalnya, 'and', 'the', 'is') yang dihilangkan selama vektorisasi untuk memfokuskan pada konten yang bermakna. Mereka ditentukan menggunakan parameter `stop_words` di kelas `TfidfVectorizer`, disetel ke 'english'.
   - **TF-IDF Vectorization**: TF-IDF (Term Frequency-Inverse Document Frequency) merepresentasikan tingkat kepentingan setiap kata dalam sebuah dokumen relatif terhadap kumpulan dokumen. Frekuensi istilah (TF) mengukur seberapa sering sebuah istilah muncul dalam sebuah dokumen, sementara frekuensi dokumen terbalik (IDF) mengukur seberapa penting sebuah istilah di seluruh korpus. Kelas `TfidfVectorizer` menginisialisasi dan menyesuaikan vektorizer TF-IDF untuk mengubah data tekstual menjadi vektor fitur numerik.

2. **Similarity Calculation**:
   - **Cosine Similarity**: Cosine Similarity mengukur kosinus sudut antara dua vektor dan menentukan seberapa mirip keduanya. Dalam konteks ini, ini mengukur kemiripan antara vektor TF-IDF dari artikel berita yang berbeda. Kemiripan kosinus berkisar antara -1 hingga 1, di mana 1 menunjukkan dokumen yang identik, 0 menunjukkan dokumen yang ortogonal (yaitu, tidak memiliki kemiripan), dan -1 menunjukkan dokumen yang sama sekali berbeda. Fungsi `cosine_similarity` menghitung kemiripan kosinus berpasangan antara vektor TF-IDF semua artikel.

3. **Top-N recommendations**:
   - **Top-N Recommendation Function**: Fungsi `content_based_recommendation` mengambil kueri teks sebagai masukan dan mengembalikan artikel rekomendasi top-N berdasarkan kemiripannya dengan kueri. Fungsi ini melakukan prapemrosesan kueri, mengubahnya menjadi vektor TF-IDF, menghitung skor kemiripan kosinus antara vektor kueri dan vektor semua artikel, mengurutkan artikel berdasarkan skor ini, dan mengembalikan artikel top-N dengan skor kemiripan tertinggi. Parameter `top_n` menentukan jumlah rekomendasi yang akan dikembalikan, dan fungsi ini mengecualikan kueri itu sendiri dari rekomendasi.

## Evaluation
### Similarity Score
|   article_id   | similarity_score |
|:--------------:|:-----------------:|
|      664       |      0.148865     |
|      2147      |      0.144956     |
|      2176      |      0.141775     |
|      335       |      0.140491     |
|      2170      |      0.134959     |

### Evaluation Analysis:
- **Advantages**:
  1. **Relevance**: Artikel yang direkomendasikan terkait dengan genre film horor, yang sesuai dengan permintaan pengguna.
  2. **Personalization**: Sistem menyesuaikan rekomendasi berdasarkan konten tekstual artikel, memastikan relevansi dengan minat pengguna.
  3. **Diverse Recommendations**: Meskipun kueri secara khusus menyebutkan film horor, rekomendasinya mencakup artikel yang terkait dengan kontroversi film, film terbaik tahun ini, dan ulasan film, sehingga memberikan pilihan yang beragam.
  4. **Scalability**: Sistem ini dapat menskalakan secara efisien untuk menangani volume besar artikel dan kueri pengguna, sehingga cocok untuk aplikasi dunia nyata.

- **Limitations**:
  1. **Limited Context**: Sistem ini hanya mengandalkan konten tekstual artikel untuk menghasilkan rekomendasi. Hal ini dapat mengabaikan faktor-faktor lain seperti preferensi pengguna untuk aktor, sutradara, atau sub-genre tertentu dalam film horor.
  2. **Lack of Serendipity**: Karena rekomendasi hanya didasarkan pada kemiripan tekstual, sistem mungkin tidak memperkenalkan pengguna pada konten baru atau tak terduga yang mungkin mereka sukai tetapi tidak secara eksplisit disebutkan dalam kueri.
  3. **Cold Start Problem**: Sistem mungkin kesulitan untuk memberikan rekomendasi yang akurat untuk topik baru atau topik khusus dengan data yang tersedia terbatas, karena sistem ini sangat bergantung pada konten artikel yang sudah ada untuk perhitungan kemiripan.
  4. **Difficulty with Ambiguous Queries**: Jika kueri ambigu atau tidak jelas, seperti 'rekomendasi film' tanpa menentukan genre, sistem mungkin kesulitan untuk memberikan rekomendasi yang relevan.

### System Performance:
Sistem secara efektif merekomendasikan artikel yang terkait dengan film horor berdasarkan kueri masukan. Sistem ini menunjukkan kemampuan untuk memahami maksud pengguna dan memberikan saran yang relevan. Namun, kinerja sistem dapat bervariasi berdasarkan kekhususan dan kejelasan input pengguna. Secara keseluruhan, meskipun sistem rekomendasi berbasis konten menawarkan rekomendasi yang dipersonalisasi dan relevan, sistem ini dapat memperoleh manfaat dari peningkatan untuk mengatasi keterbatasan seperti masalah cold start dan kurangnya pemahaman kontekstual.


