1. QR code dapat tercuri dan digunakan oleh penyerang, untuk mencegah serangan ini QR code dapat di atur agar hanya sekali pakai atau merefresh QR code dalam jangka waktu tertentu.
2. Backup Code dapat tercuri oleh man in the middle untuk mencegah hal teresebut terjadi kita dapat melakukan enkripsi atau hashing pada backup code.
3. Serangan keylogger dengan serangan ini penyerang dapat merekam kode 2FA yang kita ketik dan menggunakan kode tersebut untuk masuk, untuk mencegah hal tersebut terjadi kita dapat menggunakan onetime code atau melakukan refresh code dalam jangka waktu tertentu.
4. penyerang dapat melakukan bruteforce pada bagian memasukan 6 digit kode untuk mencegah hal ini terjadi dapat dilakukan beberapa cara seperti memberikan penalti jika salah memasukan kode setelah beberapa kali percobaan dan menggunakan variasi kode yang banyak selain itu melakukan refresh code dalam jangka waktu tertentu.
5. SQL injection pada halaman login dapat dilakukan jika tidak melakukan pencegahan terhadap karakter karakter berbahaya dan membatasi jumlah karakter yang dapat dimasukan, dapat dicegah dengan mengatur format kotak pengisian, memvalidasi input, menggunakan parameterized SQL query, menggunakan SQL escape string, mematikan notifikasi error, mengatur privilege pada database, dan menggunakan WAF maupun IPS.
6. Attack man in the middle juga dapat dilakukan oleh penyerang dan mengambil data seperti backup code saat dimasukan, dapat diatasi dengan menggunakan sertifikat SSL yang berkualitas dan jangan menggunakan WIFI publik atau bisa juga menggunakan VPN.