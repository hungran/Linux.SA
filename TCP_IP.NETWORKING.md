# TCP/IP NETWORKING
Internet: Là một hệ thống toàn cấu có nhiệm vụ kết nối các hệ thống máy tính lại với nhau theo các tiêu chuẩn chung.

- Một số khái niệm cơ bản về TCP/IP và các giao thức mạng cơ bản
	- TCP/IP (Transmission Control Protocol/Internet Protocol) - là hệ thống mạng tạo nên internet toàn cầu.
	- TCP/IP không phụ thuộc vào phần cứng, hệ điều hành, các thiết bị có thể trao đổi thông tin qua giao thức này
- Một số tổ chức Internet: ICANN: QUản lý IP address, domain ISOC, GF

- Các tiêu chuẩn mạng
	- RFC1149, RFC1925, RFC3251, RFC4041...
	
## Networking Basics
- IP: Internet Protocal, là tiêu chuẩn để truyền dữ liệu dạng parcket từ 1 may tính sang các máy tính khác
- ICMP: Internet Control Protocol, định nghĩa một số khái niệm hỗ trợ mô tả IP bao gồm: thông báo lỗi, debugg, routing...
- ARP: Là giao thức để dịch IP address sang Hardware Address
- UDP User Datagram Protocol, giao thức truyển tài 1 chiều
- TCP: giao thức truyền tải 2 chiều, theo flow, có khả năng tự khắc phục sửa lỗi
Theo mô hình TCP/IP ta có bảng sau để phân biệt các tầng làm việc của các giao thức mạng
<img src="https://imgur.com/UtvPvbk.jpg">

## IPv4 và IPv6
[tham khảo](https://techdifferences.com/difference-between-ipv4-and-ipv6.html)
- Phiên bản IPv4 sử dụng 4-byte (32bits) trong data packet để đánh địa chỉ, chia làm 4 octa, mỗi octa có 8bits, sử dụng decimal
Do vậy ipv4 có 4294967296 (2^32) addresses
<img src="https://imgur.com/xb1JV2w.jpg">
- Datagram của IPv4
<src img="https://techdifferences.com/wp-content/uploads/2017/08/IPv4-datagram.jpg">
- Giải thích một số kí hiệu như sau:
	- Version: 4 bits, định nghĩa version number của IP
	- Header Lenght (HLEN): 
	- Service type 8 bits: Mô tả throughput, reliability adn dêlay
	- Identificatio 16bit:  
	- Flags: đánh dấu điểm giữa hoặc điểm cuối của fragment
- Phiên bản IPv6 sử dụng 16-byte, địa chỉ dưới dạng hexadecimal
<img src="https://imgur.com/IxzBgNB.jpg">

Ta có bảng so sánh như sau:

| Basis of Comparison | IPv4 | IPv6 |
| Address Configuration | Support Manual and DHCP configuration | Support Auto-configuration and renumbering |
| End-to-end connection integrity |	Unachievable | Achievable |
| Address Space |	It can generate 4.29 x 109 addresses. | It can produce quite a large number of addresses, i.e., 3.4 x 1038. |
| Security features |	Security is dependent on application | IPSEC is inbuilt in the IPv6 protocol |
| Address length | 32 bits (4 bytes) | 128 bits (16 bytes) |
| Address Representation | In decimal | In hexadecimal |
| Fragmentation performed by | Sender and forwarding routers | Only by the sender |
| Packet flow identification | Not available | Available and uses flow label field in the header |
| Checksum | Field Available | Not available |
| Message Transmission Scheme | Broadcasting | Multicasting and Anycasting |
| Encryption and Authentication | Not Provided | Provided |