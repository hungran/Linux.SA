# Phần 2. The File System 
Đối với Linux, tất cả các thiết bị được kết nối vào máy tính đều được nhận dạng như tập tin, kể cả phần cứng như ổ đĩa cứng, phân vùng của ổ đĩa cứng, USB hay DVD-ROM.
- `filesystem` là các phương pháp, cách thức dữ liệu được đọc và lưu trên thiết bị.
- Mỗi một thiết bị (vd: ổ cứng, usb, DVD-ROM,...) có các loại `filesystem` khác nhau
- Việc tổ chức `filesystem` sao cho thuận tiện, dễ dàng truy cập, an toàn khi cần là một nhiệm vụ cơ bản.
- Các loại `filesystem` cơ bản:
  `EXT2, EXT3, EXT4, XFS, Btrfs, JFS, NTFS...`
  
  
## 2.1 PATHNAMES (đường dẫn)
- Filesystem được sắp xếp theo đường dẫn, phân bậc qua dấu `/` cũng là bậc cao nhất của tệp hệ thống.
- `/` ký hiệu này tượng trưng cho thư mục root
- Đường dẫn có thể là một đường dẫn tuyệt đối bắt đầu bằng dấu `/` (vd: /tmp/foo) hoặc tương đối (vd: ./foo)
- Tối đa của một đường dẫn lên đến 4095 byte trên Linux. Nếu truy cập vượt quá độ dài này bạn phải `cd` vào một mục trung gian hoặc sử dụng một đường dẫn tương đối.

## 2.2 Filesystem mounting and unmounting
- Thông thường, các thiết bị được gán vào 1 thư mục trống bất kì và gọi đó là 1 mount point, sử dụng lệnh `mount` để thực hiện việc này.
- Dùng lệnh `man mount` để tìm hiểu hướng dẫn sử dụng cơ bản lệnh `mount`
- Sau khi được `mount` vào hệ thống, người sử dụng có thể dễ dàng truy cập vào các thiết bị với định nghĩa `filesystem` khác nhau.
- Tệp `/etc/fstab` chứa danh sách các `filesystem` đã được mount vào hệ thống. Thông tin này cho phép `filesystems` tự động kiểm tra và mount trong quá trình khởi động.
- Ngược lại khi muốn gỡ `filesystems` ra khỏi hệ thống ta sử dụng lệnh `unmount`
 - lênh `unmount -l` không cho phép filesystem được unmount mà phải đợi khi file này thực sự được đóng lại. 
 - lệnh `unmount f` cho phép unmount `filesystem` được gắn với tiến trình đang chạy.
