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

### Model Data

![image](https://user-images.githubusercontent.com/47923906/190261967-47f5a1c7-391c-4ef8-bb02-f832002dbddd.png)

### Menambahkan pesan ke Firestore

![Menambahkan form pesan](./images/06.png)

* Pengguna yang mengeklik tombol KIRIM akan memicu cuplikan kode di bawah ini. Itu menambahkan isi bidang input pesan ke koleksi guestbook dari database. Secara khusus, metode addMessageToGuestBook menambahkan konten pesan ke dokumen baru (dengan ID yang dibuat secara otomatis) ke koleksi guestbook.

```dart
  Future<DocumentReference> addMessageToGuestBook(String message) {
    if (_loginState != ApplicationLoginState.loggedIn) {
      throw Exception('Must be logged in');
    }

    return FirebaseFirestore.instance
        .collection('guestbook')
        .add(<String, dynamic>{
      'text': message,
      'timestamp': DateTime.now().millisecondsSinceEpoch,
      'name': FirebaseAuth.instance.currentUser!.displayName,
      'userId': FirebaseAuth.instance.currentUser!.uid,
    });
  }
```

### Menghubungkan UI ke database

memodifikasi di widget HomePage

```dart
     Consumer<ApplicationState>(
            builder: (context, appState, _) => Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                if (appState.loginState == ApplicationLoginState.loggedIn) ...[
                  const Header('Discussion'),
                  GuestBook(
                    addMessage: (message) =>
                        appState.addMessageToGuestBook(message),
                  ),
                ],
              ],
            ),
          ),
````

### Konsol Firebase

![Tampilan konsol](./images/07.png)

### Sinkronisasi Pesan

![Sinkronisasi Pesan](./images/08.png)

* Pesan yang dibuat sebelumnya di database ditampilkan di aplikasi.

## Menambahkan Aturan Keamanan Dasar

![Keamanan Dasar](./images/09.png)

## Catat status RSVP peserta

![Catat status RSVP peserta](./images/10.png)

Update Rules Cloud Firestore

```bash
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /guestbook/{entry} {
      allow read: if request.auth.uid != null;
      allow write:
      if request.auth.uid == request.resource.data.userId
          && "name" in request.resource.data
          && "text" in request.resource.data
          && "timestamp" in request.resource.data;
    }
    match /attendees/{userId} {
      allow read: if true;
      allow write: if request.auth.uid == userId
          && "attending" in request.resource.data;
    }
  }
}

```



















