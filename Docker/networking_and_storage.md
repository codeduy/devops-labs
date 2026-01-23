# Storage

## Bind Mount

* Ánh xạ file ở host bên ngoài vào trong container; cần lưu ý đồng bộ UID của container và host ngoài để container có thể truy cập được
file đó.

## Docker Volume

* Là phần volume được Docker tạo ra và quản lí quyền toàn bộ; chỉ là không thể được chọn thư mục lưu trữ theo ý cá nhân như **Bind Mount**.
Đánh đổi lại là hiệu năng cao hơn, an toàn hơn do đã cô lập trong Docker.

# Networking

## Cần lưu ý các quy tắc sau khi cấu hình network trong docker-compose

* Service Discovery
  * Khi cấu hình giao tiếp giữa các app - service thì gọi trực tiếp tên service thay vì địa chỉ IP cục bộ của service đó (Docker đã có sẵn
    DNS nội bộ để xử lí việc này)
* Network Drivers:
  * Có 3 network drivers phổ biến như sau:
    * Bridge: là bridge NIC để các container kết nối đến NIC đó có thể giao tiếp cục bộ với nhau và thông ra ngoài Internet qua NAT.
    * Host: Container sẽ dùng NIC của Host, tức sẽ dùng IP và port của Host trực tiếp; không NAT.
    * Overlay: là cơ chế network kết nối các container ở đa cluster/server.
* Isolation:
  * Đối với việc triển khai web lên Docker container thì cần định hình rõ kiến trúc để cô lập những thành phần không cần thiết phải kết
    nối mạng ra ngoài. Ví dụ: Frontend container thì cần map port ra Internet để phục vụ client; nhưng đối với Backend container - DB container
    thì cần cô lập - chỉ giao tiếp cục bộ để đảm bảo bảo mật.
* ports và expose
  * ports: ánh xạ port host vào port cục bộ trong container để client có thể truy cập dịch vụ nằm trong container
  * expose: mang tính khai báo cổng cục bộ phục vụ cho app - service
* Race Condition: dùng **depends_on**, **healthcheck** trong cấu hình docker-compose để đảm bảo tính trước - sau của các service khi khởi động
  để tránh các lỗi do sai thứ tự khởi động. (ví dụ: DB service cần khởi động và có thể queryDB trước khi Backend service khởi động).
