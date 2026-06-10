# Hướng dẫn triển khai app "Giờ Chuẩn Giảng Dạy" — chi phí 0 đồng

Ứng dụng trong thư mục `webapp` này là bản **PWA (Progressive Web App)** hoàn chỉnh, viết lại từ phần mềm ASP.NET của bạn với **toàn bộ công thức tính giữ nguyên**: hệ số sĩ số, quy đổi lý thuyết/thực hành, 91 hoạt động quy đổi (4 nhóm), định mức theo chức danh/trình độ, chế độ giảm 50% cho giảng viên tập sự/nghiên cứu sinh.

Đặc điểm quan trọng: app chạy **hoàn toàn trên thiết bị người dùng** (dữ liệu lưu trong trình duyệt, không gửi đi đâu), nên bạn **không cần server, không cần database, không tốn một đồng vận hành nào** dù có 10 hay 10.000 người dùng.

## Bước 1 — Chạy thử ngay trên máy

Mở file `index.html` bằng Chrome hoặc Edge là dùng được ngay (chưa cần đưa lên mạng).

Để kiểm tra logic tính toán, mở app với đường dẫn kết thúc bằng `#test` (ví dụ `index.html#test`) — app sẽ tự chạy 12 phép thử đối chiếu công thức và báo kết quả.

## Bước 2 — Đưa lên mạng miễn phí (GitHub Pages)

1. Tạo tài khoản miễn phí tại https://github.com (nếu chưa có).
2. Bấm **New repository**, đặt tên ví dụ `giochuan`, chọn **Public**, bấm Create.
3. Trong trang repo, bấm **uploading an existing file**, kéo thả 5 file trong thư mục `webapp` này vào (`index.html`, `manifest.webmanifest`, `sw.js`, `icon.svg`, `icon-maskable.svg`), bấm **Commit changes**.
4. Vào **Settings → Pages**, mục Source chọn **Deploy from a branch**, Branch chọn `main` / thư mục `/ (root)`, bấm Save.
5. Sau 1–2 phút, app của bạn có địa chỉ công khai dạng: `https://tommyduong248.github.io/giochuan/`

Gửi đường link này cho bất kỳ ai — họ mở là dùng được, miễn phí, không cần đăng ký.

Lựa chọn thay thế tương đương (cũng miễn phí, nhanh hơn ở Việt Nam): **Cloudflare Pages** (pages.cloudflare.com) — tạo project, kéo thả thư mục `webapp` là xong.

## Bước 3 — Cài lên điện thoại như app thật

- **Android (Chrome):** mở link → menu ⋮ → **Thêm vào màn hình chính** (hoặc "Cài đặt ứng dụng"). 
- **iPhone (Safari):** mở link → nút **Chia sẻ** → **Thêm vào MH chính**.

Sau khi cài, app có biểu tượng riêng, mở toàn màn hình và **hoạt động cả khi không có mạng**.

## Dữ liệu của người dùng

- Mỗi thiết bị lưu dữ liệu riêng trong trình duyệt — riêng tư tuyệt đối.
- Người dùng nên vào **Cài đặt → Sao lưu (JSON)** định kỳ; file sao lưu dùng để phục hồi hoặc chuyển sang thiết bị khác.
- Định mức giờ chuẩn, hệ số sĩ số và danh mục hoạt động đều **chỉnh sửa được** trong tab Cài đặt, để phù hợp quy chế từng trường.

## Lộ trình phát triển (khi muốn mở rộng)

| Giai đoạn | Mục tiêu | Công nghệ | Chi phí |
|---|---|---|---|
| **1 (hiện tại)** | Bản cá nhân: mỗi GV tự tính giờ của mình | PWA tĩnh + GitHub Pages | **0 đ vĩnh viễn** |
| **2** | Đồng bộ nhiều thiết bị, đăng nhập | Thêm Supabase (free tier: 50.000 người dùng đăng nhập/tháng, 500MB DB) | 0 đ tới vài nghìn người dùng |
| **3** | Bản trường học: admin quản lý GV, quy trình duyệt (NHAP → GUI_DUYET → DA_DUYET), báo cáo toàn khoa, xuất Excel | Supabase (phân quyền RLS) hoặc quay lại ASP.NET của bạn deploy lên VPS | ~0–120k đ/tháng (Supabase Pro $25/tháng chỉ khi rất đông) |

Gợi ý chiến lược: phát hành bản cá nhân miễn phí để nhiều giảng viên dùng và góp ý → khi có trường muốn dùng chính thức, bản trường học (giai đoạn 3) chính là thứ có thể thu phí theo trường, trong khi bản cá nhân vẫn miễn phí mãi mãi.

## Cập nhật app sau này

Sửa file `index.html` rồi upload đè lên GitHub — mọi người dùng tự nhận bản mới ở lần mở app kế tiếp (có mạng). Khi thay đổi lớn, đổi tên cache trong `sw.js` (`gcgd-v1` → `gcgd-v2`) để chắc chắn bản mới được tải.
