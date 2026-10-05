# Reflection: Small-File Anti-Pattern trong Streaming Ingestion

## 1. Anti-Pattern & Nguy cơ
Small-file problem là anti-pattern phổ biến khi ingest streaming (như clickstream, IoT). Việc ghi liên tục các micro-batch nhỏ sinh ra hàng chục nghìn file Parquet vài chục KB. Điều này gây suy giảm nặng hiệu năng đọc (I/O amplification), phình to transaction log và lãng phí chi phí tính toán khi scan.

## 2. Cách phòng tránh
- **Buffering:** Tăng chu kỳ flush ở writer (theo thời gian hoặc dung lượng) thay vì ghi từng giây.
- **Compaction & Z-Order:** Thiết lập job định kỳ gộp file nhỏ về 128–512 MB và Z-order theo khóa truy vấn chính (như `user_id`, `timestamp`) để tối ưu file-skipping.
- **Log Maintenance:** Định kỳ tạo checkpoint Parquet và chạy vacuum dọn dẹp file thừa.

## 3. Khai báo sử dụng AI
AI hỗ trợ rà soát yêu cầu rubric, kiểm tra đối chiếu checklist và định dạng bài nộp. Toàn bộ notebook được thực thi thực tế trên máy cá nhân.
