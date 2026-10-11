# Bài 3: Viết Dockerfile 3 dòng đóng gói trang Web HTML tĩnh

## 1. Mục tiêu
Viết tệp `Dockerfile` siêu ngắn gọn để tự đóng gói một trang HTML tĩnh thành Docker Image và triển khai trên máy chủ Nginx.

---

## 2. Cấu trúc thư mục
```text
homework/session_09/ex3/
├── Dockerfile
├── index.html
└── README.md
```

---

## 3. Nội dung các tệp tin

### 3.1. `index.html`
Nội dung trang web tĩnh:
```html
<h1>Hello Docker Session 09!</h1>
```

### 3.2. `Dockerfile`
Được tối ưu với 2 câu lệnh chính:
```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

#### Giải thích chi tiết:
- **`FROM nginx:alpine`**: Sử dụng base image là Nginx chạy trên nền tảng Alpine Linux siêu nhẹ (~40MB), tối ưu hóa dung lượng image và giảm bề mặt tấn công bảo mật.
- **`COPY index.html /usr/share/nginx/html/index.html`**: Đưa tệp `index.html` từ máy host vào đúng thư mục document root mặc định phục vụ web tĩnh của Nginx.

---

## 4. Hướng dẫn thực thi và kiểm tra

### Bước 1: Build Docker Image
Chạy lệnh sau tại thư mục chứa Dockerfile:
```bash
docker build -t my-html-app:v1 .
```

### Bước 2: Khởi chạy Container
Chạy container ở chế độ nền (detached) trên cổng `8081`:
```bash
docker run -d -p 8081:80 --name html-app my-html-app:v1
```

### Bước 3: Kiểm tra kết quả
Sử dụng `curl` hoặc truy cập trực tiếp qua trình duyệt web:
```bash
curl http://localhost:8081
```

**Kết quả mong đợi:**
```html
<h1>Hello Docker Session 09!</h1>
```

---

## 5. Dọn dẹp tài nguyên
Khi hoàn tất kiểm tra, dừng và xóa container bằng lệnh:
```bash
docker stop html-app
docker rm html-app
```
Xóa image nếu không còn sử dụng:
```bash
docker rmi my-html-app:v1
```
