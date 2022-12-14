| Vulnerability | Entrypoint | Parameter | Affected page | WAF mitigations |
|---|---|---|---|---|
1. | HTML injection (a limitated XSS where the user can inject only some types of tags) | application.com/support  | ticketBody | application.com/backoffice/viewTicket | tags that work: <a href= , <a src= |
2. | Cross Site Request Forgery | not applicable | not applicable | the web site is not protected with CSRF tokens | not applicable |
3. | Reflected Cross-Site-Scripting (POST) | application.com/userProfile  | userFullName | application.com/userProfile  | yes |
4. | Insecure Direct Object Reference | DELETE application.com/expenses/{id} | id (url parameter) | http://application.com/expenses/{id} - deletes file | not applicable |
5. | Insecure Direct Object Reference | application.com/expenses/{id} | id (url parameter) | application.com/expenses/{id} — returns different responses if id exists or not | not applicable |

saya menaruh kasus HTML injection pada urutan pertama karena pada kasus tersebut penyerang dapat menginject atau memasukan script maupun link URL berbahaya yang dapat menjadi fatal. 
cara mitigasi:
-URL encoding
-Implement Content Security Policy
-Validate the URL
-URL White Listing
-Remove javascript
dokumentasi: https://www.developsec.com/2017/09/06/javascript-in-an-href-or-src-attribute/

kasus CSRF pada urutan kedua karena penyerang dapat request palsu pada website jika seseorang membuka website/link yang dapat melakukan request palsu berbahaya. Salah satu cara memitigasi CSRF ini dapat dengan cara menggunakan CSRF Token yang dapat memberikan token yang unik untuk setiap user session dan memiliki random value yang banyak agar sulit ditebak. Selain itu jika menggunakan CSRF Token pada server menyebabkan masalah dapat dilakukan cara lain dengan menggunakan double submit cookie, double submit cookie mudah dilakukan dengan cara kita mengirim value pada cookie dan request parameter lalu server melakukan penyocokan pada value cookie dan request value. Dokumentasi cara mitigasi CSRF: https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html

Lalu kasus reflected XSS pada urutan ketiga karena WAF dapat melakukan mitigasi pada XSS tetapi tetap harus dilakukan pengamanan karena dikhawatirkan terdapat celah untuk XSS dapat melalui WAF tersebut. Untuk memitigasi XSS kita perlu untuk melakukan sanitasi pada kode HTML kita dengan menggunakan DOMpurify. Dokumentasi untuk memitigasi XSS: https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html

Untuk kasus IDOR penyerang dapat mendelete data expense milik orang lain dengan mengganti ID pada URL parameter, dan kerugian yang terjadi tidak separah serangan lain. cara memitigasi atau mencegah terjadinya IDOR adalah dengan melakukan hashing pada ID sehingga tidak mudah ditebak dan tidak dapat memodifikasi data milik orang lain. Dokumentasi: https://cheatsheetseries.owasp.org/cheatsheets/Insecure_Direct_Object_Reference_Prevention_Cheat_Sheet.html

Untuk kasus IDOR kedua melakukan serangan pada expense milik orang lain juga tetapi hanya dapat melihat expense milik orang lain dan tidak menghapus data milik orang lain, jadi kerugian tidak fatal. Cara mitigasi sama seperti IDOR yang sebelumnya dengan melakukan hashing pada ID pada URL sehingga tidak mudah di tebak dan memodifikasi atau melihat data milik orang lain. Dokumentasi: https://cheatsheetseries.owasp.org/cheatsheets/Insecure_Direct_Object_Reference_Prevention_Cheat_Sheet.html
