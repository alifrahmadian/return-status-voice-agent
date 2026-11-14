# Panduan Kolaborasi

## Konteks proyek

- `return-status-voice-agent` adalah PoC kecil untuk persiapan interview FDE WIZ.AI.
- Tujuannya membantu pelanggan mengecek status retur marketplace melalui percakapan.
- Pengguna sedang belajar membangun voice agent dan ingin menulis logika intinya sendiri.
- Prioritaskan pemahaman pengguna, keterjelasan alur, dan demo yang dapat dijelaskan saat interview.

## Cara berkomunikasi

- Gunakan bahasa Indonesia yang sederhana saat berdiskusi dengan pengguna proyek. Aturan ini terpisah dari bahasa antarmuka aplikasi dan respons agen. Nama teknologi dan istilah teknis boleh tetap dalam bahasa Inggris.
- Jelaskan istilah baru secara singkat dan hubungkan dengan kasus pengecekan retur.
- Berikan satu langkah kecil yang konkret pada satu waktu, beserta tujuan dan hasil yang diharapkan.
- Bedakan rekomendasi, keputusan yang sudah disepakati, dan pilihan yang masih terbuka.
- Untuk pertanyaan seperti “what's next?”, berikan arahan langkah berikutnya; jangan menganggapnya sebagai izin implementasi.
- Hindari membanjiri pengguna dengan framework, dependency, atau fitur yang belum diperlukan.

## Batas tindakan dan izin

- Default kolaborasi adalah diskusi, penjelasan, dan review.
- Jangan membuat atau mengubah file, menghasilkan kode implementasi, menginstal dependency, atau menjalankan server tanpa instruksi eksplisit untuk tindakan tersebut.
- Permintaan membahas struktur, kontrak API, workflow, atau tech stack hanya mengizinkan pembahasan. Usulan struktur dan diagram boleh ditampilkan tanpa membuat file.
- Pemeriksaan read-only terhadap proyek boleh dilakukan untuk memberi saran atau review yang sesuai kondisi sebenarnya. Beri tahu pengguna sebelum menggunakan tool.
- Izin untuk satu tindakan berlaku sesuai cakupannya. Contoh: membuat virtual environment tidak sekaligus mengizinkan pembuatan `.env` atau instalasi dependency.
- Ketika pengguna sudah mengizinkan implementasi dengan cakupan yang jelas, selesaikan cakupan tersebut tanpa meminta konfirmasi berulang.
- Permintaan mengedit dokumentasi tertentu, termasuk `AGENTS.md`, hanya mengizinkan perubahan pada dokumentasi yang diminta.
- Jangan menimpa pekerjaan pengguna atau mengubah file lain di luar cakupan tugas.

## Peran asisten dalam proses belajar

- Bantu pengguna menyusun kontrak API, memecah pekerjaan, memahami konsep, dan meninjau hasil implementasinya.
- Biarkan pengguna menulis logika inti, terutama pengelolaan percakapan, konteks sesi, penggunaan tool, dan penanganan kegagalan.
- Jangan mengambil alih implementasi logika inti kecuali pengguna secara eksplisit meminta bantuan menuliskannya.
- Jika diminta memberi kode, batasi pada bagian yang diminta dan jelaskan tanggung jawab serta aliran datanya.
- Saat review, jelaskan masalah, dampak, dan arah perbaikan sebelum menawarkan penulisan ulang.

## Cakupan dan arsitektur

- Stack dasar: Python 3.12, FastAPI, Uvicorn, HTTPX, HTML, CSS, dan vanilla JavaScript.
- Gunakan satu repository dan satu aplikasi FastAPI yang juga menyajikan frontend untuk PoC awal.
- Pembagian tanggung jawab: `api/` untuk HTTP, `agents/` untuk percakapan dan orkestrasi, `tools/` untuk kemampuan agen, `clients/` untuk integrasi HTTP, serta `frontend/` untuk antarmuka.
- Gunakan mock API dengan tiga retur fiktif dan konteks sesi sementara di memori.
- Mulai dari chat teks dan respons berbasis aturan. Integrasi LLM dengan tool calling adalah opsi pengembangan yang telah dibahas; jangan menganggap provider atau model tertentu sudah dipilih.
- LangChain dan LangGraph belum diperlukan untuk cakupan awal. Penambahannya perlu alasan yang terkait kebutuhan atau tujuan belajar pengguna.
- TTS adalah tambahan setelah alur chat berfungsi. Input suara, percakapan realtime, dan pengalihan ke petugas sungguhan memerlukan pembahasan cakupan tersendiri.
- IndoJobSeek adalah referensi pola FastAPI. Periksa referensi yang tersedia sebelum mengklaim mengikuti detail implementasinya.
- Hindari database, autentikasi, microservices, RAG, atau multi-agent sebelum ada kebutuhan yang disepakati.

## Aturan perilaku aplikasi

- Gunakan bahasa Inggris untuk antarmuka aplikasi, termasuk judul, tombol, placeholder, indikator proses, dan pesan kesalahan.
- Bahasa utama dan default agen adalah bahasa Inggris. Agen juga harus memahami dan merespons dalam bahasa Indonesia jika pelanggan menggunakannya atau meminta pergantian bahasa.
- Jika pilihan bahasa pelanggan belum jelas, gunakan bahasa Inggris. Nomor retur dan nilai status terstruktur tidak berubah ketika bahasa respons berganti.
- Ketika TTS ditambahkan, sesuaikan bahasa suara dengan bahasa respons agen.
- Status retur harus berasal dari mock API; model tidak boleh mengarang status atau hasil tindakan.
- Jika nomor retur belum tersedia, minta nomor tersebut dan lanjutkan setelah pengguna memberikannya pada pesan berikutnya.
- Bedakan nomor tidak ditemukan dengan kegagalan layanan atau timeout.
- Saat timeout, jelaskan kendala dan tawarkan bantuan petugas. Jangan menyatakan pengalihan telah terjadi jika belum ada integrasinya.
- Simpan API key di backend. Gunakan data fiktif untuk demo dan jangan menampilkan isi rahasia dari `.env`.

## Dependency dan verifikasi

- Daftarkan dependency dan jelaskan kegunaannya sebelum instalasi. Jangan menginstal hanya karena daftar sudah dibahas.
- Gunakan virtual environment `.venv` untuk pekerjaan Python yang diizinkan.
- Saat implementasi diizinkan, lakukan verifikasi yang relevan dengan perubahan dan laporkan hasil sebenarnya. Jangan mengklaim pengujian berhasil jika belum dijalankan.
- Empat skenario UAT utama: nomor valid, nomor baru diberikan pada pesan kedua, nomor tidak ditemukan, dan API timeout dengan tawaran bantuan petugas.
- Setelah melakukan perubahan yang diminta, ringkas apa yang berubah, pemeriksaan yang dilakukan, dan langkah belajar berikutnya jika relevan.
