# MathPlickers – Trắc nghiệm Toán học & quét thẻ

Ứng dụng web tĩnh gồm hai màn hình:

- `index.html`: máy tính giáo viên – ngân hàng câu hỏi, trình chiếu, lớp/học sinh, thẻ, báo cáo và kết nối điện thoại.
- `mobile-scanner.html`: điện thoại – camera quét thẻ, xác nhận ổn định nhiều khung hình, lịch sử quét và điều khiển trình chiếu.

## Triển khai nhanh bằng GitHub Pages

1. Tạo repository GitHub mới.
2. Upload **cả hai file HTML** (`index.html`, `mobile-scanner.html`) và `README.md` lên thư mục gốc repository.
3. Vào **Settings → Pages**.
4. Ở **Build and deployment → Source**, chọn **GitHub Actions**.
5. Đẩy các file lên nhánh `main`; workflow `.github/workflows/pages.yml` sẽ tự triển khai. Chờ workflow hoàn tất màu xanh trong tab **Actions**.
6. Mở URL Pages trên máy tính giáo viên. Dùng QR/mã phòng hiện trên màn hình để mở trang `mobile-scanner.html` trên điện thoại.
7. Trên điện thoại, cho phép quyền camera. Camera trình duyệt yêu cầu HTTPS; GitHub Pages đáp ứng điều kiện này.

## Công thức, đồ thị và hình minh họa

- Công thức dùng KaTeX: `$...$`, `$$...$$`, `\\(...\\)`, `\\[...\\]`.
- Có macro tập hợp thường dùng: `\\R`, `\\N`, `\\Z`, `\\Q`, `\\C`.
- Đồ thị nhận biểu thức `x`, lũy thừa `^`/`**`, các hàm `sin`, `cos`, `tan`, `sqrt`, `abs`, `log`/`ln`, `exp`, `asin`, `acos`, `atan`, `floor`, `ceil`, `round`, và hằng `pi`, `e`. Ví dụ `x^3-3*x+1`, `sin(x)`, `sqrt(x)`.
- Hình học SVG được lọc các thẻ nguy hiểm và thuộc tính sự kiện trước khi hiển thị.
- Bảng số liệu/bảng biến thiên: chọn loại minh họa **Bảng**, nhập JSON dạng mảng hai chiều. Ví dụ:

```json
[
  ["x", "-∞", "0", "+∞"],
  ["f′(x)", "+", "0", "−"],
  ["f(x)", "↗", "Cực đại", "↘"]
]
```

- Ảnh minh họa: chọn **Ảnh**, nhập URL HTTPS.

## Quy ước công thức

Nên nhập công thức bằng LaTeX có dấu phân cách, ví dụ `\\frac{a}{b}`, `\\sqrt{x}`, `\\begin{cases}...\\end{cases}`. KaTeX không hỗ trợ mọi gói lệnh của MathType/LaTeX; nếu lệnh không được hỗ trợ, cần chuyển sang cú pháp KaTeX tương thích. Kiểm tra bản xem trước trước khi trình chiếu.

## Quét thẻ – lưu ý quan trọng

- Bộ quét nhận diện bộ thẻ ma trận 5×5 do chính ứng dụng tạo (dải số thẻ 1–60) và bốn hướng A/B/C/D. Đây **không phải cam kết tương thích với bộ thẻ Plickers chính thức**.
- Cần in thẻ đúng từ mục **Lớp học & In thẻ** trong ứng dụng; không tự vẽ lại, không bóp méo tỷ lệ. Khi quét, đặt thẻ trong khung, đủ sáng, tránh lóa và giữ ổn định.
- Phần mềm yêu cầu nhiều khung hình ổn định trước khi ghi nhận, có lọc độ tương phản và chống ghi nhận lặp. Đây là xử lý ảnh trên trình duyệt, không phải hệ thống thị giác máy tính đã được chứng nhận. Cần kiểm thử thực tế trên thiết bị, camera, giấy in và ánh sáng của lớp trước khi dùng để chấm điểm chính thức.
- Điện thoại cần HTTPS, quyền camera và kết nối Internet để thiết lập PeerJS. Hai thiết bị khác nhau không dùng chung `localStorage`; dữ liệu lớp/câu hỏi được lưu trong trình duyệt máy tính giáo viên.

## Dữ liệu và quyền riêng tư

Dữ liệu lớp, học sinh, câu hỏi và kết quả được lưu cục bộ trong `localStorage` của trình duyệt giáo viên. Hãy xuất/sao lưu dữ liệu định kỳ và không dùng chung máy tính không tin cậy. Kết nối điện thoại dùng PeerJS/WebRTC; cần có Internet để khởi tạo kết nối.

## Kiểm tra trước giờ dạy

- Mở trang trên Chrome/Edge máy tính và kiểm tra các tab.
- Tạo thử một câu có phân số, căn thức, hệ phương trình, một đồ thị, một bảng và một hình SVG.
- In một số thẻ thử, quét ở nhiều góc/độ sáng và xác nhận số thẻ + đáp án trên máy tính.
- Thử ngắt mạng, tải lại trang và xuất dữ liệu để bảo đảm có bản sao lưu.

## Phụ thuộc ngoài

Giao diện tải Tailwind CSS, KaTeX, PeerJS, QRCode.js, SheetJS, JSZip, Font Awesome và Google Fonts từ CDN. Khi CDN không truy cập được, một số tính năng/giao diện có thể không hoạt động đầy đủ.
