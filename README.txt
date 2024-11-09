Dưới đây là danh sách mô tả các bài thực hành và kết quả thu được
Dù đã tắt tường lửa và tìm hiểu một số cách khác nhưng em vẫn chưa tìm được nguyên do không thể chạy lệnh `curl`
Em xin phép dùng lệnh `minikube service <service_name> --url` để truy cập vào các trang web

# Cấp độ 1: Nginx mặc định

* Mục tiêu:
Triển khai deployment chạy Nginx mặc định lên Kubernetes và cho phép truy cập từ bên ngoài thông qua NodePort

* Các bước thực hiện:
1. Tạo file `nginx-deployment.yaml` để cấu hình deployment
2. Tạo file `nginx-service.yaml` để cấu hình service NodePort
3. Sử dụng lệnh `kubectl apply -f <tên_file>` để áp dụng cấu hình
4. Kiểm tra pods và services bằng lệnh `kubectl get pods` và `kubectl get services`
5. Thực hiện `minikube service <service_name>` để kiểm tra kết quả

* Ảnh chụp kết quả thu được:
- Kết quả deployment với 2 replicas, service Nodeport 30103, pods thu được
- Trang web mặc định của nginx sau khi thử truy cập

---

# Cấp độ 2: Pod web tĩnh

* Mục tiêu:
Triển khai một ứng dụng web tĩnh (Pixelgreen) lên Kubernetes và cho phép truy cập từ bên ngoài thông qua NodePort

* Các bước thực hiện:
1. Tải mẫu template 
2. Đóng gói template vào container image sử dụng file Dockerfile
3. Tạo file `web1-deployment.yaml` để cấu hình deployment
4. Tạo file `web1-service.yaml` để cấu hình service NodePort
5. Áp dụng cấu hình với `kubectl apply -f <tên_file>` sau đó kiểm tra pods và service
6. Thực hiện `minikube service <service_name>` để kiểm tra

* Ảnh chụp kết quả thu được:
- Kết quả deployment với 2 replicas, service NodePort 30009, pods thu được
- Trang web Pixelgreen hiển thị trên màn hình

---

# Cấp độ 3: Nginx-Proxy

* Mục tiêu:
Triển khai Nginx proxy cho nhiều ứng dụng và thiết lập cấu hình proxy với các đường dẫn khác nhau

* Các bước thực hiện:
1. Tạo file `nginx-proxy.yaml` và `nginx.conf` để cấu hình deployment, service và proxy
2. Áp dụng `kubectl create configmap <configmap_name> --from-file=nginx.conf`
3. Áp dụng cấu hình với `kubectl apply -f <tên_file>` sau đó kiểm tra pods và services
4. Thực hiện `minikube service <service_name> --url` để kiểm tra

* Ảnh chụp kết quả thu được:
- Kết quả deployments, nginx-proxy-service NodePort 30000, web1-service và web2-service dùng ClusterIP, pods thu được
- Màn hình hiển thị web1 (Pixelgreen) và web2 (Primecare)
