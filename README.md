# Email Banner — repo mẫu cho từng client

Chữ ký email của client trỏ tới 2 URL cố định. Agency chỉ thay nội dung phía sau 2 URL đó:

- `https://sig.client.com/sig/banner.png`: ảnh banner, kích thước 600×150, định dạng PNG hoặc JPG (không dùng SVG).
- `https://sig.client.com/go/banner`: link khi người nhận bấm vào banner.

## Setup client mới (1 lần)

1. Trên GitHub, bấm **Use this template**, tạo repo `sig-<client>` trong org của agency.
2. Sửa `CNAME` thành `sig.<client-domain>`. Thay `sig.client.com` bằng domain đó trong `signature-snippet.html` và `HUONG-DAN-IT.md`.
3. Vào Settings → Pages, chọn Deploy from branch `main` / root, rồi bật **Enforce HTTPS** (bật được khi DNS đã trỏ xong).
4. Gửi `HUONG-DAN-IT.md` và `signature-snippet.html` cho IT của client.

## Phương án thay thế: dùng Hostinger thay cho GitHub Pages

1. Trong hPanel, chọn **Websites → Add website**, dùng domain có sẵn `sig.<client-domain>`. Ghi lại IP server để gửi cho IT client (bản ghi A).
2. Sau khi DNS đã trỏ về, vào **Security → SSL** và cài SSL miễn phí.
3. Mở **File Manager** của website đó, upload toàn bộ repo vào `public_html/` (trừ `CNAME`, file này không cần cho Hostinger).
   - Hoặc dùng **Advanced → Git**: kết nối repo GitHub và bật auto-deploy, khi đó cứ push lên GitHub là Hostinger tự cập nhật.
4. Đổi event: upload đè ảnh vào `public_html/sig/banner.png` và sửa `go/banner/index.html` (hoặc push lên Git nếu đã bật auto-deploy). Nếu có bật CDN hoặc LiteSpeed Cache thì purge cache sau khi đổi.

## Đổi event (khoảng 5 phút)

1. Upload ảnh mới đè lên `sig/banner.png`. Giữ nguyên tên file.
2. Sửa URL ở 2 chỗ trong `go/banner/index.html`.
3. Commit. Khoảng 1–10 phút sau là thấy thay đổi (GitHub Pages cache tối đa 10 phút).

## Hạn chế

- Email cũ cũng hiện banner mới.
- Outlook desktop có thể chặn ảnh từ bên ngoài cho tới khi người nhận bấm "Download pictures".
- Gmail cache ảnh qua proxy, nên người nhận có thể thấy banner cũ thêm một thời gian.
