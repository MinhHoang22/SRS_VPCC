# Workflow: Bước 3 - Đánh giá Logic, Luồng ngoại lệ & NFR (Logic & Exception & NFR Check)

Trong bước này, Agent tập trung phân tích logic nghiệp vụ, các kịch bản lỗi hệ thống và tính khả thi của các yêu cầu phi chức năng.

## CÁC ĐẦU MỤC CẦN KIỂM TRA:
1. **Phân tích Luồng ngoại lệ (Missing Exception Flows):**
   - Đối với mỗi tính năng trong phần System Features, kiểm tra xem ngoài luồng thành công (Happy Path), BA đã viết các luồng xử lý lỗi chưa.
   - Kiểm tra các lỗi phổ biến: Lỗi kết nối API bên thứ ba, dữ liệu nhập sai định dạng, tài sản bị ngăn chặn (đối với nghiệp vụ công chứng), lỗi tài chính/thanh toán.
2. **Kiểm tra Sự nhất quán (Consistency):**
   - So sánh thông tin phần mô tả tổng quát (Section 2) với phần chi tiết (Section 4).
   - Đảm bảo các thuộc tính thực thể dữ liệu (ERD) khớp với các thông tin nhập vào ở bảng đặc tả input.
3. **Đánh giá Khả năng kiểm thử của NFR (Non-functional Requirements Testability):**
   - Kiểm tra xem các chỉ số về Hiệu năng (Performance), Bảo mật (Security), An toàn (Safety) có ở dạng đo lường được bằng con số hay không.
   - Cắm cờ cảnh báo các NFR chung chung như "Hệ thống bảo mật tối đa".

> **Hành động sau bước 3:** Lưu lại các lỗi logic, thiếu ngoại lệ và bất đồng bộ, sau đó chuyển sang Bước 4.
