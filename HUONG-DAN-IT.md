# Hướng dẫn cho IT của Client

Làm 1 lần. Sau đó agency tự đổi banner, nhân viên không phải làm gì.

## Bước 1 — DNS

Tạo bản ghi CNAME trong DNS của domain công ty:

| Type  | Name | Value                                          |
|-------|------|------------------------------------------------|
| CNAME | sig  | `<agency-org>.github.io` (nếu agency dùng GitHub Pages) |
| A     | sig  | `<IP server Hostinger>` (nếu agency dùng Hostinger)     |

Agency sẽ báo cho IT nên dùng dòng nào.

## Bước 2 — Gắn banner (chọn 1 trong 2 cách)

### Cách A — Tự động cho toàn công ty (Microsoft 365, cần quyền Exchange admin)

```powershell
Connect-ExchangeOnline
New-TransportRule -Name "Email banner" `
  -FromScope InOrganization -SentToScope NotInOrganization `
  -ApplyHtmlDisclaimerLocation Append `
  -ApplyHtmlDisclaimerFallbackAction Wrap `
  -ApplyHtmlDisclaimerText '<a href="https://tn-mg.github.io/sig-test/go/banner"><img src="https://tn-mg.github.io/sig-test/sig/banner.png" width="600" height="150" alt="Sự kiện của Test"></a>'
```

- Banner chỉ gắn vào email gửi ra ngoài công ty, nằm ở cuối email.
- Người gửi không thấy banner khi soạn mail. Điều này là bình thường.

### Cách B — Mỗi nhân viên dán vào chữ ký 1 lần (không cần quyền admin)

Mở `signature-snippet.html` trong trình duyệt, bấm Ctrl+A, Ctrl+C rồi dán vào phần chữ ký:

- **Outlook (web / bản mới):** Settings → Account → Signatures.
- **Outlook classic:** File → Options → Mail → Signatures.
- **Gmail:** Settings → General → Signature.

Không chèn ảnh từ file trên máy. Ảnh phải được tải từ link `tn-mg.github.io/sig-test` thì sau này mới đổi được.
