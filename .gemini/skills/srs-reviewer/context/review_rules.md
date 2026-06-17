# Bộ Quy tắc & Tiêu chuẩn Review SRS (Review Guidelines)

Tài liệu này chứa các quy tắc, biểu mẫu và checklist được sử dụng để kiểm duyệt tài liệu SRS.

## 1. Bộ lọc từ ngữ mơ hồ cần phát hiện (Linguistic Ambiguity Filter)
Agent phải quét qua toàn bộ tài liệu và cắm cờ các từ sau:
- **Từ chỉ tốc độ/hiệu năng:** "Nhanh chóng", "tức thời", "tối ưu", "mượt mà", "ngay lập tức".
  - *Sửa đổi yêu cầu:* Chỉ rõ thời gian (vd: "phản hồi dưới 1 giây").
- **Từ chỉ giao diện/UX:** "Thân thiện", "đẹp mắt", "dễ sử dụng", "đơn giản", "trực quan".
  - *Sửa đổi yêu cầu:* Mô tả cụ thể hành vi (vd: "không quá 3 lần nhấp chuột", "tương thích chuẩn WCAG 2.1").
- **Từ chỉ số lượng/tần suất:** "Nhiều", "khoảng", "khoảng chừng", "hầu hết", "phần lớn", "v.v.", "thỉnh thoảng".
  - *Sửa đổi yêu cầu:* Nêu rõ số lượng hoặc tỷ lệ phần trăm cụ thể.
- **Từ chỉ mức độ bắt buộc:** "Nên", "có thể", "sẽ tốt hơn nếu", "tùy chọn".
  - *Sửa đổi yêu cầu:* Sử dụng các từ chỉ mức độ bắt buộc rõ ràng như "Phải (Must/Shall)", "Không được phép (Must not)".

## 2. Checklist kiểm tra logic nghiệp vụ & Ngoại lệ (Logic & Exception Checklist)
- **Kiểm soát đầu vào (Input Validation):** Mỗi form/trường dữ liệu nhập vào phải xác định rõ:
  - Loại dữ liệu (số, chữ, định dạng email/sđt).
  - Độ dài tối thiểu/tối đa.
  - Trường đó có bắt buộc hay không.
- **Lỗi tích hợp bên thứ ba:** Nếu hệ thống giao tiếp với API bên ngoài (ví dụ: API Thuế, API Ngân hàng, API Zalo), đặc tả đã làm rõ:
  - Trường hợp API bị lỗi phản hồi (5xx, 4xx).
  - Trường hợp kết nối bị ngắt quãng hoặc timeout (quá thời gian phản hồi).
  - Phương án dự phòng (offline queue, cho phép nhập tay).
- **Luồng phân quyền:** Mọi thao tác ghi dữ liệu, phê duyệt hoặc thao tác tài chính bắt buộc phải chỉ rõ vai trò người thực hiện (Actor) có quyền hạn đó.

## 3. Tiêu chí Yêu cầu Phi chức năng đo lường được (Quantifiable NFRs)
- **Hiệu năng:** Phải chỉ ra số người dùng đồng thời tối đa (Concurrent Users), thời gian phản hồi ở mức trung bình và mức đỉnh.
- **Bảo mật:** Quy định cụ thể về mã hóa dữ liệu (khi lưu trữ và truyền tải), chuẩn hóa mật khẩu, và cơ chế hết hạn phiên làm việc (session timeout).
- **Sao lưu:** Xác định tần suất sao lưu (RPO) và thời gian khôi phục (RTO).
