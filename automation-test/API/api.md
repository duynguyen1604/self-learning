
# TỔNG QUAN VỀ API VÀ API TESTING

---

## Phần I: API

### 1.1. API là gì?

** Khái niệm:**

> **API (Application Programming Interface)** – Giao diện lập trình ứng dụng là một tập hợp các quy tắc, giao thức và công cụ cho phép các phần mềm hoặc hệ thống khác nhau tương tác và giao tiếp với nhau.

** Ví dụ (mua hàng onl):**

- Bạn là **khách hàng** muốn mua một chiếc áo.
- Bạn không đến trực tiếp **kho hàng (server)** để lấy áo → bạn sử dụng **ứng dụng mua sắm (API)**.
- Ứng dụng sẽ gửi yêu cầu đến kho, kho kiểm tra hàng, đóng gói, và giao hàng cho bạn  → Bạn chỉ thấy kết quả **áo được giao đến**.
- Bạn không cần biết hệ thống ra sao .

** Vai trò API:**

- Là **trung gian** giữa Client (người dùng, ứng dụng) và Server (dữ liệu, xử lý).
- API định nghĩa rõ cách tương tác, dữ liệu gửi/nhận, và quyền truy cập.

---

### 1.2. Tại sao API quan trọng? 

| Lợi ích | Mô tả |
|--------|-------|
|  Tái sử dụng | Một chức năng được xây dựng 1 lần, dùng được nhiều nơi. VD: Đăng nhập Google. |
|  Dễ tích hợp | Dễ dàng kết nối các hệ thống khác nhau, bất kể nền tảng hay ngôn ngữ. |
|  Phát triển độc lập | Mỗi nhóm có thể làm module riêng, miễn tuân theo API. |
|  Tự động hóa | API giúp máy móc, hệ thống tự động thao tác. |
|  Bảo mật | Kiểm soát dữ liệu & quyền truy cập theo chính sách. |
|  Mô hình kinh doanh | Cung cấp API như sản phẩm: Google Maps API, Zalo API... |

---

### 1.3. Cơ chế hoạt động API - Request/Response 

**Mô hình Client-Server:**

```text
Client ----(HTTP Request)----> API Gateway/Server---(HTTP Response)----->Client

```
+ Client: Ứng dụng, trình duyệt, mobile app hoặc dịch vụ khác gửi yêu cầu đến API để lấy dữ liệu hoặc thao tác với tài nguyên.
+ API Gateway/Server: Nhận yêu cầu, xử lý (bao gồm xác thực, xử lý nghiệp vụ, truy vấn database...), và trả kết quả về cho client.
---
**Cấu trúc HTTP Request:**
- **Base URL:** Địa chỉ chính của máy chủ (gồm giao thức, tên miền/IP). `https:` 
- **Endpoint (URL):** Đường dẫn đến tài nguyên cụ thể. `/products/123`
- **Parameters:** Thêm sau dấu ? dưới dạng key=value, ngăn cách bằng &. `/products?category=phone&page=2`
- **Base URL** + **Endpoint** + **Parameters**: Xác định tài nguyên mà client muốn thao tác.

- **HTTP Method:**
  - `GET`: Lấy dữ liệu.
  - `POST`: Tạo mới.
  - `PUT`: Cập nhật toàn bộ.
  - `PATCH`: Cập nhật 1 phần.
  - `DELETE`: Xóa.

- **Headers:** Metadata của request
  - `Content-Type: application/json`Định dạng dữ liệu gửi đi.
  - `Authorization: Bearer <token>`Xác thực người dùng, đảm bảo chỉ người được phép mới thao tác.
  - `Accept: application/json`Định dạng dữ liệu client muốn nhận.

- **Body:** Dữ liệu gửi lên, thường dạng JSON:
  ```json
  {
    "name": "New Product",
    "price": 100
  }
  ```

**HTTP Response:**

- **Status Code:** Mã trạng thái kết quả request
  - 2xx (Success): `200 OK`, `201 Created`
  - 3xx (Redirection): `301 Moved Permanently`
  - 4xx (Client Error):`400 Bad Request`, `401 Unauthorized`, `404 Not Found`
  - 5xx (Server Error):`500 Internal Server Error`

- **Headers:** Thông tin metadata đi kèm response
  - `Content-Type`, `Content-Length`

- **Body:** Dữ liệu trả về, có thể là kết quả hoặc thông báo lỗi
  ```json
  {
    "id": 123,
    "name": "Product A",
    "price": 50
  }
  ```

