** Link tham khảo : https://help.ubuntu.com/community/LinuxFilesystemsExplained **
# Phân 2.1 So sánh giữa các loại FILESYSTEM phổ biến

Ta có bảng kích thước file như dưới:

| Tên | Kích thước |
| --- | --- |
| Kilobyte - KB | 1024 Bytes |
| Megabyte - MB | 1024 KBs |
| Gigabyte - GB | 1024 MBs |
| Terabyte - TB | 1024 GBs |
| Petabyte PB | 1024 TBs |
| Exabyte EB | 1024 PBs |
| Zettabyte - ZB | 1024 EBs |
| Yottabyte - YB | 1024 ZBs |

## 2.1.1 Journaling
- ** Link tham khảo : https://en.wikipedia.org/wiki/Journaling_file_system
- ** Link tham khảo : https://quantrimang.com/tim-hieu-khai-niem-co-ban-ve-he-thong-file-trong-linux-84900

Một filesystem được gọi là journaling file system khi nó có thể theo dõi các thay đổi chưa được "cam kết" hay chưa được chính thức ghi vào đĩa cứng. Nó giống như một dạng nhật kí của file system có khả năng tự động đưa filesystem trở lại trạng thái bình thường khi có sự cố.
Hiểu đơn giản quy trình của filesystem được lưu vào đĩa cứng như sau:
1. File ghi vào journal
2. journal ghi file vào đĩa cứng khi sẵn sàng.
3. Sau khi ghi thành công, file sẽ được xóa khởi journal -> Quá trình hoàn tất

-> Do vậy khi xảy ra lỗi, hệ thống có thể kiểm tra lại journal với các thao tác còn lại trên journal (chưa hoàn tất).
- Nhược điểm: chiếm nhiều hiệu suất hơn với hệ thống filesystem không có tính năng journaling

 
## 2.1.2 EXT2
- Không có tính năng Journaling
- Dung lượng tối đa 1 file 2TiB
- Dung lượng tối đa phân vùng 32 TiB
- Phù hợp với các thiết bị gắn ngoài (thẻ nhớ, usb...)

## 2.1.3 EXT3
- Là Ext2 có thêm tính năng Journaling
- Tương thích với Ext2
- Chuyển đổi phân vùng từ Ext2 lên Ext3 không cần format
### Ví dụ: 
Dưới đây là file system của 01 x ubuntu server aws_ec2
<img src="https://imgur.com/F5ve8DG.jpg">

- Filesystem ở đây là loại ext4.
- Bỏ qua root partition ta sẽ add thêm 1 aws_ebs cho con ec2 và được kết quả như sau:
- Đường dẫn trên aws cho ec2 dev/sdf, kiểm tra bằng lệnh `lsblk -f`
- Kết quả:

<img src="https://imgur.com/MdpBp9F.jpg">

- Ta thực hiện các bước sau để mount volume này vào ec2
- Bước 1: (option) kiểm tra xem volume này đã có data hay chưa: 
`sudo file -s /dev/xvdf`
- Bước 2: format với định dạng ext2
`sudo mkfs -t ext2 /dev/xvdf`
- Kết quả :

<img src="https://imgur.com/lbigl7Z.jpg">

<img src="https://imgur.com/qtfx3X7.jpg">

- Bước 3: Tạo volume mới trên ubuntu ec2 bằng lệnh sau:
`sudo mkdir /hungvolume`

- Bước 4: Mount volume với filesystem vừa format
`sudo mount /dev/xvdf /hungvolume`
- Kết quả:

<img src="https://imgur.com/h2hn3SS.jpg">

- Bước 5: Converting từ ext2 sang ext3 (bật tính năng Journaling)

`tune2fs -j /dev/xvdf`
- Kết quả
<img src="https://imgur.com/jEQMHIR.jpg">

&

<img src="https://imgur.com/Tbvw11i.jpg">

#### Tìm hiểu về fstab
- fstab là file được sử dụng để định nghĩa cách các phân vùng ổ đĩa, remote filesystem hay các block device được mount vào filesystem như thế nào
- Mỗi filesystem được mount như thế nào dựa vào từng dòng trong /etc/fstab. Trong qá trình boot, quá trình mount sẽ dựa trên file này, đọc lần lượt các dòng trong file này để mount các phân vùng.
- Mặc định trước khi khởi chạy các dịch vụ cần thiết để mount filesystem, filesystem sẽ được "fsck" (filesystemcheck).
- việc `mount` bản chất sẽ sử dụng cấu hình từ file `fstab`

- Từ ví dụ ở phía trên, ta tạo thêm directory `/hungvolume2019`

<img src="https://imgur.com/iJPqex9.jpg">

Bây giờ ta thêm entry vào `/etc/fstab` như lệnh dưới:	
- `/dev/xvdf       /hungvolume2019   ext3    defaults,nofail        0       0`
- kết quả sau khi reboot
<img src="https://imgur.com/ctXO1kl.jpg">

- Các thông tin trong `/etc/fstab`
	- với vị dụ trên ta xem bên trong file `/etc/fstab`
	- <img src="https://imgur.com/1M70CNQ.jpg">
	- `/dev/xvdf` hay `LABEL=cloudimg-rootfs` là partition hoặc remote partition. Với ví dụ ở đây thì `LABEL=Cloudimg-rootfs` là phân vùng root từ AWS mặc định tạo sẵn khi chạy ubuntu EC2, phân vùng `/dev/xvdf` được tạo khi ta tạo AWS_EBS (1 dạng ổ đĩa trên cloud)
	- `/` hay `/hungvolume2019` là thư mục được mount với định dạng phân vùng là `ext4` hay `ext3`.
	- default là lựa chọn mặc định cài đặt, các cài đặt này được lưu trong file `/proc/mounts`, với mỗi các chuẩn filesystem khác nhau, mặc định sẽ có các lựa chọn khác nhau (xem ví dụ sau về các option
, ngoài ra ta có các lựa chọn sau:
		- async: Tất cả I/O đến filesystem được đồng bộ hóa
		- atime: không sử dụng tính năng **noatim**, do đó inode access time được điểu khiển bởi kernel mặc định
		- noatime: Không cập nhật inode access times cho filesystem (vd: để truy cập vào news spoool nhanh hớn, tăng tốc news servers. Hoạt động ch tất cấc loại inodes
		- auto: được mount với lựa chọn **-a**
		- noauto: chỉ có thể mount khi có mọi tham số cụ thể.
		-
	
** Tham khảo https://www.linux.com/tutorials/convert-ext2-ext3-file-system/ **
** Tham khảo https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8#FILESYSTEM-INDEPENDENT_MOUNT_OPTIONS **
