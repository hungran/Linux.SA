# Inode Là Gì
Theo wiki
https://en.wikipedia.org/wiki/Inode
- Inode là kiến trúc dữ liệu của File System
- Hiểu đơn giản Inode chứa thông tin mô tả các tệp và  tài liệu
- Nếu hiểu một thư mục chỉ đơn giản là một file đặc biệt với quyền đặc biệt, các file này được lưu trữ trên ổ đĩa ở 2 phần khác nhau là: "data blocks và inodes"
- Trong đó:
	- Data block chứa nội dung của file.
	- Inode chứa các thông tin của file và được lưu trữ ở vị trí khác với data blocks
	
- Inode chứa cụ thể các thông tin sau:
`	1 Mode/permission (protection)
	2 Owner ID
	3 Group ID
	4 Size of file
	5 Number of hard links to the file
	6 Time last accessed
	7 Time last modified
	8 Time inode last modified 
`	
- Nếu hiểu các thư mục hay file là một bảng chứa các thông tin, thì 2 thông tin đầu tiên trong bảng luôn luôn là "." và ".." . Dấu "." đầu tiên là là thư mục hiện tại, ".." là thư mục cha.
- Bảng chứa thông tin của thư mục cũng chứa thông tin "name" và số inode. 
- Số inode luôn luôn là duy nhất trên từng phân vùng. 
- Khi tao tạo hard link sẽ có 2 hoặc nhiều hơn "name" với cùng 1 file và cùng 1 số inode. Khi đổi tên hoặc di chuyển file có nghĩa ta đã tạo 1 entry bao gồm thông tin 'name" và số inode, tương tự như việc tạo một file mới, nó sẽ xóa entry cũ của bảng trong thư mục cũ.
- Do vậy khi di chuyển 1 file lớn sẽ mất thời gian vì ta sẽ tạo mới và đồng thời xóa entry "name" và số inode trong bảng phía trong thư mục.
- Ngược lại khi di chuyển hay đổi tên thư mục lại nhanh hơn mặc dù thư mục chứa rất nhiều nội dung.

