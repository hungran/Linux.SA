# Phần 1. Quy trình khởi động Linux/UNIX
 Quy trình khởi động Linux/UNIX được diễn ra tính từ thời điểm bật máy "Power-On" và theo lần lượt như bảng dưới
 
 <img src="https://imgur.com/XjpWlE0.jpg">
 Mặc dù đây là quy trình tiêu chuẩn cho bất kì hệ thống Linux nào tuy nhiên cũng đã có sự thay đổi khi các hệ thống di chuyển lên các dịch vụ điện toán đám mây, container. Các quản trị viên có thể quản lý quá trình này bằng một số công cụ hình ảnh, API, bảng điều khiển thay vì chạm vào phần cứng vật lý.
 Để dễ hình dung các bước ta có bảng như sau:
 
  |Bước|   |
  | --- | --- |
  | Bước 1 | BIOS/UEFI (system firmware) |
  | Bước 2 | Kiểm tra phần cứng |
  | Bước 3 | Chọn nguồn khởi động (từ ổ đĩa, mạng,..) |
  | Bước 4 | Xác định phân vùng EFI |
  | Bước 5 | Load boot loader |
  | Bước 6 | Xác định nhân Linux |
  | Bước 7 | Load nhân |
  | Bước 8 | Khởi tạo nhân |
  | Bước 9 | Khởi chạy tiến trình số 1 |
  | Bước 10 | Thực thi các lệnh ban đầu |
  | Bước 11 | Hệ thống chạy |
  
   
 ** BIOS / UEFI (system firmware) **
 Khi một máy tính Linux được bật, việc đầu tiên CPU sẽ thực thi các dòng lệnh được chứa trong ROM (bộ nhớ chỉ đọc)
 Chương trình này được gọi là `system firmware`, `system firmware` trong hệ thống linux truyền thống được biết đến là `BIOS`.
 Với BIOS ta có thể hiểu đây là chương trình cổ điển được nạp sẵn trong bo mạch chủ của máy tính (ví dụ: NVRAM).
 Quá trình này kiểm tra các thông số cần thiết của phần cứng ngoài ra cho phép ta thay đổi thiết lập cũng như cấu hình của nó, với UEFI (Unified Extensible Firmware Interface) đây là tiêu chuẩn mới dần được thay thế cho BIOS.
 
- BIOS: 
  + Với máy tính sử dụng `system firmware` chuẩn BIOS, BIOS sẽ tìm đến MBR (Master Boot Record).
  + `MBR` chứa các thông tin cho quá trình khởi động và vị trí phân vùng khởi động (vd ổ cứng), chịu trách nhiệm cho việc tìm và nạp nhân hệ điều hành.
- UEFI:
  + Cũng giống như BIOS, UEFI là một chương trình nằm trên phần cứng của máy tính. Thay vì được lưu trong firmware giống như BIOS, chương trình này được lưu trữ ở thư mục `/efi/`
  + UEFI sử dụng bảng phân vùng GUID (Globally Unique IDentifier) để định danh phần vùng khởi động
  + Khác với BIOS, UEFI thông tin các phân vùng được lưu ở thư mục `/efi/` trên 1 phân vùng gọi là phân vùng bảo đảm.
- Có một sự so sánh như sau:
`BIOS sử dụng bản ghi MBR tương thích ở mỗi đầu ổ đĩa để định danh phân vùng boot, đối với UEFI tất cả thông tin được lưu trong bảng phần vùng, máy tính sẽ  sử dụng bản này để chạy quá trình boot tương ứng với phân vùng boot được định danh. Ngày nay, UFEI đang dần trở thành tiêu chuẩn cho các hệ thống Linux và dần thay thế cho BIOS.`

** Boot Loaders (bộ tải khởi động) **

