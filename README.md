# Session 09 - Bài 5: Khởi chạy dịch vụ đơn giản với Docker Compose

## Mục tiêu
Viết tệp `docker-compose.yml` tối giản để khởi chạy 1 dịch vụ web (Nginx)
bằng Docker Compose CLI v2, thay cho việc gõ lệnh `docker run` thủ công.

## Nội dung tệp `docker-compose.yml`
```yaml
services:
  web:
    image: nginx:alpine
    ports:
      - "8082:80"
```

## Các lệnh đã thực hiện

### 1. Khởi chạy dịch vụ ở chế độ ngầm
```bash
docker compose up -d
```

### 2. Kiểm tra trạng thái dịch vụ
```bash
docker compose ps
```
Kết quả: service `web` đang chạy, ánh xạ cổng `8082 -> 80`.

### 3. Kiểm tra bằng curl
```bash
curl http://localhost:8082
```
Kết quả: trả về trang chào mừng mặc định của Nginx ("Welcome to nginx!").

### 4. Hạ dịch vụ xuống
```bash
docker compose down
```

## Kết quả mong đợi
- `docker compose ps` hiển thị service `web` chạy trên port 8082.
- `curl http://localhost:8082` trả về trang chào mừng của Nginx.

## Nhận xét
- Chỉ với 1 lệnh `docker compose up -d` là khởi chạy được toàn bộ dịch vụ,
  thay vì phải gõ `docker run -d -p 8082:80 nginx:alpine` thủ công.
- Cấu hình được khai báo (declarative) trong 1 file duy nhất, dễ lưu vào Git
  và tái sử dụng trên mọi máy.
