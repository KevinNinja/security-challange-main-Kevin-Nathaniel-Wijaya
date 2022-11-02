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

kasus CSRF pada urutan kedua karena penyerang dapat request palsu pada website jika seseorang membuka website/link yang dapat melakukan request palsu berbahaya. Salah satu cara memitigasi CSRF ini dapat dengan cara menggunakan CSRF Token yang dapat memberikan token yang unik untuk setiap user session dan memiliki random value yang banyak agar sulit ditebak. Dokumentasi cara mitigasi CSRF: https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html

Lalu kasus reflected XSS pada urutan ketiga karena WAF dapat melakukan mitigasi pada XSS tetapi tetap harus dilakukan pengamanan karena dikhawatirkan terdapat celah untuk XSS dapat melalui WAF tersebut. Dokumentasi untuk memitigasi XSS: https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html

lalu untuk kasus IDOR penyerang dapat mendelete dan melihat data milik orang lain dengan mengganti ID, kerugian yang terjadi tidak separah serangan lain. cara memitigasi atau mencegah terjadinya IDOR adalah dengan melakukan hashing pada ID sehingga tidak mudah ditebak. Dokumentasi: https://cheatsheetseries.owasp.org/cheatsheets/Insecure_Direct_Object_Reference_Prevention_Cheat_Sheet.html