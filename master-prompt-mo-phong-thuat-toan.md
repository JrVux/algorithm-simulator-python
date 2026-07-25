# MASTER PROMPT: Công cụ mô phỏng thuật toán trực quan (dùng trình chiếu trên lớp)

> Dán toàn bộ nội dung dưới đây vào Claude (claude.ai, Claude Code, hoặc bất kỳ AI coding agent nào) để yêu cầu xây dựng công cụ.

---

## 1. Bối cảnh

Tôi là giáo viên Tin học THPT (Việt Nam), dạy Python cho học sinh lớp 10. Tôi cần một **công cụ mô phỏng thuật toán trực quan** để trình chiếu trên lớp (máy chiếu/TV), do **giáo viên điều khiển** trực tiếp trong lúc giảng bài — không phải công cụ cho học sinh tự thao tác ở nhà.

Hãy xây dựng công cụ này dưới dạng **một file HTML duy nhất** (HTML/CSS/JS thuần, không cần build step, không cần server — mở trực tiếp bằng trình duyệt hoặc host trên GitHub Pages là chạy được).

## 2. Yêu cầu chức năng tổng thể

### 2.1. Trang tổng hợp nhiều thuật toán
- Có **menu chọn thuật toán** ở đầu trang, chia theo **nhóm** (dạng tab nhóm lớn + danh sách con bên trong, hoặc sidebar phân nhóm), dễ bấm bằng chuột từ xa/con trỏ trình chiếu:
  - **Nhóm Sắp xếp**: Bubble Sort, Selection Sort, Insertion Sort
  - **Nhóm Tìm kiếm**: Linear Search, Binary Search
  - **Nhóm Đệ quy**: Giai thừa (Factorial), Fibonacci, Tháp Hà Nội (Tower of Hanoi)
  - **Nhóm Cấu trúc dữ liệu**: Stack (Push/Pop), Queue (Enqueue/Dequeue)
- Thiết kế kiến trúc code sao cho **dễ thêm thuật toán mới sau này** (ví dụ đồ thị BFS/DFS) mà không phải viết lại toàn bộ — mỗi thuật toán là một module độc lập, cùng chung một interface: nhận dữ liệu đầu vào, trả về danh sách các "bước" (state + biến + dòng code đang chạy) để phát lại. Vì các nhóm thuật toán có kiểu trực quan hóa khác nhau (bar chart / cây đệ quy / ngăn xếp), interface "step" cần đủ tổng quát để mỗi loại renderer tự đọc và vẽ theo cách riêng (xem mục 2.2b–2.2d).

### 2.2. Khu vực trực quan hóa (trung tâm màn hình, to, rõ)
- Vẽ mảng dưới dạng **các cột (bar chart)**, chiều cao tỉ lệ với giá trị.
- Tại mỗi bước: highlight màu khác nhau cho các phần tử đang so sánh, đang hoán đổi, đã sắp xếp xong.
- Có animation mượt khi hoán đổi vị trí (transition, không giật cục).
- Hiển thị giá trị số ngay trên/trong mỗi cột (học sinh ngồi xa vẫn đọc được số).

### 2.2b. Trực quan hóa nhóm Tìm kiếm
- Dùng chung kiểu bar chart như sắp xếp, nhưng highlight thêm:
  - Vùng đang xét (với Binary Search: highlight rõ `low`, `mid`, `high` và loại bỏ dần nửa mảng không còn khả năng chứa kết quả — có thể làm mờ/ẩn dần phần bị loại).
  - Phần tử tìm thấy: highlight màu nổi bật kèm thông báo "Tìm thấy tại vị trí X" hoặc "Không tìm thấy" khi kết thúc.
- Cho phép giáo viên nhập **giá trị cần tìm** (ô input riêng, cạnh ô nhập mảng).

### 2.2c. Trực quan hóa nhóm Đệ quy
- Vẽ dưới dạng **cây gọi hàm (call tree)**: mỗi lần gọi đệ quy là một node mới, node cha–con nối bằng đường kẻ, thêm dần khi "step forward".
- Mỗi node hiển thị tham số đầu vào của lần gọi đó (ví dụ `fib(4)`) và giá trị trả về khi lần gọi đó hoàn tất (hiển thị sau, có thể đổi màu node khi "return").
- Với Tháp Hà Nội: cần thêm một khu vực trực quan phụ vẽ 3 cọc và các đĩa di chuyển theo từng bước, song song với cây đệ quy.
- Node đang "active" (lệnh gọi hiện tại trên call stack) cần highlight khác với node đã hoàn tất.

### 2.2d. Trực quan hóa nhóm Cấu trúc dữ liệu (Stack/Queue)
- Stack: vẽ dạng chồng khối thẳng đứng, Push thêm khối lên trên có animation trượt vào, Pop gỡ khối trên cùng có animation trượt ra.
- Queue: vẽ dạng hàng ngang, Enqueue thêm vào cuối, Dequeue lấy ra từ đầu, có animation trượt tương ứng.
- Cho giáo viên bấm nút thao tác trực tiếp (Push/Pop hoặc Enqueue/Dequeue) với giá trị nhập tùy ý — đây là nhóm duy nhất mang tính "thao tác tương tác" hơn là "phát lại một thuật toán có sẵn", nên control bar cho nhóm này thay Play/Step bằng các nút thao tác + nút Reset.

