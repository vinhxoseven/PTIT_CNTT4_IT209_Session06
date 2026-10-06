\# Bài 1: Khảo sát FHS và Phân quyền File/Folder nâng cao



\## 1. Mục tiêu



Thực hành tạo cấu trúc thư mục Linux theo FHS và thiết lập quyền truy cập cho thư mục dùng chung của ứng dụng web.



\## 2. Cấu trúc thư mục



```text

/var/www/my-app/

├── public/

└── logs/

```



\## 3. Các lệnh đã thực hiện



\### Tạo thư mục



```bash

sudo mkdir -p /var/www/my-app/public

sudo mkdir -p /var/www/my-app/logs

```



\### Gán Owner và Group



```bash

sudo chown -R devops:www-data /var/www/my-app

```



\### Phân quyền public



```bash

sudo chmod 750 /var/www/my-app/public

```



\### Phân quyền logs



```bash

sudo chmod 770 /var/www/my-app/logs

```



\## 4. Kiểm tra



Lệnh:



```bash

stat -c '%A %a %U %G %n' /var/www/my-app/public

stat -c '%A %a %U %G %n' /var/www/my-app/logs

```



Kết quả thực tế:



```text

drwxr-x--- 750 devops www-data /var/www/my-app/public

drwxrwx--- 770 devops www-data /var/www/my-app/logs

```



Kiểm tra cấu trúc:



```bash

ls -la /var/www/my-app

```



\## 5. Giải thích quyền



\### public - 750



\* Owner: `rwx` — đọc, ghi và truy cập.

\* Group: `r-x` — đọc và truy cập.

\* Others: `---` — không có quyền.



\### logs - 770



\* Owner: `rwx` — toàn quyền.

\* Group: `rwx` — toàn quyền.

\* Others: `---` — không có quyền.



\## 6. Kết luận



Đã hoàn thành việc tạo `/var/www/my-app/public` và `/var/www/my-app/logs`, đồng thời thiết lập Owner là `devops`, Group là `www-data` và phân quyền đúng theo yêu cầu.



