# Phần 2. The File System 
- Mục đích cơ bản của `filesystem` là các phương pháp cách dữ liệu được đọc và lưu trên thiết bị.
- Mỗi một thiết bị (vd: ổ cứng, usb, DVD-ROM,...) có các loại `filesystem` khác nhau
- Việc tổ chức `filesystem` sao cho thuận tiện, dễ dàng truy cập, an toàn khi cần là một nhiệm vụ cơ bản.
- Các loại `filesystem` cơ bản:
  `EXT2, EXT3, EXT4, XFS, Btrfs, JFS, NTFS...`
  
  
## 2.1 PATHNAMES (đường dẫn)
- Filesystem được sắp xếp, trình bày dưới mục gốc bắt đầu bằng kí hiệu `/`
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
## 2.4 File Types
- Có 7 loại tệp dựa trên từng chức năng nhiệm vụ: 
 + Regular file: Là loại file thông thường, có thể chứa text, thực thi chương trình. 
 + Directory: chứa các regular file. Khởi tạo bằng lệnh `mkdir` hoặc xóa bằng lệnh `rmdir`
 + hard links: chứa đường dẫn thư mục cha. Sử dụng lệnh `ln` để tạo links (vd: ln file linkfile). Lệnh `ln -l` để xem số lượng link đang có.
 +
 

 