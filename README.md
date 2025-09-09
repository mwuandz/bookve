# Seat Booking (Firebase Hosting + Realtime DB)

## 1) Tạo project Firebase
- Vào https://console.firebase.google.com → Add project
- Build → Realtime Database → Create Database (location gần bạn)
- Ghi lại `databaseURL` (ví dụ: https://YOUR-PROJECT-default-rtdb.asia-southeast1.firebasedatabase.app)

## 2) Cập nhật Rules (tùy chọn, đã khai báo trong `firebase.json`)
Trong Console → Realtime Database → Rules → dán nội dung của `database.rules.json` rồi Publish.
Rule này cho phép tạo ghế mới hoặc cập nhật ghế nếu cùng `userId` (không thể cướp ghế).

## 3) Điền cấu hình vào index.html
Mở `index.html`, tìm khối:
```js
const firebaseConfig = { apiKey: "...", authDomain: "...", databaseURL: "...", ... }
```
Sao chép cấu hình từ **Project Settings → General → Your apps (Web app)** và dán vào.

## 4) Cài Firebase CLI & deploy
```bash
npm i -g firebase-tools
firebase login
firebase init hosting
# Chọn: Use an existing project (hoặc tạo mới)
# Public directory: .
# Single-page app: n
# Set up automatic builds & deploys with GitHub: n (tùy)
firebase deploy
```
Sau khi deploy, bạn sẽ nhận URL dạng:
```
https://<project-id>.web.app
```
Mở URL và dùng ngay.

## Tuỳ chỉnh nhanh
- Thay sơ đồ ghế: sửa `blockedSeats` trong `index.html`.
- Nhiều phòng chiếu: đổi biến `ROOM` (ví dụ `ROOM = "room-1"`).

> Lưu ý: App dùng `localStorage` để gán một `userId` ngẫu nhiên cho mỗi trình duyệt. Nếu muốn bảo mật hơn, bật **Anonymous Auth** và lưu `auth.uid` thay cho `userId`.
