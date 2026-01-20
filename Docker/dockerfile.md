## Bản chất
* Dockerfile là phiên bản kỹ thuật của docker dựa trên các bước cấu hình/cài đặt mã nguồn thực tế khi không dùng Docker.

## Các điểm cần lưu ý
* Layers: Có gộp lệnh (&&) để giảm số layer không? Có tận dụng Cache (copy file ít thay đổi trước) không?
Gộp lệnh trong 1 dòng RUN để tối ưu layer giảm thiểu data rác
Để tận dụng cache thì cái gì ít thay đổi nhất thì đưa lên đầu dockerFile -> vì nếu layer N thay đổi thì các
layer N+ ở phía sau cũng phải thay đổi - cài đặt lại mặc do bất cứ lí do gì

* Multi-stage: Có tách biệt môi trường Build (nặng) và Run (nhẹ) không?
Là cách viết DockerFile tối ưu hơn so với gộp lệnh (&&) trong lệnh RUN -> bởi gộp lệnh chỉ hữu tích với các file chỉ định đã biết trước; còn 1 môi trường java, nodejs,... thì không thể biết rõ các file cần gỡ để môi trường sạch hoàn toàn

* Security: Có chạy bằng USER thường không? Có lộ secret không?
Chạy bằng user thường -> cấu hình vào ngay trong dockerFile, tại vì nếu ở user root thì khi attacker chiếm đoạt được quyền kiểm soát container thì có thể thực thi được các lệnh ở vps/server chứa container đó

  * Còn đối với các file .env thì truyền biến khi run container (bằng lệnh chạy thông thường hoặc cấu hình trong docker-compose); dùng .dockerignore để ẩn file .env khi build image; (Build-time Secrets cho 1 số trường hợp cần biến nhạy cảm trong lúc build image -> build xong sẽ xóa ngay chứ k để lưu lại trong image)

  * Tuy nhiên, vẫn có rủi ro do container dùng chung kernel -> tấn công kernel (giải pháp: update OS thường xuyên)

  * Tấn công mạng cục bộ: do dùng chung mạng cục bộ với các thành phần container nhạy cảm như database container (giải pháp: dùng managed database hoặc tương tự với các tính năng bảo vệ nâng cao hơn cho nhiều kịch bản attack)

  * Lộ secret key ? (giải pháp: đổi secret key -> vô hiệu hóa secret key cũ)

* Context: Có file .dockerignore chưa?
-> để đảm bảo không build kèm các file rác của source code không cần thiết -> tiết kiệm thời gian build


* Explicit: Có dùng tag phiên bản cụ thể (không dùng latest) không?
-> việc ghi rõ phiên bản sẽ dễ dàng làm việc với các bộ phận liên quan (dev) trong trường hợp mã nguồn cần được thay đổi hay debug

