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

<src img="https://techdifferences.com/wp-content/uploads/2017/08/IPv4-datagram.jpg">
- Packet Format 
	- Một IPv4 datagram các thông tin để định tuyến và truyền thông tin
	- Packer Format bao gồm 2 phần là header 20 bytes và data với giá trị có thể lên đến 65,536 cùng với header.
- Trong Header chứa các trường sau:
	- Version: 4 bits, định nghĩa phiên bản của giao thức IP
	- Header Lenght (HLEN): 4 bits, mô tả chiều dài, kích  thước của header 
	- Service type 8 bits: Mô tả loại dịch vụ, throughput, reliability and delay
	- Total lenght: 16 bits  chứa thông tin về độ dài của IP datagram
	- Identificatio: 16bits, dùng để đóng gói fragementation. Mỗi datagram được chia ra và chuyển đến các mạng khác nhau với yêu cầu về kích thước frame khác nhau. Mỗi fragment được định nghĩa với số sequence number trong trường này
	- Flags: đánh dấu điểm giữa hoặc điểm cuối của fragment
	- Fragementation offset:13 bits trường này dùng để bù lại các fragment được chia không đều, trong đó fragment đầu tiên sẽ có offset bằng 0
	- Time To Live: 8 bit, là trường chứa thời gian vòng đời của datagram, tính theo đơn vị giây (s). Thực tế được sử dụng để tính số hop khi gói tin đi qua các bộ định tuyến, giảm 1 khi qua mỗi bộ định tuyến, khi TTL về 0 gói tin sẽ bị drop.
	- Protocol: 8 bits, mô tả giao thức được đóng gói cho datagram (vd: TCP, UDP, ICMP,...)
	- Header checksum: 16 bit, xác định tính toàn vẹn, đúng đắn của header. Khi packet đến 1 router, router sẽ tính toán checksum và so nó với trường checksum này của packet. Nếu giá trị checksum kiểm tra được và trường checksum trong packet không giống nhau thì router sẽ loại bỏ packet. 
	- Source address: 4 byte, xác định nguồn của datagram
	- Destination address: 4 byte, xác định đích của datagram
	- Options: thường không được sử dụng, nhiệm vụ thêm một số chức năng cho IP datagram. 
- Data
	- bản thông tin về các giao thức:
| Protocol Number |	Protocol Name | Abbreviation |
|1 | Internet Control Message Protocol | ICMP |
| 2 | Internet Group Management Protocol | IGMP |
| 6 | Transmission Control Protocol | TCP |
| 17 | User Datagram Protocol | UDP |
| 41 | IPv6 encapsulation |	ENCAP |
| 89 | Open Shortest Path First |	OSPF | 
| 132 | Stream Control Transmission Protocol | SCTP |	

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