- Tham số của lệnh mount và file /etc/fstab tương tự, có một số lưu ý như dưới:
- Thiết bị không có trong /etc/fstab chỉ root mới mount được.
## 2.3 ORGANIZATION OF THE FILE TREE (Tổ chức sắp xếp cây thư mục)
Danh sách các thư mục thông thường được nhìn thấy dưới thư mục gốc (`/`) 
root/
### 2.3.1 Root
- Mở từng tập tin và thư mục từ thư mục root
- Chỉ có user root mới có quyền chỉnh sửa dưới thư mục này
- /root là thư mục gốc của user root/
### 2.3.2 /bin - User Binaries
- Lệnh Linux sử dụng ở chế độ Singer-user mode nằm trong thư mục này.
- Tất cả user trên hệ thống nằm tại thư mục này đểu có thể sử dụng các lệnh : ls, ping, cp/...
### 2.3.3 /sbin
Giống như /bin, /sbin lệnh linux được sử dụng bởi người quản trị vd: iptables, reboot, ifconfig...
### 2.3.4 /etc
Chứa tâp tin cấu hình của hệ thống, các tập tin khởi động các dịch vụ của hệ thống or các dịch vụ khác.
### 2.3.5 /dev
Chưa tập tin nhận biết các thiết bị của hệ thống bao gồm các thiết bị đầu cuối, USB, các cổng giao tiếp v..vd
vd: /dev/tty1, /dev/usbmon0
### 2.3.6 /proc
Chứa thông tin về tiến trình hệ thống. Nó mô tả các thông tin về các tiến trình đang chạy
vd: /proc/uptime
### 2.3.7 /var
Viết tắt của variable file, lưu các các biến số thay đổi theo thời gian.
vd: /var/log, /var/email, các file tạm thời khi cần reboot /var/tmp/foo
### 2.3.8 /tmp/
Đây là thư mục chứa các tập tin tạm thời được tạo bởi user. Các tập tin này sẽ bị xóa khi hệ thống được reboot.
### 2.3.9 /usr
Đây là thư mục chứa các ứng dụng, thư viện, tài liệu và mã nguồn của các chương trình thứ cấp.
- /usr/bin chứa các tập tin của các ứng dụng chính đã được cài đặt cho user.
- /usr/sbin có chứa các tập tin ứng dụng cho người quản trị
- /usr/lib chứa thư viện của /usr/bin và /usr/sbin.
- /usr/local chứa các trương chình mà user mà bạn cài đặt từ nguồn.
### 2.3.10 /home
- Thư mục cá nhân của user
### 2.3.11 /boot
Là thư mục chứa tập tin cấu hình cho qua trình khởi động (boot loader file)
vd: initrd, grub nằm trong boot
### 2.3.12 /lib
Là các file thư viện hỗ trợ các thư mục nằm dưới /bin và /sbin
Tên file thư viện có thể là `ld* hoặc lib*.so*`
### 2.3.13 /opt
Opt là viết tắt của option chứa các ứng dụng add-on từ nhà cung cấp
### 2.3.14 /mnt Mount Directory
Liên kết các thư mục hệ thống tạm như temporary, gắn kết các `filesystem`
### 2.3.15 /media
Các mount point cho filesystem của các thiết bị ngoại vi.
vd CD-ROM...
### 2.3.16 /srv
Viết tắt của service, chứa các service của hệ thống liên quan đến dữ liệu

Để hình dung được tổ chức sắp xếp của thư mục ta có hình ảnh như sau:

<img src="https://imgur.com/7XZitwN.jpg">

## 2.4 File Types
-Phân loại các kiểu file
 + Regular file: Là loại file thông thường, có thể chứa text, thực thi chương trình. 
 + Directory: chứa các regular file. Khởi tạo bằng lệnh `mkdir` hoặc xóa bằng lệnh `rmdir`
 + Hard links: Liên kết cứng chứa đường dẫn thư mục cha. Sử dụng lệnh `ln` để tạo links (vd: ` ln **[File nguồn]**  **[File đích]**`). Lệnh `ln -l` để xem số lượng link đang có. Khi dùng lệnh `rm` để xóa file số lượng hard link giảm đi một, khi hark link giảm còn 0 thì không thể truy cập đến nội dung file được nữa.
 + Character device files: Đây là loại file được sử dụng để liên kết phần cứng với hệ điều hành. Các file này được đặt dưới `/dev` và thông thường đã được mount sẵn vào hệ thống.
 + Local domain socket: 
  + Sockets là các liên kết truyền thông 2 chiều, thông thường liên quan đến mạng máy tính.
  + Local domain socket :
 + Named pipes: Giống với local domain sockets, cho phép liên kết giữa 2 tiến trình trên cùng 1 hosts
 + Symbolic links: Liên kết mềm (tương tự như shortcut). Sử dụng lệnh `ln -s` để tạo liên kết mềm. Khác với liên kết cứng, khi xóa file ở thư mục gốc thì nội dung ở softlink sẽ lỗi.
## 2.5 File Atribute (thuộc tính của file)
Các thuộc tính của file có nhiệm vụ kiểm soát xem ai có quyền đọc, ghi và thực thi. 
Cùng tìm hiểu ví dụ dưới để hiểu rõ hơn về thuộc tính của file


 