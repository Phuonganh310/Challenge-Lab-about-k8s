# Sử dụng Nginx làm base image
FROM nginx:latest

# Xóa các file mặc định của Nginx
RUN rm -rf /usr/share/nginx/html/*

# Copy tất cả các file web tĩnh vào thư mục web của Nginx
COPY . /usr/share/nginx/html

# Copy file cấu hình Nginx vào đúng vị trí
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose cổng 80 để truy cập từ bên ngoài
EXPOSE 80

# Chạy Nginx ở chế độ nền
CMD ["nginx", "-g", "daemon off;"]
