# Tìm hiểu về virtual file system
- Bài tìm hiểu về [Filesystem]()

- Virual file system là một hệ thống nằm phía trên file system, cho phép người dùng truy cập vào các loại hệ thống filesystem khác nhau. Nghĩa là bạn không thể tìm thấy bất kỳ filesystem nào trong `/etc/fstab`. Tuy nhiên, bạn vẫn sẽ tìm thấy chúng nếu gõ lệnh `mount`.
## Hệ thống file /Proc

- Là 1 hệ thống virtual filesystem được gắn vào thư mục `/Proc`. Không có filesystem nào thực sự tồn tại trong `/Proc`, đó là một lớp ảo để xử lý các chức năng của kernel.
Vd: Kiểm tra CPU:

&& `$ cat /Proc/cpuinfo`

- Lưu ý: Nếu kiểm tra kích thước của file bên trong `/Proc`, tất cả các file đều có kích thước bằng 0, do không tồn tại trong đĩa cứng.
- Khi gõ lệnh `cat /Proc/cpuinfo khi đó, một file sẽ được tạo tự động để hiện thị thông tin CPU.
- Tệp duy nhất có kích thước trong thư mục `/Proc` là file `/Proc/kcore`, dùng để hiển thị nội dung của RAM. Thực tế file này không chiếm không gian trong đĩa nhớ.

## Viết Proc Filesystem
Vd: file `/proc/sys/net/ipv4/ip_forward`  điểu khiển việc forward IP trong mạng.
- Có thể thay đổi giá trị của file này như sau:

&& `$ echo "1" > /Proc/sys/net/ipv4/ip_forward`

## Thay đổi /proc 
- Mọi sự thay đổi `/proc/sys/net/ipv4/ip_forward` đều không thể tồn tại sau khi reboot nếu ta không viết nó thành file vì đây là filesystem ảo, nó chỉ chiếm trên bộ nhớ 
- Có 2 cách để lưu thay đổi trong `/proc`:
	- Viết thông tin vào /etc/rc.local , đối với Red Hat hoặc các ản distro Centos thì viết trong `/etc/rc.d/rc.local` với quyền có  thể chạy, sử dụng systemd service để bật file rc.local.
	- Để thay đổi /proc/sys ta làmnhư sau:
	`$ sysctl net.ipv4.ip_forward`
	- Lệnh trên sẽ hiển thị giá trị hiện tại
	- Sử dụng lệnh dưới với `-w` để thay đổi entry
	`$ sysctl -w net.ipv4.ip_forward=1`
	- Sau đó lưu vào sysctl.conf:
	`$echo "net.ipv4.ip_forward = 1" >> /etc/sysctl.conf`
## Các file en try phổ biến trong /proc
| Name | Description |
| `/proc/cpuinfo` | Thông tin của CPU|
| `/proc/meminfo | thông tin usage của memory|
| `