- Với việc BIOS kiểm tra thông số cần thiết của phần cứng và xác định phân vùng khởi động thành công.
 Máy tính sẽ làm công việc tiếp theo là `Boot Loaders'
 Boot loaders cũng là một chương trình có nhiệm vụ định danh lựa chọn nhân của hệ điều hành máy tính để khởi động. Boot loader sẽ nạp nhân này và bộ nhớ và chuyển quyền điều khiển máy tính cho nhân (kernel) này.
 Có một số Boot Loader phổ biến trên Linux là GRUB hay UNIX là FreeBSD
 Trong bài viết này em xin phép chỉ được nhắc đến GRUB
 
- ** GRUB **
  + GRUB là chương tình chứa các tham số để khởi động máy tính. (ví dụ bảng menu entry)
  + Với hệ thống dùng BIOS/MBR bộ tải khởi động nằm ở khu vực đầu tiên (các block đầu tiên) trên đĩa cứng. Giai đoạn này, bộ nạp khởi động kiểm tra bảng phân vùng và tìm một phân vùng có khả năng khởi động. Khi tìm thấy một phân vùng có khả năng khởi động, GRUB sẽ tìm kiếm bộ tải khởi động giai đoạn thứ hai để nạp nhân.
  + Giai đoạn 2 nằm trong /boot . Tệp chứa cấu hình của boot gọi là `grub.cfg` sẽ lưu trong `/boot/grub` hoặc `/boot/grub2`
  + Tệp `grub.cfg` cho phép chúng ta tùy biến tại /etc/default/grub với các tham số phổ biến như bảng dưới
 
  + Sau khi thay đổi ta chạy (run) update-grub hoặc grub2-mkconfig để tệp được dịch đến tệp `grub.cfg`
 
  + GRUB cũng có các dòng lệnh cơ bản như bảng dưới cho phép ta nhập khi quá trình này diễn ra
 <img src="https://imgur.com/lA7WiAN.jpg">
 
- ** The UEFI path **
  + Khác với BIOS dùng boot loader như GRUB, hệ thống UEFI tạo phân vùng EFI và cài đặt các đoạn mã khởi động theo đường dẫn mặc định là /boot/bootx64.efi
  + Với hệ thống sử dụng phương pháp EFI / UEFI, phần mềm UEFI đọc dữ liệu trình quản lý khởi động để xác định ứng dụng UEFI nào sẽ được khởi chạy và từ nơi nào.
  + Trong trạng thái đầu tiên, UEFI boot loader tìm phần vùng và nạp chương trình gọi là `UEFI loader` từ /boot/loader.efi .  Đến đây quy trình lại tương tự như với hệ thống BIOS sử dụng bootloader là GRUB
Sau khi qua trình tải và nạp nhân thành công, máy tính sẽ chạy tiến trình đầu tiên có định danh ID là 1 và được chạy với tên gọi là `init`. `init` là một tiến trình phân cấp (runlevel) và là cha của mọi tiến trình trong hệ thống linux 
`note: không được sử dụng lệnh kill với tiến trình này`

- `init` có một số chế độ thông thường như sau:
    + Chế độ một người dùng, cho hệ thống đơn giản, không gắn kết, không có dịch vụ.
	+ Chế độ đa người sử dụng, các hệ thống được liên kết và đã được cấu hình kết hợp với hệ thống cửa sổ và giao diện đồ họa để điều khiển,
	+ Chế độ máy chủ, tương tư như chế độ đa người sử dụng nhưng không có giao diện đồ họa.
	+ Các tác dụng của `init` : đặt tên máy tính, đặt múi giờ, kiểm tra đĩa cứng với lệnh fsck, xóa tệp tạm, cấu hình mạng, và đặt biệt là chạy một tập hợp lệnh hoặc các kịch bản có sẵn.
	
- Phân cấp trong tiến trình `init` lưu tại /etc/initiab
  + Runlevel 0: Shutdown hệ thống.
  + Runlevel 1: Level chỉ  dùng cho 1 tài khoản / 1 người dùng để sửa lỗi tập tin hệ thống hoặc thay đổi (ví dụ xóa mật khẩu root khi quên mật khẩu)
  + Runlevel 2: Không sử dụng.
  + Runlevel 3: Dùng cho nhiều người nhưng chỉ giao tiếp qua dòng lệnh (không có giao diện)
  + Runlevel 4: Không sử dụng
  + Runlevel 5: Level dùng cho nhiều người dùng và được cung cấp giao diện đồ họa.
  + Runlevel 6: Level Reboot hệ thống.
	 
** Systemd ** 
- Để thay thế cho `init`, `systemd` với nhiều tính năng hơn được sử dụng phổ biết cho các hệ thống linux.
- `systemd` cũng là tiến trình đầu tiên trên hệ thống với ID = 1
- `systemd` có đầy đủ các tính năng như `init` không chỉ quản lý các tiến trình song song mà còn quản lý kết nối mạng `networkd`, kernel log `journald` và logins `logind`
- `systemd` sử dụng mục tiêu thay vì runlevel như `init`. Có 2 mục tiêu chính là `multi-user.target` và `graphical.target`.
bảng dưới 
- `systemctl` là lệnh dùng để quản lý (bắt đầu, dừng, tải lại, kiểm tra trạng thái,... của dịch vụ nói cách khác `systemctl` là ứng dụng kiểm soát các dịch vụ của hệ thống\
VD: `systemctl start mysql`

Dưới đây là bảng so sánh phân cấp và target giữa `init` và `systemd`.

<img src="https://imgur.com/zIpjznT.jpg">
