# Xác thực trong ứng dụng Web/App

## 1. Xác thực là gì?
Xác thực (Authentication) là quá trình xác minh danh tính của người dùng => **Đăng nhập == Xác thực**

Ví dụ gần gũi:
Bạn đi vào công ty -> Quẹt thẻ nhân viên / Dấu vân tay -> Cửa xác nhận thẻ nhân viên / dấu vân tay ĐÚNG -> Bạn được vào

## Nhầm lẫn phổ biến: Authentication vs Authorization
> Đây là 2 khái niệm thường bị lẫn lộn nhất.

|Khái niệm|Ý nghĩa|Ví dụ|
|-|-|-|
|Xác thực (Authentication)|Bạn là ai? Who are you :) == Login|Login với email & password|
|Phân quyền (Authorization)|Bạn được phép làm gì (tức là sau khi xác thực xong, tiếp theo sẽ có quyền gì?)|Admin có thể xóa được user|

> 🧠 Ghi nhớ:
Bạn phải xác thực trước (authentication), rồi mới được phân quyền (authorization).

## Các loại Authentication phổ biến và ví dụ thực tế

### 1. Username & Password

#### Flow:
1. Người dùng gửi email và mật khẩu lên server.
2. Server kiểm tra mật khẩu (đã hash) có đúng không.
3. Nếu đúng, server tạo phiên làm việc (session) hoặc token và gửi lại cho client.

#### Ví dụ thực tế:
- Đăng nhập vào website bằng form email và mật khẩu.

---

### 2. Session-based Authentication

#### Flow:
1. Người dùng đăng nhập thành công, server tạo một `session_id`.
2. `session_id` được lưu trên server (trong bộ nhớ hoặc database).
3. Server gửi `session_id` về client trong cookie.
4. Mỗi request sau client gửi cookie kèm `session_id`.
5. Server kiểm tra `session_id` để xác định user.

#### Ví dụ thực tế:
- Ứng dụng web dùng cookie để giữ trạng thái đăng nhập (ví dụ PHP session).

---

### 3. Token-based Authentication (Ví dụ JWT)

#### Flow:
1. Người dùng đăng nhập thành công, server tạo JWT chứa thông tin user.
2. JWT được gửi cho client (thường trong response body).
3. Client lưu JWT (ví dụ trong localStorage hoặc cookie).
4. Client gửi JWT trong header `Authorization: Bearer <token>` mỗi khi gọi API.
5. Server xác thực JWT và cho phép truy cập tài nguyên.

#### Ví dụ thực tế:
- REST API bảo vệ tài nguyên bằng JWT token.

---

### 4. OAuth / Social Login

#### Flow:
1. Người dùng chọn đăng nhập bằng Google/Facebook.
2. Ứng dụng chuyển hướng người dùng đến trang đăng nhập của bên thứ ba.
3. Sau khi xác thực thành công, bên thứ ba trả về access token hoặc authorization code.
4. Ứng dụng nhận token/code, lấy thông tin user và tạo session hoặc JWT.

#### Ví dụ thực tế:
- "Login with Google" trên các website như Medium, Spotify.

---

