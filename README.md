# Bản Làng

Trò chơi dựng bản làng vùng cao qua **9 thời kỳ lịch sử Việt Nam**, chạy ngay trên trình duyệt, cài được lên điện thoại như một ứng dụng (PWA) và chơi được khi không có mạng.

**Chơi:** https://iamboo98.github.io/banlang/ (sau khi bật GitHub Pages, xem bên dưới)

## Hành trình 9 màn chơi

| Màn | Thời kỳ | Lối chơi |
|---|---|---|
| 1 | Thời nguyên thuỷ (trước khoảng 2000 TCN) | Sinh tồn, săn bắt, hái lượm, công cụ đá |
| 2 | Dựng nước Văn Lang – Âu Lạc | Xây làng, trồng lúa nước, đúc đồng, trống đồng Đông Sơn |
| 3 | Bắc thuộc (179 TCN – 938) | Bảo vệ cộng đồng, đồn luỹ, góp lương thực cho nghĩa quân |
| 4 | Phong kiến độc lập (938 – 1858) | Xây kinh đô, Hoàng thành, Văn Miếu, chợ phiên |
| 5 | Pháp thuộc (1858 – 1945) | Truyền bá chữ Quốc ngữ, ủng hộ phong trào yêu nước |
| 6 | Kháng chiến chống Pháp (1945 – 1954) | Bình dân học vụ, cột cờ, lương thực cho chiến dịch |
| 7 | Kháng chiến chống Mỹ (1954 – 1975) | Trạm y tế, trường học, chi viện tiền tuyến |
| 8 | Thống nhất (1975 – 1986) | Khôi phục kinh tế: đường, điện, đài tưởng niệm |
| 9 | Đổi mới (1986 – nay) | Nhà kiên cố, chuyển đổi số, thành phố thông minh |
| ∞ | Việt Nam phát triển hơn nữa | Các kỷ nguyên mới nối tiếp, không có điểm dừng |

Mỗi thời kỳ có mục tiêu riêng (dân số, công trình, dự án, góp lương thực). Xong hết mục tiêu là sang thời kỳ sau, kèm một đoạn sự kiện lịch sử mở đầu.

## Bật GitHub Pages

Settings → Pages → Build and deployment → Source: **Deploy from a branch** → Branch: **main**, thư mục **/ (root)** → Save. Sau 1–2 phút trò chơi có ở https://iamboo98.github.io/banlang/.

## Bật đăng nhập Google để lưu tiến trình

Trò chơi dùng Firebase (gói miễn phí Spark) cho đăng nhập Google và lưu bản chơi.

1. Vào https://console.firebase.google.com → **Add project** (có thể tắt Google Analytics).
2. **Build → Authentication → Get started → Sign-in method → Google → Enable**, chọn email hỗ trợ → Save.
3. **Authentication → Settings → Authorized domains → Add domain:** `iamboo98.github.io`
4. **Build → Firestore Database → Create database**, chọn vị trí (ví dụ `asia-southeast1`), chế độ Production. Sang tab **Rules**, dán nội dung file [`firestore.rules`](firestore.rules) → **Publish**. Luật này chỉ cho mỗi người đọc, ghi bản lưu của chính mình.
5. **Project settings → General → Your apps → biểu tượng `</>` (Web)** → đặt tên → Register app → sao chép phần `firebaseConfig`.
6. Mở file [`firebase-config.js`](firebase-config.js) (bấm bút chì để sửa), thay `window.BANLANG_FIREBASE = null;` bằng:
   ```js
   window.BANLANG_FIREBASE = {
     apiKey: "...",
     authDomain: "...",
     projectId: "...",
     storageBucket: "...",
     messagingSenderId: "...",
     appId: "..."
   };
   ```
   rồi Commit.
7. Mở lại trang, bấm **Đăng nhập Google để lưu tiến trình**. Bản đang chơi trên máy được đưa lên tài khoản; máy khác chỉ cần đăng nhập cùng tài khoản là chơi tiếp.

`apiKey` của Firebase cho web không phải mật khẩu nên để công khai được; dữ liệu được bảo vệ bằng luật Firestore ở bước 4.

## Cài lên điện thoại

- Android (Chrome): mở link → menu ⋮ → **Cài đặt ứng dụng**.
- iPhone (Safari): mở link → nút Chia sẻ → **Thêm vào MH chính**.

Muốn có file APK hoặc đưa lên Google Play: dán link vào https://www.pwabuilder.com → Package for stores → Android.

## Các file

| File | Vai trò |
|---|---|
| `index.html` | Toàn bộ trò chơi (một file) |
| `firebase-config.js` | Cấu hình Firebase để bật đăng nhập Google |
| `firestore.rules` | Luật bảo mật Firestore |
| `sw.js`, `manifest.webmanifest`, `icon-*.png` | Phần ứng dụng PWA: chơi offline, cài lên màn hình chính |
| `HUONG-DAN.txt` | Hướng dẫn dạng văn bản |
