# Deep Dive Use Case: Chứng thực chữ ký

## 1. Các trường hợp thực tế (Real Cases)

> [!NOTE]
> Chứng thực chữ ký là một trong những nghiệp vụ diễn ra rất thường xuyên. Đặc điểm là quy trình diễn ra nhanh, khách hàng bắt buộc ký ngay tại quầy trước mặt người tiếp nhận hồ sơ.

### Case 1: Cá nhân chứng thực giấy ủy quyền (Phổ biến nhất)
- **Bối cảnh:** Anh A đến văn phòng để chứng thực chữ ký trên "Giấy ủy quyền nhận lương hưu" cho người nhà.
- **Thực tế:** Anh A mang theo CCCD gốc và mẫu giấy ủy quyền tự viết hoặc in sẵn.
- **Yêu cầu hệ thống:** Nhập nhanh thông tin anh A, in Lời chứng chứng thực chữ ký (dành cho 1 người ký), đính kèm vào giấy ủy quyền.

### Case 2: Nhiều người cùng ký trên một văn bản
- **Bối cảnh:** Hai vợ chồng (Anh B và Chị C) cùng đến ký trên văn bản cam kết tài sản chung.
- **Thực tế:** Cần lấy thông tin CCCD của cả 2 người.
- **Yêu cầu hệ thống:** Form tiếp nhận hồ sơ phải cho phép add thêm nhiều khách hàng vào chung một văn bản. Lời chứng xuất ra phải tự động hiển thị thông tin cả 2 vợ chồng vào mục "Người yêu cầu chứng thực".

### Case 3: Doanh nghiệp chứng thực chữ ký trên đăng ký mẫu dấu
- **Bối cảnh:** Giám đốc công ty X đến chứng thực chữ ký để mở tài khoản ngân hàng.
- **Thực tế:** Người ký là Giám đốc, nhưng với tư cách pháp nhân là Công ty X. 
- **Yêu cầu hệ thống:** CRM phải lưu được thông tin khách hàng là tổ chức (Công ty X) và người đại diện pháp luật (Giám đốc). Lời chứng phải ghi rõ chức danh Giám đốc công ty X.

### Case 4: Khách gửi hồ sơ Online và chỉ đến ký/nhận giấy tờ (O2O - Online to Offline)
- **Bối cảnh:** Khách hàng (hoặc đối tác ngân hàng/môi giới) muốn làm dịch vụ nhưng không muốn chờ đợi. Họ chụp ảnh/scan bản gốc và gửi file qua kênh Zalo/Web của VPCC trước.
- **Thực tế:** Nhân viên VPCC kiểm tra file ảnh hợp lệ, soạn sẵn lời chứng, tính phí và hẹn giờ khách qua. Khách đến chỉ cần chìa bản gốc ra đối chiếu, ký tên rồi lấy kết quả đi ngay (tiết kiệm 80% thời gian).
- **Yêu cầu hệ thống:** Hệ thống có tính năng tiếp nhận "Hồ sơ Online chờ xử lý". Nhân viên check file, lên báo giá, gửi lại Zalo cho khách chốt phí. Khi khách đến, chỉ cần đọc SĐT hoặc quét mã QR là phần mềm hiển thị ngay hồ sơ đã soạn sẵn, chuyển thẳng sang bước in ấn và ký kết.

---

## 2. Hành trình khách hàng & Luồng xử lý trên phần mềm

### 2.1. Luồng xử lý trực tiếp tại quầy (Offline)
Quy trình chuẩn từ lúc khách bước vào đến khi cầm hồ sơ đi về, **có luồng chốt báo giá trước khi ký để tránh rủi ro hủy dịch vụ**:

#### Bước 1: Tiếp nhận và Khởi tạo hồ sơ
- **Khách hàng:** Đưa CCCD và yêu cầu chứng thực.
- **Hành động của Lễ tân:** Nhập số điện thoại hoặc quẹt CCCD vào hệ thống.
- **Phần mềm xử lý:** 
  - Hiển thị form tạo hồ sơ mới. 
  - Gõ số điện thoại `090xxxx` -> Hệ thống tìm thấy anh A (khách quen) -> **Auto-fill** họ tên, CCCD, ngày cấp, nơi cấp. 
  - Tự động sinh mã hồ sơ: `CTCK-20231015-001`.
  - Lễ tân chọn loại dịch vụ: **Chứng thực chữ ký** và nhập số lượng: 3 bản.