---

### 1.4. Các loại API phổ biến

| Loại | Mô tả |
|------|-------|
| **REST** | Phổ biến nhất, dùng HTTP method, dữ liệu thường là JSON. |
| **SOAP** | Cấu trúc XML nghiêm ngặt, dùng trong các hệ thống lớn, ngân hàng, doanh nghiệp. |
| **GraphQL** | Truy vấn chính xác dữ liệu cần. Giảm dư thừa. Hiện đại, linh hoạt hơn REST. |

---

## Phần II: Authentication & Authorization

### 2.1. Sự khác biệt giữa Authentication và Authorization

| Khía cạnh | Authentication (Xác thực) | Authorization (Phân quyền) |
|----------|----------------------------|-----------------------------|
| Câu hỏi | "Bạn là ai?" | "Bạn được làm gì?" |
| Mục tiêu | Xác minh danh tính | Cấp quyền truy cập |
| Diễn ra khi | Đầu tiên | Sau khi xác thực xong |
| Ví dụ | Đăng nhập | Chỉ admin mới được xóa tài khoản |

---

### 2.2. Các cơ chế Authentication phổ biến

| Loại | Mô tả | Ưu & Nhược |
|------|------|-------------|
| **Basic Auth** | Gửi `username:password` mã hóa Base64 trong Header. | Đơn giản, nhưng không an toàn nếu không có HTTPS. |
| **API Key** | Gửi 1 chuỗi key định danh trong Header hoặc URL. | Dễ triển khai, dùng cho xác thực ứng dụng. |
| **Bearer Token (OAuth 2.0)** | Client lấy `access_token`, gửi vào Header mỗi lần gọi. | Bảo mật cao, phổ biến cho app hiện đại. |
| **Session-based (Cookie)** | Server tạo session, gửi `SessionID` về Client lưu bằng Cookie. | Dùng nhiều cho web truyền thống. |

---

### 2.3. Authorization: Phân quyền truy cập

| Mô hình | Mô tả |
|--------|-------|
| **RBAC (Role-Based)** | Gán quyền theo vai trò: admin, user, editor. |
| **ABAC (Attribute-Based)** | Dựa trên thuộc tính người dùng, hành vi, thời gian, địa điểm... |

**🔎 Kiểm thử Authorization cần:**
- User A không thấy dữ liệu User B.
- Không có quyền thì bị từ chối truy cập.
- Gán sai vai trò → kiểm tra giới hạn hành vi.

---

### 2.4. Rủi ro nếu làm sai Auth/Author

- Rò rỉ dữ liệu.
- Truy cập trái phép tài nguyên.
- OWASP API Top 10:
  - BOLA (Broken Object Level Authorization)
  - Broken Authentication
  - Broken Function Level Authorization

---

## Phần III: API Testing

### 3.1. API Testing là gì?

> Là quá trình kiểm thử API bằng cách gửi các request (GET, POST...) và kiểm tra response mà không cần thông qua giao diện UI.

---

### 3.2. Vì sao phải test API?

- Phát hiện lỗi sớm ở tầng logic.
- Tốc độ nhanh hơn UI testing.
- Dễ tự động hóa & tích hợp CI/CD.
- Ổn định hơn UI testing (ít thay đổi).
- Không phụ thuộc nền tảng.
- Bao phủ nhiều logic hơn giao diện có thể thể hiện.

---

### 3.3. Kiểm thử API gồm những gì?

| Tiêu chí | Mô tả |
|---------|------|
| Dữ liệu trả về | Có đúng định dạng, giá trị, schema không? |
| Status Code | Có phản ánh đúng kết quả request không? |
| Hiệu suất | Phản hồi có đủ nhanh không? |
| Xử lý lỗi | Có xử lý hợp lệ các input sai, server lỗi? |
| Bảo mật | Có kiểm tra Auth & Author đúng không? |
| Tính nhất quán | Gọi nhiều lần có cho kết quả giống nhau? |

---

## Phần IV: Các loại hình và quy trình kiểm thử API

### 4.1. Các loại kiểm thử API

| Loại | Mục tiêu |
|------|---------|
| **Functional Testing** | Kiểm tra đúng/sai của chức năng API (đúng data, đúng method, sai input...). |
| **Performance Testing** | Kiểm tra tốc độ phản hồi, khả năng chịu tải (stress, load test). |
| **Security Testing** | Kiểm tra xác thực, phân quyền, SQL injection, brute-force, DDoS... |
| **Reliability Testing** | API có hoạt động ổn định lâu dài không? |
| **Usability & Documentation Testing** | Kiểm thử khả năng sử dụng của API. |

