<h1 align="center">MindCheck</h1> <br>

<h3 align="center">Sistem Pakar Diagnosa Gangguan Kesehatan Mental Remaja</h3>
<p align="center">
  <img src="https://github.com/user-attachments/assets/example-placeholder" alt="Logo" width="200"/>
</p>

<p align="center">
  <strong>AINUL HAYAT. H</strong><br/><br/>
  <strong>D0223317</strong><br/><br/>
  <strong>Framework Web Based</strong><br/><br/>
  <strong>2025</strong>
</p>

<h3>Role dan Fitur</h3>

## 🧑‍⚕️ Admin

| Fitur                     | Deskripsi                                               |
| ------------------------- | ------------------------------------------------------- |
| Kelola data pengguna      | Tambah, edit, hapus akun psikolog dan pengguna          |
| Kelola basis pengetahuan  | Menambah, edit, dan hapus data gejala dan diagnosa      |
| Kelola hasil konsultasi   | Melihat dan mengelola hasil diagnosa pengguna           |
| Manajemen rules           | Mengatur relasi antara gejala dan gangguan mental       |

## 👩‍⚕️ Psikolog

| Fitur                          | Deskripsi                                                  |
| ------------------------------ | ---------------------------------------------------------- |
| Lihat hasil diagnosa pengguna  | Melihat histori diagnosa dari pengguna                     |
| Evaluasi lanjutan              | Menambah catatan atau rekomendasi terhadap hasil diagnosa  |
| Umpan balik                    | Memberikan feedback atau rujukan lanjutan                  |

## 🧑 Remaja (User)

| Fitur                              | Deskripsi                                                           |
| ---------------------------------- | ------------------------------------------------------------------- |
| Registrasi dan login               | Membuat akun dan masuk ke sistem                                    |
| Konsultasi (diagnosa mandiri)     | Menjawab pertanyaan / gejala yang dirasakan untuk mendapatkan hasil |
| Lihat riwayat diagnosa             | Melihat hasil konsultasi sebelumnya                                 |
| Rekomendasi                        | Mendapatkan saran atau rujukan berdasarkan hasil diagnosa           |

<h3>Tabel-tabel database beserta field dan tipe datanya</h3>

<h3>Tabel Users</h3>

| Kolom       | Tipe      | Keterangan                         |
| ----------- | --------- | ---------------------------------- |
| id          | bigint    | Primary key                        |
| name        | string    | Nama pengguna                      |
| email       | string    | Email unik                         |
| password    | string    | Password terenkripsi               |
| role        | enum      | admin, psikolog, user              |
| created_at  | timestamp | Waktu dibuat                       |
| updated_at  | timestamp | Waktu diubah                       |

<h3>Tabel Gejalas</h3>

| Kolom       | Tipe      | Keterangan               |
| ----------- | --------- | ------------------------ |
| id          | bigint    | Primary key              |
| kode        | string    | Kode gejala (misal: G01) |
| nama        | string    | Nama atau deskripsi gejala |
| created_at  | timestamp |                          |
| updated_at  | timestamp |                          |

<h3>Tabel Gangguans</h3>

| Kolom       | Tipe      | Keterangan                         |
| ----------- | --------- | ---------------------------------- |
| id          | bigint    | Primary key                        |
| kode        | string    | Kode gangguan (misal: D01)         |
| nama        | string    | Nama gangguan                      |
| deskripsi   | text      | Penjelasan gangguan                |
| solusi      | text      | Saran penanganan                   |
| created_at  | timestamp |                                    |
| updated_at  | timestamp |                                    |

<h3>Tabel Rules</h3>

| Kolom        | Tipe    | Keterangan                                       |
| ------------ | ------- | ------------------------------------------------ |
| id           | bigint  | Primary key                                      |
| gangguan_id  | foreign | ID dari tabel gangguans                          |
| gejala_id    | foreign | ID dari tabel gejalas                            |
| nilai_cf     | float   | Nilai certainty factor (CF) dari gejala terhadap gangguan |

<h3>Tabel Konsultasis</h3>

| Kolom        | Tipe      | Keterangan                                    |
| ------------ | --------- | --------------------------------------------- |
| id           | bigint    | Primary key                                   |
| user_id      | foreign   | ID dari pengguna                              |
| hasil_diagnosa | string  | Nama gangguan hasil diagnosa                  |
| nilai_cf     | float     | Nilai keyakinan akhir                         |
| created_at   | timestamp |                                               |

<h3>Tabel konsultasi_detail</h3>

| Kolom          | Tipe    | Keterangan                                   |
| -------------- | ------- | -------------------------------------------- |
| id             | bigint  | Primary key                                  |
| konsultasi_id  | foreign | ID dari konsultasi                           |
| gejala_id      | foreign | Gejala yang dipilih oleh pengguna            |
| nilai_cf_user  | float   | Nilai keyakinan pengguna terhadap gejala itu |

<h3>Relasi Antar Tabel</h3>

| Tabel Asal  | Tabel Tujuan       | Jenis Relasi | Keterangan                                                              |
| ----------- | ------------------ | ------------ | ----------------------------------------------------------------------- |
| users       | user\_profiles     | One to One   | Setiap user memiliki satu profil tambahan (alamat, usia, jenis kelamin) |
| users       | konsultasis        | One to Many  | Satu user dapat melakukan banyak sesi konsultasi                        |
| konsultasis | konsultasi\_detail | One to Many  | Satu konsultasi memiliki banyak detail gejala yang dipilih              |
| gejalas     | konsultasi\_detail | Many to One  | Banyak detail konsultasi bisa merujuk ke satu gejala yang sama          |
| gangguans   | rules              | One to Many  | Satu gangguan memiliki banyak aturan (rules) gejala                     |
| gejalas     | rules              | One to Many  | Satu gejala bisa digunakan dalam banyak rules                           |
| gangguans   | gejalas            | Many to Many | Melalui tabel **rules**, menghubungkan banyak gejala ke banyak gangguan |
| users       | psikolog\_profiles | One to One   | Psikolog punya data tambahan (spesialisasi, lisensi, pengalaman)        |

