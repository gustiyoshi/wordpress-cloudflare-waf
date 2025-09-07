# WordPress Cloudflare WAF
Cloudflare custom security rules yang saya pakai untuk menambah lapisan keamanan di situs WordPress.
Pastikan **Orange Cloud** sudah aktif, buat custom security rules dengan konfigurasi berikut:
* Rules name: ⁠`WordPress Hardening`. Boleh diisi nama lain, yang penting deskriptif.
* Di bagian **When incoming requests match…**, klik **Edit Expression**, lalu copy-paste kode di bawah ini:
~~~
((http.request.uri.path eq "/wp-login.php" and not (http.cookie contains "wordpress_logged_in_")) or (http.request.uri.path eq "/xmlrpc.php") or ((starts_with(http.request.uri.path, "/wp-admin/") or http.request.uri.path eq "/wp-admin") and not (ends_with(http.request.uri.path, "/admin-ajax.php")) and not (ends_with(http.request.uri.path, "/admin-post.php")) and not (http.cookie contains "wordpress_logged_in_")) or (starts_with(http.request.uri.path, "/pma/")) or (starts_with(http.request.uri.path, "/phpmyadmin/")))
~~~
* Di bagian **Then take action...**, pilih `⁠Managed Challenge`, lalu klik **Deploy**.