---

## Checklist kiểm thử API cơ bản

- [1] Gửi request hợp lệ → Kiểm tra response đúng.
- [2] Gửi request thiếu/sai field → Xử lý lỗi đúng.
- [3] Check status code đúng mục đích.
- [4] Test với token hợp lệ, hết hạn, sai, thiếu.
- [5] Test role user không được thực hiện hành động admin.
- [6] Test performance: thời gian phản hồi < x ms.
- [7] Test nhiều request đồng thời (load test).
- [8] Kiểm tra format response JSON (schema).
- [9] Test dữ liệu biên (max, min, null...).

---
## Công cụ hỗ trợ kiểm thử API

| Công cụ | Mục đích |
|--------|----------|
| **Postman** | Giao diện thân thiện để test API thủ công, tạo collection test. |
| **Swagger UI** | Test trực tiếp trên giao diện tài liệu API. |
| **JMeter** | Performance & Load Test. |
| **RestAssured (Java)** | Tự động hóa API test. |

---
## Phần V: HTTP vs HTTPS
### 1. HTTP là gì?

- **HTTP** (HyperText Transfer Protocol) là giao thức truyền tải siêu văn bản, dùng để trao đổi dữ liệu giữa client (trình duyệt, app) và server qua mạng Internet.
- HTTP hoạt động ở tầng ứng dụng trong mô hình OSI.
- Dữ liệu được gửi dưới dạng **plaintext** (dữ liệu không được mã hóa).
- Ví dụ URL: `http://`

#### Đặc điểm HTTP:
- Dữ liệu truyền qua mạng dễ bị nghe lén (sniffing), sửa đổi hoặc giả mạo.
- Không có cơ chế bảo mật tích hợp.
- Thường dùng cho các trang web hoặc dịch vụ không quan trọng về bảo mật.

---

### 2. HTTPS là gì?

- **HTTPS** (HyperText Transfer Protocol Secure) là phiên bản bảo mật của HTTP, sử dụng **SSL/TLS** để mã hóa dữ liệu khi truyền tải.
- Dữ liệu giữa client và server được mã hóa, đảm bảo tính riêng tư và toàn vẹn.
- Ví dụ URL: `https://`

#### Đặc điểm HTTPS:
- Dữ liệu được mã hóa giúp chống nghe lén và tấn công trung gian (MITM).
- Server có chứng chỉ số (SSL Certificate) được cấp bởi CA uy tín để xác thực danh tính.
- Tăng độ tin cậy cho người dùng, thường thấy biểu tượng khóa trên trình duyệt.
- Bảo vệ thông tin nhạy cảm như mật khẩu, token, dữ liệu cá nhân.

---

### 3. So sánh HTTP và HTTPS

| Tiêu chí            | HTTP                          | HTTPS                          |
|---------------------|-------------------------------|--------------------------------|
| **Bảo mật**          | Không mã hóa, dễ bị đánh cắp dữ liệu | Mã hóa dữ liệu, bảo vệ khỏi nghe lén và giả mạo |
| **Cổng mặc định**    | 80                            | 443                            |
| **Tốc độ**           | Nhanh hơn vì không mã hóa      | Chậm hơn 1 chút do mã hóa giải mã |
| **Chứng chỉ**        | Không cần                     | Cần chứng chỉ SSL/TLS     |
| **Xác thực server**  | Không                        | Có, qua chứng chỉ số           |
| **Đáng tin cậy**     | Thấp                         | Cao, người dùng yên tâm hơn    |
| **SEO & UX**         | Không được ưu tiên             | Được ưu tiên trên Google và trình duyệt hiện đại |

---
### 4. Tại sao nên dùng HTTPS cho API?

- **Bảo vệ dữ liệu nhạy cảm:** Token, mật khẩu, thông tin khách hàng, thanh toán…
- **Ngăn chặn tấn công MITM:** Kẻ gian không thể đọc hoặc sửa dữ liệu đang truyền.
- **Xác thực server:** Đảm bảo client đang kết nối đúng máy chủ API thật, tránh giả mạo.
- **Tuân thủ chuẩn bảo mật:** Nhiều chuẩn bảo mật yêu cầu HTTPS.
- **Cải thiện độ tin cậy và uy tín:** Người dùng tin tưởng và thoải mái sử dụng dịch vụ.
---
