# MISTRAL tìm hiểu và ứng dụng thực tế #

## 1. Mistral là gì

Theo https://docs.openstack.org/mistral/latest/overview.html
Mistral là dịch vụ cho phép tạo, quản lý, các workflow. Trong đó người sử dụng có thể định nghĩa các tác vụ và đặt nó vào các tiến trình thực thi nối hay song song tùy ngữ cản và điều kiện đặt trước.
VD: Tạo lịch tắt bật VM.

## ** Các Main use case của mistral **
### 1. Scheduling - Cron cloud
- Giống như crontab trong môi trường Linux, Mistral có đặt lịch được tác vụ trong môi trường cloud. Có thể ra lệnh chạy được shell scripts, chuỗi trong VM, gọi các hàm API trong môi trường cloud.
- Tạo & hủy virtual instants trong cloud. 
- Kết hợp được nhiều single workflow và chạy theo lịch.
- Mistral có thể thực thi các tác vụ song song (nếu các tác vụ về mặt logic có thể), tự sửa lỗi
- Quản lý, theo dõi các workflow theo trạng thái.

### 2. Cloud enviroment deployment
- Chỉ định quy trình công việc để triển khai môi trường nhiều VM và ứng dụng (quy mô lớn) 

### 3. Long-running business process
- Đây là use case dành cho doanh nghiệp hoặc người quản trị khi có nhiều tiến trình cần thực thi và muốn giảm thiểu lỗi khi gặp sự cố.
Ví dụ: Khi các tác vụ chạy đến 1 node gặp lỗi, Mistral sẽ chọn 1 node đang active để tiếp tục thực thi tiến trình từ chính xác điểm đang bị dừng.
Để thực hiện được việc này, người sử dụng phải chia nhỏ từng tiến trình và đưa nó vào các task, Mistral sẽ quản lý chúng. Sẽ xác định thời điểm bắt đầu và có trách nhiệm chuyển tác vụ sang một instance khác khi 1 ứng dụng nào đó lỗi.
### 4. Big Data analysis & reporting

### 5. Live migration
- Dựa theo sự kiện (CPU Ceilometer) để chạy tác vụ live migration


## 2. Kiến trúc của Mistral

Theo slide có 3 thành phần cơ bản:
- Workflow: mô tả các bước, quy trình 
- Task: Định nghĩa các tác vụ
- Action: Hành động

Hoạt động của mistral mô tả như sau:
1. Các API Server theo lịch sẽ đưa workflow vào hàng đợi
2. Workflow sẽ nạp vào các engine
3. engine sẽ chạy các task lần lượt hoặc song song
4. Các tác vụ trong workflow được thực thi và sinh ra kết quả hoặc các sự kiện (vd: success, error, gửi email).


## 3. Sử dụng