#### Bước 2: Báo giá và Xin xác nhận đồng ý
- **Hành động của Lễ tân:** Dựa trên số lượng vừa nhập, thông báo tổng phí dự kiến cho khách.
- **Phần mềm xử lý:**
  - Tự động lấy công thức từ Module Phí: `Phí chứng thực chữ ký = 10.000 VNĐ / chữ ký / bản`.
  - Phần mềm tính báo giá dự kiến: `3 bản x 10.000 = 30.000 VNĐ`.
  - Nếu khách mua thêm bìa hồ sơ VPCC, lễ tân thêm phụ phí: `Bìa hồ sơ: 5.000 VNĐ`. Tổng dự kiến: `35.000 VNĐ`.
  - **Khách đồng ý**, lễ tân bấm checkbox: `[x] Khách hàng đồng ý báo phí`. 
  - *Chỉ khi checkbox này được tích, hệ thống mới mở khóa bước tiếp theo (In lời chứng/Ký duyệt).*

#### Bước 3: Quét giấy tờ và Soạn Lời chứng
- **Khách hàng:** Đợi trong lúc nhân viên xử lý.
- **Hành động của Lễ tân:** Quét CCCD gốc và văn bản khách mang đến.
- **Phần mềm xử lý:**
  - Lưu file scan vào hồ sơ `CTCK-20231015-001`.
  - Dựa vào loại dịch vụ, hệ thống xuất mẫu **"Lời chứng chứng thực chữ ký"**. 
  - **Auto-merge data:** Tự điền Họ tên, CCCD của khách, ngày giờ hiện tại, tên Công chứng viên phụ trách vào Lời chứng để xuất ra bản Word/PDF.
  - Lễ tân in Lời chứng ra giấy kẹp vào văn bản.

#### Bước 4: Ký chứng thực
- **Khách hàng:** Ký và ghi rõ họ tên trước mặt nhân viên tiếp nhận hoặc Công chứng viên.
- **Phần mềm xử lý:** Trạng thái hồ sơ tự động chuyển sang `Chờ duyệt/Chờ đóng dấu`. Công chứng viên ký và đóng dấu giáp lai.

#### Bước 5: Thu tiền thực tế và Xuất hóa đơn
- **Hành động của Kế toán/Lễ tân:** Tiến hành thu tiền theo báo giá đã chốt ở Bước 2.
- **Phần mềm xử lý:**
  - Lễ tân bấm nút `Xác nhận thanh toán`.
  - Hệ thống đóng gói dữ liệu và gọi API sang phần mềm Hóa đơn điện tử (MISA, VNPT...) để phát hành biên lai/hóa đơn.

#### Bước 6: Hoàn tất và Trả kết quả (Tích hợp Zalo)
- **Hành động:** Trả bản gốc cho khách hàng kèm hóa đơn.
- **Phần mềm xử lý:** 
  - Trạng thái hồ sơ đổi thành `Hoàn tất`. 
  - **Kích hoạt gửi Zalo OA:** Ngay khi chuyển trạng thái Hoàn tất và có thanh toán, hệ thống gọi Zalo API.
  - **Nội dung tin nhắn nhận được qua Zalo:** *"VPCC XYZ xin cảm ơn anh A đã sử dụng dịch vụ Chứng thực chữ ký. Hồ sơ của anh đã hoàn tất. Link tra cứu hóa đơn điện tử: [Link_Hoa_Don]. Nếu cần hỗ trợ thêm, anh vui lòng nhắn tin tại đây."*

### 2.2. Luồng xử lý cho Hồ sơ đặt trước (O2O - Online to Offline)
Luồng này phục vụ khách hàng gửi tài liệu qua Zalo/Web trước để VPCC chuẩn bị, khách chỉ việc đến ký và lấy kết quả.

#### Bước 1: Tiếp nhận Online
- **Khách hàng:** Gửi ảnh chụp/scan văn bản cần chứng thực và CCCD qua Zalo, Facebook hoặc Email của VPCC.
- **Phần mềm xử lý:** Nhân viên tiếp nhận tự tải file về và upload lên phần mềm để tạo **Hồ sơ nháp (Pending)** chờ xử lý.

