# Analisis Pelanggaran Prinsip SOLID (Sebelum Refactoring)

analisis "Code Smell" pada sistem validasi registrasi mahasiswa sebelum di *refactoring*. Kode `ValidatorManager` menjadi GodClass karena menangani berbagai hal dan melanggar tiga prinsip utama SOLID.

## 1. Pelanggaran Single Responsibility Principle (SRP)
**Prinsip:** Sebuah kelas harus memiliki satu, dan hanya satu, alasan untuk berubah.

**Analisis:**
Kelas `ValidatorManager` memiliki lebih dari satu tanggung jawab (tanggung jawab ganda):
* Mengatur alur eksekusi validasi registrasi.
* Memiliki logika detail pengecekan jumlah SKS.
* Memiliki logika detail pengecekan mata kuliah prasyarat.

**kelemahan:** Jika ada peraturan seperti jumlah SKS yang perlu perubahan, kita harus mengubah kelas yang sama. Hal ini menciptakan "God Class" yang rawan terjadi kesalahn.

---

## 2. Pelanggaran Open/Closed Principle (OCP)
**Prinsip:** Entitas perangkat lunak harus terbuka untuk ekstensi, tetapi tertutup untuk modifikasi.

**Analisis:**
Logika validasi di dalam metode `validasi_registrasi` menggunakan struktur percabangan `if/else` untuk menentukan tipe validasi berdasarkan parameter string. Jika ada kebutuhan untuk menambah validasi baru (contoh: Validasi Keuangan atau Validasi Berkas), pengembang **dipaksa untuk membuka dan mengubah** kode sumber yang sudah ada.

**kelemahan:** jika ingin menambahkan fitur baru, ada risiko merusak fungsi yang sudah berjalan. Kode bersifat kaku (*rigid*) karena tidak bisa diperbarui tanpa memodifikasi isi kelasnya.

---

## 3. Pelanggaran Dependency Inversion Principle (DIP)
**Prinsip:** Modul tingkat tinggi tidak boleh bergantung pada modul tingkat rendah. Keduanya harus bergantung pada abstraksi.

**Analisis:**
Kelas `ValidatorManager` (modul tingkat tinggi) bergantung  pada logika pengecekan (modul tingkat rendah) yang dicode secara *hardcoded*. Tidak ada kontrak atau abstraksi yang menjadi perantara.

**Kelemahan:** Kode menjadi sangat terikat satu sama lain (*tight coupling*). Membuat komponen sulit untuk diuji secara mandiri (*unit testing*) danm harus mengubah sistem yang ada jika ingin mengganti.

---

## Kesimpulan
Kode awal terindikasi **Code Smell** karena melanggar tiga prinsip SOLID. Dengan melakukan *refactoring* program akan menjadi lebih terstruktur dan mudah dikembangkan.
