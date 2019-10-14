# The File System: Ext4
- Ext 4 là một chuẩn định dạng của File System thường được sử dụng trong các hệ thống Linux ngày nay
- Sơ lược lại về File System trong Linux:
	- Chức năng chính là chứa dữ liệu.
	- Namespace
	- Phân quyền
	- API
	- Implementation
- Ext ra đời nhằm nâng cao hiệu năng, độ tin cậy và độ lớn của file system.
- Để tăng độ tin cậy, các tính năng về Metadata (vd: inode) và journal checksums (kiểm tra toàn vẹn dữ liệu) được bổ sung.
- việc phân bố dữ liệu thay vì được đặt trong các block cố định thì được phân bổ theo từng vùng, mỗi vùng được đánh dấu vị trí bắt đầu và kết thúc. 
	** Lợi ích: Cho phép tạo không giới hạn tệp con, giảm phân mảnh. **
- Có thuật toán phân bổ vị trí khi tệp mới được tạo
- Các file mới tạo không bao giờ được phân bổ ngay sau các file hiện có
	** lợi ích: Giảm phân mảnh các file hiện có và khi tạo các file mới **
	
- Các thông tin của Ext4: 

	- Ra đời năm 2006
	- Hỗ trợ dung lượng volume lên đến 1 EiB = 10^30 TB.
	- Kích thước tối đa File = 16 TiB.
	- Không giới hạn thư mục con.
	- Tăng hiệu suất làm việc với file. Vd: Xóa tập tin dung lượng lớn,
	- Kiểm tra toàn vẹn dữ liệu.
	- Tính toán thời gian chuẩn đến nano giây.( 1 nano dây băng 109 giây).
	- Giảm bớt hiện tượng phân mãnh dữ liệu
	
# Btrfs
- Realse năm 2014
- Giải quyết các vấn để về Pool, Snapshot, checksum HDD	
- Btrfs dựa trên công nghệ COPY-ON-WRITE (CoW) tích hợp các tính năng:
	- Chống phân mảnh dữ liệu, tự kiểm tra và sửa lỗi cấu trúc file system
	- Kiểm tra và khôi phục lỗi của dữ liệu bằng bản dự phòng
	- Hỗ trợ incremental, mirroring backup
	- Hỗ trợ clone folder, sub-volume trong 1 pooling
	- Vloume có dung lượng tối đá 16EiB, kích thước file tối đa 16 EiB
## Công nghệ Copy - on - write
tham khảo wiki: https://en.wikipedia.org/wiki/Copy-on-write
- Khái niệm cơ bản: công nghệ được sử dụng có tác động đến việc sao chép, nhân bản trong hệ thống máy tính.
- Hiển đơn giản, nếu hệ thống máy tính muốn nhân bản (copy or duplicate) mà không chỉnh sửa 1 file, thay vì tạo một file mới (có cấu trúc A), file mới này được copy với cấu trúc **trỏ** đến cấu trúc của file cũ. 
- Khi cần thay đổi dữ liệu trên file, máy tính sẽ copy file ra bản mới và sửa đổi trên bản mới, bản cũ được giữ lại.
Lợi ích: Tiết kiệm tài nguyên, bảo đảm tính toàn vẹn.

# So sánh Btrfs và Ext:
- Ext: Khi thay đổi dữ liệu filesystem, dữ liệu cũ bị ghi đè.
- Btrfs: Khi thay đỏi dữ liệu của filesystem, hệ thống tạo ra bản sao và ta sửa đổi trên bản sao đó và trỏ cấu trúc file đến vị trí file cũ, tạo ghi chú để xóa tập tin cũ sau 1 khoảng thời gian
- Ext hỗ trợ max 1EiB phân vùng, 16 TiB file
- Btrfs : 16 EiB volume max và 16 EiB file size max

# XFS
- Là filesystem dành cho hệ thống 64 bit, có khả năng scal mạnh, có journal, hỗ trợ xử lý song song các tác vụ I/ON-WRITE
- Hỗ trợ file size lên đế 8EiB 
- XFS cung cấp tính năng journal cho metadata, các file system được lưu vào journal trước khi được thực sự ghi vào block (từ 512 bytes đến 64KB). Journal giống như vòng lặp để trung chuyển lưu trữ cho các disk block
- Bên trong XFS được phân vùng thành các nhóm, các nhóm có nhiệm vụ phân bổ các vùng dữ liệu có kích thước bằng nhau. Do vậy để tăng dung lượng, các file hay các thư mục mở rộng các nhóm này. Mỗi nhóm có inode riêng, có không gian riêng biệt.
- XFS cho phép mở rộng và xử lý luồng song song các tiến trình đọc ghi nhưng không thể **Shirnk** (co rút phân vùng)
- Phù hợp cho việc lưu trư và stream video.
- Hiệu suất làm việc với các file dung lượng nhỏ không tốt, không phù hợp với database, email, server có nhiều log

Nguồn: https://en.wikipedia.org/wiki/XFS
