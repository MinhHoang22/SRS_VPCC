# Workflow: Bước 1 - Kiểm tra Cấu trúc & Định dạng (Compliance Check)

Trong bước này, Agent sẽ quét cấu trúc của tài liệu SRS được cung cấp để đối chiếu với cấu trúc chuẩn IEEE 830.

## CÁC ĐẦU MỤC CẦN KIỂM TRA:
1. **Sự tồn tại của các chương mục chính:**
   - 1. Introduction (Giới thiệu, đối tượng, từ điển)
   - 2. Overall Description (Bối cảnh, chức năng cốt lõi, vai trò người dùng, ràng buộc)
   - 3. External Interface Requirements (Giao diện người dùng, phần cứng, phần mềm, giao thức)
   - 4. System Features / Functional Requirements (Đặc tả chi tiết tính năng)
   - 5. Non-functional Requirements (Hiệu năng, bảo mật, chất lượng)
   - 6. Appendices / Phụ lục (Glossary, TBD)
2. **Quy tắc đặt mã yêu cầu (Requirement ID):**
   - Đảm bảo tất cả các chức năng nhỏ được mô tả đều có ID đi kèm (VD: `REQ-CRM-01`).
   - Kiểm tra xem ID có trùng lặp hay không.
3. **Mục TBD (To Be Determined):**
   - Tìm kiếm từ khóa `TBD` hoặc `Cần xác nhận` trong tài liệu.
   - Thống kê các điểm chưa rõ ràng này và đưa vào danh sách để nhắc nhở BA cần chốt thông tin.

> **Hành động sau bước 1:** Ghi nhận danh sách các phần bị thiếu hoặc sai định dạng để chuyển tiếp sang Bước 2.
