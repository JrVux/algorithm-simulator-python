# Mô Phỏng Thuật Toán Python - Lớp 10 🧮

Công cụ mô phỏng thuật toán trực quan cho giáo viên dạy Python lớp 10, dùng trình chiếu trên lớp.

## Tính năng

- **9 thuật toán** trong 4 nhóm:
  - 🎨 Nhóm Sắp xếp: Bubble Sort, Selection Sort, Insertion Sort
  - 🔍 Nhóm Tìm kiếm: Linear Search, Binary Search
  - 🌳 Nhóm Đệ quy: Giai thừa (Factorial), Fibonacci, Tháp Hà Nội
  - ⬛ Cấu trúc dữ liệu: Stack (Push/Pop), Queue (Enqueue/Dequeue)

- Trực quan hóa:
  - Bar chart mảng số với highlight so sánh/hoán đổi/sắp xếp
  - Code Python kèm highlight dòng đang chạy
  - Bảng biến và tham số cập nhật theo thời gian
  - Stack và Queue visualization
  - Binary Search hiển thị low/mid/high

- Điều khiển:
  - Play / Pause / Step (tung bước) / Step Back (lùi bước) / Reset
  - Tốc độ điều chỉnh
  - Nhảy tới bước bất kỳ
  - Nhập mảng ngẫu nhiên hoặc tùy chỉnh

## Cách sử dụng

1. Mở `algorithm-simulator.html` bằng trình duyệt
2. Chọn thuật toán từ menu bên trái
3. Bấm **Play** để chạy animation
4. Dùng **Step** để xem từng bước chi tiết
5. Bấm **Reset** để bắt đầu lại

## Deploy

Upload file `.html` duy nhất lên GitHub Pages để sử dụng online.

## Cấu trúc

```
Dự án/
├── algorithm-simulator.html  # File duy nhất (HTML + CSS + JS)
├── master-prompt-mo-phong-thuat-toan.md  # Prompt gốc
└── README.md  # Tài liệu này
```