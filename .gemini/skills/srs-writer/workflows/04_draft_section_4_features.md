# Workflow: Bước 4 - Viết sâu Phần 4 (Tính năng Hệ thống - System Features)

Đây là phần cốt lõi và dài nhất của tài liệu SRS. Hãy chia mỗi tính năng lớn (System Feature) thành các block theo chuẩn template như sau:

Cấu trúc mỗi Feature:
- **4.x [Tên Feature]** (Ví dụ: 4.1 Module Quản lý Khách hàng)
  - **4.x.1 Description and Priority:** Mô tả ngắn gọn tính năng và gán độ ưu tiên (High/Medium/Low).
  - **4.x.2 Stimulus/Response Sequences:** Mô tả luồng tương tác cơ bản (Người dùng làm gì -> Hệ thống phản hồi ra sao). *Khuyến khích sinh mã Mermaid diagram để vẽ biểu đồ luồng (Flowchart) hoặc Sequence diagram tại đây.*
  - **4.x.3 Functional Requirements:** Liệt kê các yêu cầu chức năng chi tiết. Đánh mã ID rõ ràng (Ví dụ: `REQ-CRM-01`, `REQ-FEE-02`). Đảm bảo mỗi yêu cầu phải rành mạch và có thể test được.

> **Lưu ý:** Xử lý từng module một cách cẩn thận. Thay thế các placeholder `<...>` bằng nội dung thực tế.
