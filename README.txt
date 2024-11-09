Dưới đây là danh sách mô tả các bài thực hành và kết quả thu được
Dù đã tắt tường lửa và tìm hiểu một số cách khác nhưng em vẫn chưa tìm được nguyên do không thể chạy lệnh `curl`
Em xin phép dùng lệnh `minikube service` để truy cập vào các trang web

# Cấp độ 1: Nginx mặc định

* Mục tiêu:
Triển khai deployment chạy Nginx mặc định lên Kubernetes và cho phép truy cập từ bên ngoài thông qua NodePort

* Kết quả đạt được:
- Tạo một Deployment tên `nginx` với 2 replicas
- Tạo một service NodePort trỏ tới deployment Nginx
- Thực hiện kiểm tra bằng lệnh `curl` tới NodePort và xác nhận hiển thị trang mặc định của Nginx

* Các bước thực hiện:
1. Tạo file `nginx-deployment.yaml` để cấu hình deployment
2. Tạo file `nginx-service.yaml` để cấu hình service NodePort
3. Sử dụng lệnh `kubectl apply -f <tên_file>` để áp dụng cấu hình
4. Kiểm tra pods và services bằng lệnh `kubectl get pods` và `kubectl get services`
5. Thực hiện `curl <node-ip>:<node-port>` để kiểm tra kết quả

* Ảnh chụp màn hình:
- Kết quả các deployment, service, pod thu được
- Trang web mặc định của nginx sau khi thử truy cập

---

# Cấp độ 2: Pod web tĩnh

* Mục tiêu:
Triển khai một ứng dụng web tĩnh (Pixelgreen) lên Kubernetes và cho phép truy cập từ bên ngoài thông qua NodePort

* Kết quả đạt được:
- Đóng gói thành công container chứa ứng dụng web tĩnh
- Tạo một Deployment tên `web1` với 2 replicas
- Tạo một service NodePort tên `service web 1` trỏ tới deployment `web1`
- Thực hiện kiểm tra bằng lệnh `curl` tới NodePort và xác nhận hiển thị nội dung trang web tĩnh

* Các bước thực hiện:
1. Tải mẫu template 
2. Đóng gói template vào container image sử dụng file Dockerfile
3. Tạo file `web1-deployment.yaml` để cấu hình deployment
4. Tạo file `web1-service.yaml` để cấu hình service NodePort
5. Áp dụng cấu hình với `kubectl apply -f <tên_file>`
6. Thực hiện `curl <node-ip>:<node-port>` để kiểm tra

* Ảnh chụp màn hình:
- Kết quả các deployment, service, pod thu được
- Trang web pixelgreen hiển thị trên màn hình

---

# Cấp độ 3: Nginx-Proxy

* Mục tiêu:
Triển khai Nginx proxy cho nhiều ứng dụng và thiết lập cấu hình proxy với các đường dẫn khác nhau

* Kết quả đạt được:
- Tạo một Deployment `nginx-proxy` đóng vai trò proxy
- Cấu hình Nginx proxy để chuyển tiếp yêu cầu `/web1` đến `service web1` và `/web2` đến `service web2`
- Xác nhận bằng lệnh `curl` tới NodePort với các đường dẫn khác nhau và hiển thị đúng nội dung của từng web tĩnh

* Các bước thực hiện:
1. Tạo file `nginx-proxy-deployment.yaml` và `nginx-proxy-config` để cấu hình deployment và proxy
2. Áp dụng cấu hình với `kubectl apply -f <tên_file>`
3. Thực hiện `curl http://<node-ip>:<node-port>/web1` và `curl http://<node-ip>:<node-port>/web2` để kiểm tra

* Ảnh chụp màn hình:
- Kết quả các deployment, service, pod thu được
- Màn hình hiển thị web1 (Pixelgreen) và web2 (Primecare)