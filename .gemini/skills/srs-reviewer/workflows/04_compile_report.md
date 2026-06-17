# Workflow: Bước 4 - Tổng hợp Báo cáo Review (Compile Review Report)

Đây là bước cuối cùng. Agent sẽ tổng hợp tất cả các lỗi và phát hiện từ Bước 1, 2, 3 thành một báo cáo đánh giá hoàn chỉnh bằng Markdown để trả về cho người dùng.

## YÊU CẦU BÁO CÁO ĐẦU RA:
Báo cáo phải được cấu trúc rõ ràng gồm các phần:

1. **Tổng quan Đánh giá (Executive Summary):**
   - Tên tài liệu được review.
   - Đánh giá tổng quan (Ví dụ: Đạt yêu cầu khoảng bao nhiêu %, các điểm sáng và các rủi ro lớn nhất).
   - Bảng thống kê số lượng lỗi theo mức độ: 🔴 High (Lỗi logic/thiếu luồng/an toàn) | 🟡 Medium (Mơ hồ/NFR không đo lường được) | 🔵 Low (Định dạng/Glossary/TBD).
2. **Danh sách Phát hiện Chi tiết (Detailed Findings):**
   - Trình bày dạng bảng hoặc danh sách có cấu trúc.
   - Mỗi phát hiện phải ghi rõ:
     - **Vị trí:** Chương/Mục hoặc Dòng (nếu có).
     - **Mức độ:** High/Medium/Low.
     - **Mô tả vấn đề:** Giải thích tại sao đây là lỗi hoặc rủi ro.
     - **Đề xuất sửa đổi (Suggested Rewrite):** Câu/đoạn văn bản đề nghị thay thế.
3. **Danh sách các mục cần BA làm rõ (Questions for BA):**
   - Các điểm nghi ngờ về nghiệp vụ hoặc các từ khóa TBD chưa có lời giải đáp.
