# Workflow: Bước 2 - Kiểm tra Ngôn ngữ & Tính Mơ hồ (Linguistic Ambiguity Check)

Trong bước này, Agent phân tích nội dung văn bản đặc tả để phát hiện các câu từ mơ hồ có thể gây hiểu lầm cho Đội ngũ Phát triển (Developers) hoặc Đội ngũ Kiểm thử (Testers).

## CÁC ĐẦU MỤC CẦN KIỂM TRA:
1. **Tìm kiếm các từ mơ hồ:**
   - Quét qua tài liệu để xác định các từ nằm trong danh sách mơ hồ tại file `context/review_rules.md`.
2. **Kiểm tra chủ thể hành động (Missing Actor):**
   - Phát hiện các câu mô tả ở dạng bị động hoặc không rõ ai thực hiện. 
   - *Ví dụ lỗi:* "Hồ sơ sẽ được lưu và gửi đi" -> Cần làm rõ: Hệ thống lưu và tự động gửi đi, hay người dùng phải click gửi?
3. **Lưu vết và Đề xuất viết lại:**
   - Với mỗi điểm mơ hồ phát hiện được, ghi lại số dòng hoặc tên mục tương ứng.
   - Viết sẵn phương án gợi ý sửa đổi rõ ràng, có số liệu cụ thể.

> **Hành động sau bước 2:** Lưu lại các lỗi câu chữ và đề xuất viết lại, sau đó chuyển sang Bước 3.
