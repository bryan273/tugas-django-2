# Tugas 2 PBP
Link hasil deploy aplikasi : [link](https://tugas-django-bryan-1.herokuapp.com/katalog/)

## Request-Response Django Lifecycle
<img width="491" alt="image" src="https://user-images.githubusercontent.com/88226713/189522302-0e3f9028-ca2e-4a72-8cd2-399cc94abaa2.png">

* Ketika user / client melakukan _request_ untuk ke server melalui _link_ url atau _form_, django akan mencocokan url yang di-_request_ dengan url yang sudah didefinisikan pada file urls.py.
* Setiap url akan dipetakan ke fungsi tertentu yang berada pada file views.py yang akan memanggil fungsi _view_. 
* Fungsi view ini akan melakukan _query_ terhadap database dengan memanggil objek yang terdapat pada models.py sebagai penghubung. 
* Setelah itu view function akan mengembalikan _response_  dengan format HTML (berkas html).
* Lalu hasilnya akan dirender oleh template yang akan men-_display_ konten yang akan dilihat oleh user / client.

## Alasan Virtual Environment dipakai di Django
Virtual environment merupakan sebuah wadah virtual yang digunakan untuk menampung _dependecies_ dan _library_ agar terisolasi dari _dependencies_ utama. 

Setiap proyek yang akan kita kerjakan, memerlukan _third-party packages_ Python yang unik. Bila kita terus mengunduh semua packages di _environment_ yang sama pada setiap projek, hal itu dapat merusak alat sistem atau proyek sebelumnya yang mempunyai _dependencies_ mereka masing-masing.

Oleh karena itu, setiap kita memulai suatu proyek baru, kita harus meng-_setup_ _virtual environment_ yang baru dengan _dependencies_ dan versinya tertentu untuk sebuah proyek. 

## Proyek Django tanpa Virtual Environment
Jika kita ingin membuat sebuah proyek Django tanpa Virtual Environment, tentu saja itu sangat memungkinkan. Penggunaan Virtual Environment digunakan untuk mengorganisir _dependencies_ khusus dan versinya pada setiap proyek untuk memisahkan adanya _overlap_ versi _dependencies_ pada setiap proyek dan mencegah gangguan sistem lainnya.

Bila aplikasi yang ingin dibuat hanya aplikasi kecil yang tidak akan digunakan oleh siapa pun selain diri sendiri dan mungkin hanya untuk sementara, maka kita tidak terlalu membutuhkan _virtual environment_.

## Langkah-langkah implementasi
1. Membuat sebuah fungsi pada views.py yang dapat melakukan pengambilan data dari model dan dikembalikan ke dalam sebuah HTML.

Di dalam views.py, dibuat fungsi view (show_katalog) dengan parameter _request_ dari user. Fungsi ini menggunakan class dari model yang akan memanggil query ke database dan menyimpan hasil query tersebut ke dalam variabel data_katalog. Setelah itu, katalog.html akan di-render dan ditambahkan pula context pada pengembalian fungsi render yang dapat dimunculkan pada halaman HTML. 

2. Membuat sebuah routing untuk memetakan fungsi yang telah kamu buat pada views.py.

Routing dilakukan dengan cara menambahkan `path('katalog/', include('katalog.urls'))` pada urls.py di project_django. Routing dilakukan ke urls.py pada katalog. Kemudian urls.py ini akan menjalankan fungsi view show_katalog yang berada di views.py.

3. Memetakan data yang didapatkan ke dalam HTML dengan sintaks dari Django untuk pemetaan data template.

Pemetaan data template dilakukan dari proses _render_ melalui fungsi view pada views.py ke katalog.html. Pada saat render akan dilakukan _mapping_ dengan menggunakan sintaks khusus template pada Django, yaitu `{{data}}`. Data yang terdapat pada konteks akan di _mapping_ ke halaman html tersebut. Selain itu digunakan _looping_ juga terhadap list yang katalog untuk mengambil data dari database yang akan ditampilkan.

4. Melakukan deployment ke Heroku terhadap aplikasi yang sudah kamu buat sehingga nantinya dapat diakses oleh teman-temanmu melalui Internet.

Tahap deployment dilakukan dengan menghubungkan app heroku dengan repository yang terdapat pada github. Setelah itu aplikasi di deploy dan di-run `python manage.py loaddata initial_katalog_data.json` di heroku console agar data ter-_load_. Kemudian diperlukan juga untuk memasukkan variabel HEROKU_APP_NAME dan HEROKU_API_KEY di github secret agar dapat terhubung langsung ke heroku.
