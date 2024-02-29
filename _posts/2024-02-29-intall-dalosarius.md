## 1. Persiapkan Sistem:
Pastikan sistem Ubuntu Anda diperbarui dengan menjalankan perintah:

bash
sudo apt update
sudo apt upgrade
## 2. Instal Dependensi:
Install beberapa paket dependensi yang diperlukan:

bash
sudo apt install apache2 mariadb-server php php-mysql php-gd php-common php-curl php-mail php-mail-mime php-pear php-db php-mbstring php-xml composer
## 3. Unduh Daloradius:
Unduh Daloradius dari repositori resmi atau GitHub:

bash
git clone https://github.com/lirantal/daloradius
## 4. Pindah ke Direktori Daloradius:
Pindah ke direktori Daloradius yang baru diunduh:

bash
cd daloradius
## 5. Instal Daloradius:
Instal Daloradius dan ikuti petunjuk yang muncul:

bash
sudo composer install
## 6. Salin Berkas Konfigurasi:
Salin berkas konfigurasi dan sesuaikan dengan kebutuhan Anda:

bash
sudo cp /var/www/html/daloradius/library/daloradius.conf.php.example /var/www/html/daloradius/library/daloradius.conf.php
## 7. Impor Skema Database:
Impor skema database ke MySQL/MariaDB:

bash
sudo mysql -u root -p radius < /var/www/html/daloradius/contrib/db/fr2-mysql-daloradius-and-freeradius.sql
## 8. Atur Hak Akses:
Atur hak akses untuk folder Daloradius:

bash
sudo chown -R www-data:www-data /var/www/html/daloradius
## 9. Restart Apache:
Restart layanan Apache untuk menerapkan perubahan:

bash
sudo systemctl restart apache2
## 10. Akses Daloradius melalui Browser:
Buka browser dan akses Daloradius melalui alamat IP atau nama domain server Anda.