#### Bước 2: Thẩm định & Báo giá Online
- **Nhân viên VPCC:** Xem trước file tài liệu trên màn hình "Hồ sơ Online" để thẩm định. Nếu hợp lệ, nhập loại dịch vụ, số lượng để hệ thống tính **Báo giá**.
- **Hành động tiếp theo:** Nhân viên lấy thông tin báo giá từ hệ thống và nhắn tin lại cho khách: *"VPCC báo giá dịch vụ chứng thực là 30.000đ. Anh/chị vui lòng xác nhận đồng ý để VPCC chuẩn bị hồ sơ. Khi đến vui lòng mang theo bản gốc."*
- **Khách hàng:** Phản hồi "Đồng ý" qua khung chat.

#### Bước 3: Chuẩn bị sẵn Lời chứng
- **Phần mềm xử lý:** Nhân viên tick xác nhận "Khách đã đồng ý báo giá" trên phần mềm, trạng thái hồ sơ được cập nhật thành `Đã chốt phí - Chờ khách đến`. 
- **Nhân viên VPCC:** In sẵn Lời chứng, kẹp sẵn vào bìa chờ khách đến.

#### Bước 4: Khách hàng đến quầy (Offline)
- **Khách hàng:** Có mặt tại VPCC, cung cấp số điện thoại.
- **Lễ tân:** Gõ SĐT vào phần mềm, hệ thống lấy ngay ra bộ **Hồ sơ nháp** đã soạn.
- **Luồng tiếp theo:** Nhân viên cầm Bản gốc của khách đối chiếu với bản scan trên màn hình. Nếu khớp -> Tiến hành cho khách Ký -> Đóng dấu -> Thu tiền -> Hoàn tất. Toàn bộ quá trình đối chiếu, ký và đóng dấu chỉ mất 2-3 phút thay vì chờ đợi lâu.

---

## 3. Tổng hợp Mô tả Tính năng (Feature Breakdown)

> [!IMPORTANT]
> Dưới đây là các tính năng cụ thể mà team Dev cần phát triển để đáp ứng được luồng Use Case trên:

| Module | Tính năng (Feature) | Mô tả chi tiết |
|---|---|---|
| **CRM** | Quản lý đa đối tượng | Hỗ trợ tạo khách cá nhân và khách tổ chức (Form có thêm trường tên Công ty, Mã số thuế, Người đại diện). |
| **CRM** | Auto-fill thông tin | Ô search SĐT/CCCD dạng Dropdown suggest. Khi click chọn đúng khách sẽ fill toàn bộ form. |
| **Tiếp nhận** | Khai báo nhiều người ký | Form hồ sơ có nút `[+] Thêm người ký` để gán >1 khách hàng vào chung 1 văn bản chứng thực. |
| **Phí** | Báo giá siêu tốc (Pre-quote) | Ngay khi điền loại dịch vụ và số lượng, UI hiển thị khối Báo giá. Bắt buộc có nút Tick `[x] Khách đồng ý` mới lưu sang bước sau. |
| **Biểu mẫu** | Auto-generate Lời chứng | Có kho template Lời chứng chuẩn pháp lý. Hệ thống tự map các biến `{{Ten_Khach}}`, `{{CCCD}}`, `{{Ngay_Cap}}` từ form vào file in. |
| **Phí** | Bảng giá động & Phụ phí | Cấu hình biểu phí: Dịch vụ = "Chứng thực", Đơn vị tính = "Bản", Giá = 10.000. Có box nhập "Phụ phí" tự do (số tiền + lý do). |
| **Tích hợp** | **Zalo OA Trigger** | **Webhook lắng nghe sự kiện:** Bắt event `Trạng thái hồ sơ == Hoàn tất`. Nếu hồ sơ có lưu SĐT hợp lệ, gọi API Zalo ZNS gửi tin nhắn CSKH. |
| **Tích hợp** | API Hóa đơn điện tử | Gom mảng Item (Phí dịch vụ chính, Phụ phí) và Tổng tiền sang hệ thống Hóa đơn điện tử để xuất HD có mã cơ quan thuế. |
| **Tiếp nhận O2O** | Quản lý Hồ sơ nháp (Pending) | Cần có màn hình riêng biệt để quản lý các "Hồ sơ tạo qua kênh Online", cho phép xem trước file đính kèm mà chưa cần khách có mặt. |
