# #29 | Codelab: Firebase Flutter Plugin Bagian 2 

## Studi Kasus

* Membuat aplikasi obrolan RSVP dan buku tamu acara di Android, iOS, Web, dan MacOS menggunakan Flutter.
* Mengautentikasi pengguna dengan Firebase Authentication dan menyinkronkan data menggunakan Cloud Firestore. 

## Tujuan Praktikum

* Mahasiswa mampu memanfaatkan sikronisasi data menggunakan Cloud Firestore
* Mahasiswa mampu membuat pesan chat sederhana dengan plugin cloud firestore

## Link Praktikum

Berikut ini adalah link untuk praktikum: [link](https://firebase.google.com/codelabs/firebase-get-to-know-flutter?hl=id#1)

# Praktikum

## 1. Menambahkan Login Pengguna (RSVP)

![Awal otentikasi](./images/01.png)

* Berikut adalah awal dari alur otentikasi, di mana pengguna dapat menekan tombol RSVP, untuk memulai formulir email. 

![Formulir email](./images/02.png)

* Setelah memasukkan email, sistem mengkonfirmasi jika pengguna sudah terdaftar, dalam hal ini pengguna dimintai kata sandi, atau jika pengguna tidak terdaftar, maka mereka pergi melalui formulir pendaftaran. 

![Formulir pendaftaran](./images/03.png)

* Pastikan untuk mencoba memasukkan kata sandi pendek (kurang dari enam karakter) untuk memeriksa alur penanganan kesalahan. Jika pengguna terdaftar, mereka akan melihat kata sandi sebagai gantinya. 

![Sign In](./images/04.png)

* Setelah pengguna berhasil masuk, mereka akan melihat halaman RSVP. 

![Halaman RSVP](./images/05.png)

* Pengguna dapat klik logout untuk keluar dari aplikasi.

## 2. Menulis pesan ke Cloud Firestore

Model Data

![image](https://user-images.githubusercontent.com/47923906/190261967-47f5a1c7-391c-4ef8-bb02-f832002dbddd.png)