### 2.3. Khu vực code đi kèm
- Hiển thị đoạn code Python thật của thuật toán (dạng khối code, có số dòng).
- **Highlight dòng code đang thực thi** tương ứng với bước hiện tại trên hình vẽ — đây là yêu cầu quan trọng nhất để học sinh nối được code với hành vi trực quan.

### 2.4. Bảng trạng thái biến
- Hiển thị giá trị các biến điều khiển vòng lặp tại bước hiện tại (ví dụ: `i`, `j`, `temp`, số lần so sánh, số lần hoán đổi).
- Cập nhật theo thời gian thực khi chạy/step.

### 2.5. Thanh điều khiển (control bar) — ưu tiên hàng đầu vì giáo viên là người bấm
- Nút: **Play / Pause**, **Step Forward** (từng bước một), **Step Back** (lùi lại bước trước — quan trọng để giải thích lại), **Reset**.
- Thanh trượt **tốc độ chạy** (chậm — vừa — nhanh).
- Thanh trượt hoặc số hiển thị **bước hiện tại / tổng số bước** (ví dụ "Bước 5/23"), có thể kéo để nhảy tới bước bất kỳ.
- Các nút phải **to, dễ bấm, có nhãn rõ ràng** — vì thao tác trên lớp, không phải trên máy tính cá nhân.

### 2.6. Nhập dữ liệu tùy chỉnh
- Cho phép giáo viên **nhập mảng số tùy ý** (ô input, phân tách bằng dấu phẩy) hoặc bấm nút **"Random"** để sinh mảng ngẫu nhiên (chọn được số lượng phần tử, ví dụ 5–15 phần tử để còn nhìn rõ trên máy chiếu).

## 3. Yêu cầu thiết kế giao diện

- Đây là công cụ **trình chiếu trên lớp**: chữ to, độ tương phản cao, không dùng màu sắc quá nhạt hoặc chi tiết nhỏ khó nhìn từ xa.
- Không dùng giao diện mặc định/template chung chung. Hãy thiết kế một **bản sắc hình ảnh riêng, có chủ đích** — bảng màu, font chữ, bố cục nên gợi cảm giác "phòng học/bảng đen/thuật toán" theo cách hiện đại, không sáo rỗng.
- Layout gợi ý: khu vực trực quan hóa lớn nhất, chiếm phần chính giữa; code panel và bảng biến ở hai bên hoặc bên dưới; control bar cố định, luôn hiển thị (không cần cuộn trang khi đang trình chiếu).
- Có chế độ **tối/sáng** nếu dễ triển khai (không bắt buộc).
- Responsive tối thiểu ở độ phân giải máy chiếu phổ biến (1920x1080, 4:3 nếu có thể).

## 4. Yêu cầu kỹ thuật

- Một file `.html` duy nhất, nhúng CSS và JS trực tiếp (không cần npm/build).
- Không phụ thuộc thư viện ngoài trừ khi thực sự cần thiết (nếu cần, dùng CDN qua `<script src="https://cdnjs.cloudflare.com/...">`).
- Code JS tổ chức rõ ràng: mỗi thuật toán sinh ra một mảng các "step" (trạng thái mảng + biến + dòng code đang chạy tại mỗi bước), phần render chỉ việc phát lại theo step — tách biệt logic thuật toán và logic hiển thị.
- Test kỹ với mảng có phần tử trùng nhau và mảng đã sắp xếp sẵn (trường hợp biên).

## 5. Tiêu chí nghiệm thu

- [ ] Chọn được đủ 9 thuật toán trong 4 nhóm (Sắp xếp, Tìm kiếm, Đệ quy, Cấu trúc dữ liệu) từ menu, mỗi thuật toán chạy đúng logic.
- [ ] Play/Pause/Step Forward/Step Back/Reset hoạt động mượt cho nhóm Sắp xếp/Tìm kiếm/Đệ quy, không lỗi trạng thái.
- [ ] Nhóm Cấu trúc dữ liệu (Stack/Queue) thao tác Push/Pop hoặc Enqueue/Dequeue trực tiếp mượt, đúng thứ tự.
- [ ] Highlight dòng code đúng với bước đang chạy, ở tất cả các nhóm.
- [ ] Bảng biến cập nhật đúng giá trị tại mỗi bước (bao gồm `low/mid/high` cho Binary Search, tham số/giá trị trả về cho đệ quy).
- [ ] Cây đệ quy vẽ đúng quan hệ cha–con và cập nhật đúng khi lần gọi hoàn tất (return).
- [ ] Tháp Hà Nội: 3 cọc và các đĩa di chuyển đúng luật, đồng bộ với cây đệ quy.
- [ ] Nhập mảng/giá trị tùy chỉnh và random đều hoạt động, validate input hợp lệ (báo lỗi nếu nhập sai định dạng).
- [ ] Giao diện đọc rõ từ khoảng cách xa (giả lập: thu nhỏ trình duyệt xuống 50% vẫn đọc được số liệu chính).
- [ ] Code có cấu trúc để thêm thuật toán mới (ví dụ đồ thị BFS/DFS) sau này mà không phải viết lại từ đầu.

---

**Sau khi hoàn thành**, hãy tóm tắt ngắn gọn cấu trúc file và giải thích cách tôi có thể tự thêm một thuật toán mới vào menu sau này.
