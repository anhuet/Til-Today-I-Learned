### Ví dụ về mạng máy tính
Khi nhiều thiết bị kết nối tới 1 Router A, mỗi thiết bị sẽ đc cấp 1 ** Mac Address ( Địa chỉ vật lí ) ** ngoài ra để các thiết bị này giao tiếp với nhau, thì mỗi thiết bị sẽ được cấp 1 ** IP Address ** ( Địa chỉ ảo hóa của thiết bị trong mạng máy tính).
1 thiết bị được định danh bằng Mac Address + IP Address
Mỗi ứng dung đang kết nối được định danh bằng 1 Port.
Các ứng dụng giao tiếp với nhau qua 1 giao thức : HTTP, TCP, UDP.....
### Mô hình OSI trong mạng máy tính
- Layer 7- Application: Request được gửi
- Layer 6- Presentation: Mã hóa dữ liệu được gửi (Encrypt if necessary HTTPS), nếu HTTP bỏ qua
- Layer 5- Session: Xác định thứ tự gọi tin khi gửi nhiều gói tin cùng 1 lúc
- Layer 4- Transport: Chia nhỏ gói tin thành các Segment, thêm ở mỗi segment 2 thông tin: cổng gửi đi và cổng nhận, ví dụ ứng dụng gửi dữ liệu từ port 123 sang port 80
- Layer 3- Network:  Lấy các segment và thêm các thông tin như IP gửi đi và IP nhận.
IP nhận lấy ở đâu? Dịch vụ DNS
- Layer2- Datalink: Thêm vào các segment các thông tin Mac Address gửi đi và nhận
Mac Address nhận lấy ở đâu? Dịch vụ ARP
- Layer1- Physical: Chuyển các segment thành các dãy nhị phân và truyền đi và tiếp tục thực hiện lại mô hình nhận theo chiều ngược lại