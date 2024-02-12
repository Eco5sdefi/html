

### Cài đặt Phần Mềm

1. **Cập nhật danh sách gói phần mềm:**
   ```
   apt-get update
   ```

2. **Cài đặt python-software-properties hoặc software-properties-common nếu gặp lỗi:**
   ```
   sudo apt-get install -y python-software-properties
   ```
   hoặc
   ```
   sudo apt-get install -y software-properties-common
   ```

3. **Thêm PPA cho PHP:**
   ```
   sudo add-apt-repository -y ppa:ondrej/php
   ```

4. **Cập nhật lại danh sách gói và cài đặt các gói cần thiết:**
   ```
   apt-get update
   sudo apt-get -y --allow-unauthenticated install unzip zip nginx curl php7.2 php7.2-mysql php7.2-fpm php7.2-mbstring php7.2-xml php7.2-curl redis-server
   ```

5. **Cài đặt MySQL:**
   ```
   apt-get -y install mysql-client mysql-server
   ```

6. **Cài đặt Node.js và npm:**
   ```
   curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
   apt install nodejs
   apt install npm
   ```

7. **Cài đặt pm2 và forever:**
   ```
   npm install pm2 -g
   npm install forever -g
   npm install forever-monitor
   ```

8. **Nếu gặp lỗi khi cài đặt pm2, cài đặt NVM và Node.js phiên bản mới:**
   ```
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
   nvm install 10.0.0
   ```

9. **Cấu hình PHP:**
   ```
   echo "cgi.fix_pathinfo=0" >> /etc/php/7.2/fpm/php.ini
   service php7.2-fpm restart
   ```

### Cấu hình MySQL

1. **Dừng dịch vụ MySQL và cấu hình:**
   ```
   sudo service mysql stop
   sudo mkdir -p /var/run/mysqld
   sudo chown mysql:mysql /var/run/mysqld
   sudo /usr/sbin/mysqld --skip-grant-tables --skip-networking &
   ```

2. **Cập nhật mật khẩu cho người dùng root:**
   ```
   mysql -u root
   FLUSH PRIVILEGES;
   USE mysql;
   UPDATE user SET authentication_string=PASSWORD("1234") WHERE User='root';
   UPDATE user SET plugin="mysql_native_password" WHERE User='root';
   quit
   ```
   hoặc sử dụng `ALTER USER` nếu câu lệnh trên không hoạt động.

### Cài đặt và Cấu hình Nginx

1. **Tạo và cấu hình file cho domain:**
   ```
   nano /etc/nginx/sites-available/yourdomain.com
   ```
   - Sao chép và dán cấu hình vào file.
   - Lưu và thoát.

2. **Kích hoạt cấu hình và khởi động lại Nginx:**
   ```
   ln -s /etc/nginx/sites-available/yourdomain.com /etc/nginx/sites-enabled/
   rm /etc/nginx/sites-available/default
   sudo killall apache2
   service nginx restart
   ```

### Cài đặt Composer và PHPMyAdmin

1. **Cài đặt Composer:**
   ```
   curl -sS https://getcomposer.org/installer | php
   mv composer.phar /usr/local/bin/composer
   ```

2. **Cài đặt PHPMyAdmin và cấu hình:**
   ```
   sudo apt install php-mbstring
   sudo apt install phpmyadmin
   ```

3. **Tạo liên kết cho PHPMyAdmin trong thư mục public:**
   ```
   ln -s /usr/share/phpmyadmin /var/www/yourdomain.com/public
   ```

### Tạo Cơ Sở Dữ Liệu và Cài đặt Chứng Chỉ SSL

1. **Tạo cơ sở dữ liệu:**
   ```
   mysql -u root -p
   CREATE DATABASE anyname;
   quit
   ```

2. **Cài đặt Certbot và cấu hình SSL:**
   ```
   sudo add-apt-repository ppa:certbot/certbot
   sudo apt install python-certbot-nginx
   sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com
   ```

### Khởi Động Trò Chơi và Cài đặt Script

1. **Cài đặt script và khởi động trò chơi:**
   ```
   cd /var/www/yourdomain.com
   unzip putyournamehere.zip
   cd /var/www/yourdomain.com/server
   pm2 start app.js
   ```

Hãy chắc chắn rằng bạn đã thay thế "yourdomain.com" và các thông tin khác với thông tin thực tế của bạn trước khi thực hiện các lệnh.
