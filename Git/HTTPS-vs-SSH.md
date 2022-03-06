## HTTPS và SSH
Git sử dụng 2 giao thức phổ biến nhất là HTTPS và SSH. Cả 2 đều là giao thức đáng tin cậy và an toàn.

### SSH hoạt đông
Gủa sử có 1 máy client và 1 máy server. Khi cài đặt SSH key sinh ra 1 cặp public/private key. Server giữ public key còn client lưu private key. Khi client kết nối với server(thực hiện hành động trên git) private key phải khớp với public key. Khi kết nối được tạo, không cần sử dụng đến username và password

### HTTPS
Yêu cầu username vs password, có vẻ ít bảo mật hơn SSH vì phải dùng mật khẩu để xác thực