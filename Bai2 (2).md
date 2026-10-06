\# Bài 2: Cấu hình phân quyền Nhóm và sudoers bằng visudo



\## 1. Tạo group và user



Tạo group:



```bash

sudo groupadd devops-admin

```



Group đã tồn tại trên hệ thống:



```text

devops-admin:x:1002:deployer

```



Kiểm tra user `deployer`:



```bash

id deployer

```



Kết quả:



```text

uid=1003(deployer) gid=1003(deployer) groups=1003(deployer),100(users),1002(devops-admin)

```



Như vậy user `deployer` đã thuộc group `devops-admin`.



\## 2. Cấu hình sudoers



Chỉnh sửa sudoers bằng:



```bash

sudo visudo

```



Dòng cấu hình đã thêm:



```text

%devops-admin ALL=(ALL) NOPASSWD: /usr/bin/systemctl start \*, /usr/bin/systemctl stop \*, /usr/bin/systemctl restart \*, /usr/bin/systemctl status \*

```



Cấu hình cho phép các thành viên của group `devops-admin` thực hiện các lệnh `systemctl start`, `stop`, `restart`, `status` mà không cần nhập mật khẩu.



\## 3. Kiểm tra bằng user deployer



Đăng nhập bằng:



```bash

su - deployer

```



Kiểm tra quyền:



```bash

sudo -l

```



Kết quả:



```text

Matching Defaults entries for deployer on 103725781523313:

&#x20;   env\_reset, mail\_badpass, secure\_path=/usr/local/sbin\\:/usr/local/bin\\:/usr/sbin\\:/usr/bin\\:/sbin\\:/bin\\:/snap/bin,

&#x20;   use\_pty



User deployer may run the following commands on 103725781523313:

&#x20;   (ALL) NOPASSWD: /usr/bin/systemctl start \*, /usr/bin/systemctl stop \*, /usr/bin/systemctl restart \*,

&#x20;       /usr/bin/systemctl status \*

```



\## 4. Kiểm tra systemctl



Thực hiện:



```bash

sudo systemctl restart cron

```



Lệnh được thực thi với quyền sudo mà không yêu cầu nhập mật khẩu.



\## 5. Kết luận



User `deployer` đã được thêm vào group `devops-admin`.



Group `devops-admin` được cấp quyền sử dụng các lệnh:



\* `systemctl start`

\* `systemctl stop`

\* `systemctl restart`

\* `systemctl status`



với `NOPASSWD` thông qua cấu hình `/etc/sudoers`.



