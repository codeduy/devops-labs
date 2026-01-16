# Docker Image ~ File ISO

## Bản chất
* Là 1 file nén (tarball - ví dụ: image.tar.gz -> được gom nhóm và nén lại thành 1 file duy nhất mà vẫn đảm bảo cấu trúc file và quyền); 
chứa toàn bộ thư mục gốc (bao gồm /bin, /etc,... và các thư việc cần thiết để chạy ứng dụng - service).

## Đặc điểm
* Chỉ ở trạng thái **tĩnh** (**Static**) và **chỉ đọc** (**Read-only**). Vì thế, không thể sửa đổi các thành phần trong image đã build
mà chỉ có thể build lại image mới.

## System View
* Image được cấu tạo bởi nhiều lớp (Layers) xếp chồng lên nhau dựa trên cơ chế **UnionFS** (**Union File System** là cơ chế trộn các layers rời rạc thành 1 khối thống nhất -> ta nhìn thấy như 1 volume/disk bình thường).

# Docker Container ~ Running process

## Bản chất
* Khi khởi chạy image thì Docker sẽ tạo ra 1 layer có thể ghi (Read - Write Layer) đè lên image tĩnh -> Đó là container.
* Container thực chất chỉ là 1 process được Linux kernel cách ly dựa trên cơ chế Namespace (giả lập cho service container chạy như thể
nó đang nằm 1 mình 1 OS) và Cgroups (giới hạn tài nguyên RAM, CPU, Disk I/O cho process container đó).

## Đặc điểm
* Có trạng thái **động** (**Dynamic**); có thể ghi file, log, cài thêm package vào nhưng khi xóa container thì sẽ bị mất hết dữ liệu trừ
khi có cấu hình volume.

# Docker Registry ~ Yum/Apt Repository

## Bản chất
* Là nơi lưu trữ tập trung các Image.

## Ví dụ
* **Docker Hub**: public registry tương tự kho apt mặc định của ubuntu.
* **Private Registry (Harbor, AWS ECR)**: là registry - kho nội bộ dùng riêng cho 1 tổ chức nhất định.


