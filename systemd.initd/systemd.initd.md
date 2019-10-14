# init process
- Init process là một tiến trình được khởi động lên đầu tiên trong hệ thống Linux.
- Sau khi chọn OS trong menu của bootloader.
- Nhiệm vụ của init là start và stop các process, service cần thiết.

- Vì initi là tiến trình đầu tiên của hệ thoosnh:
	- init process có PID  là 1.
	- init là tiến trình cha của tất cả các tiến trình khác

- Các kiể triển khai init system:
	- System V (system Five)
	- Upstart
	- Systemd: Là 1 init system được phát triển năm 2010.
	
# systemd

- Đang dần thay thế các init system cũ
- Ngoài start stop service or process có thể mount file system, quản lý network socket (kết nối nạng)

- Các đơn vị của systemd:
	- serive unit (.serivce): start và stop service.
	- Mount units (. Mount): quản lý mount point
	- Target units (.target) – Để điều khiển các “runlevels” (khái niệm runlevels chỉ sử dụng trong SysV init).
	
## Tạo service bằng systemd
Bảng so sánh các lệnh trong SystemV và systemd
https://www.linuxtrainingacademy.com/systemd-cheat-sheet/


Ví dụ tạo service bằng shell script như sau:
Ta tạo một vòng lặp:

Lưu vào đường dẫn **/usr/bin/myservice**

<img src="https://imgur.com/lBE6Obw.jpg">

Kiểm tra

<img src="https://imgur.com/AbQ43Rm.jpg"

Tạo systemd service **hungservice.service** đường dẫn: */lib/systemd/system/hungservice.service*:

` 
[Unit]
Description=Vu Manh Hung systemd service.

[Service]
Type=simple
ExecStart=/bin/bash hungservice

[Install]
WantedBy=multi-user.target
`
Copy tới */etc/systemd/system* và cấp quyền thực thi:

`
 - sudo cp hung.service /etc/systemd/system/
 - sudo chmod 644 /etc/systemd/system/hung.service.service
`  
Khởi động / dừng service
` 
- sudo systemctl start myservice.service
- sudo systemctl stop myservice.service
`

Kiểm tra

` sudo systemctl status myservice.service `

<img src"https://imgur.com/mqrkoJQ.jpg">
