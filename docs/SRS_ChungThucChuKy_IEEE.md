# Software Requirements Specification
## for Phân hệ Nghiệp vụ Chứng Thực Chữ Ký - Dự án ERP VPCC

**Version 1.0 approved**
**Prepared by Nguyễn Văn Tuấn**
**Danish Software**
**17 tháng 06, 2026**

---

## 1. Giới thiệu (Introduction)
### 1.1 Mục đích (Purpose) 
Tài liệu SRS này đặc tả các yêu cầu phần mềm cho phân hệ **Nghiệp vụ Chứng Thực Chữ Ký** thuộc dự án **ERP VPCC**. Mục đích của phân hệ là chuẩn hóa và số hóa quy trình tiếp nhận, báo giá, sinh lời chứng tự động, và thu tiền đối với giao dịch chứng thực chữ ký tại Văn phòng công chứng, bao gồm cả luồng trực tiếp (Offline) và luồng đặt trước (Online to Offline - O2O).

### 1.2 Quy ước tài liệu (Document Conventions)
- Mức độ ưu tiên (Priority): Cao (High), Trung bình (Medium), Thấp (Low).
- Mã yêu cầu: Đánh mã theo định dạng `REQ-[Module]-[ID]` (VD: `REQ-CTCK-01`).
- Các biểu đồ luồng và trình tự được thể hiện bằng Mermaid format.

### 1.3 Đối tượng độc giả (Intended Audience)
- **Nhà quản lý/Trưởng VPCC:** Đọc Phần 1 và Phần 2 để nắm bắt mục tiêu, các luồng nghiệp vụ thực tế và bối cảnh vận hành.
- **Lập trình viên (Developers) & Kiểm thử viên (Testers):** Đọc kỹ Phần 3, Phần 4 và Phần 5 để hiểu rõ đặc tả kỹ thuật, các biến thể Use Case (Nhiều người ký, Doanh nghiệp, Người nước ngoài) và logic xử lý.
- **Nhân sự nghiệp vụ (Lễ tân, Thư ký, Kế toán):** Đọc Phần 4 để hiểu chi tiết luồng tương tác với hệ thống.

### 1.4 Phạm vi sản phẩm (Product Scope)
ERP VPCC là giải pháp phần mềm ERP điều phối toàn bộ vận hành VPCC. Phân hệ Chứng Thực Chữ Ký tập trung vào việc quản lý khách hàng đa đối tượng (Cá nhân, Pháp nhân, Nhiều người ký), báo giá siêu tốc (Pre-quote), tự động map dữ liệu (Auto-merge data) vào các mẫu Lời chứng phức tạp, và tích hợp trả kết quả qua Zalo OA.

### 1.5 Tài liệu tham khảo (References)
- Tài liệu PRD Tổng quan hệ thống CRM VPCC.
- Các quy định tại Nghị định 23/2015/NĐ-CP về cấp bản sao từ sổ gốc, chứng thực bản sao từ bản chính, chứng thực chữ ký và chứng thực hợp đồng, giao dịch.

## 2. Mô tả tổng quan (Overall Description)
### 2.1 Bối cảnh sản phẩm (Product Perspective)
Hệ thống là một phân hệ cốt lõi của nền tảng ERP VPCC, hoạt động trên môi trường Web. Phân hệ này bổ sung khả năng xử lý hồ sơ O2O (Online to Offline), giúp khách hàng gửi tài liệu trước qua Zalo/Web và chỉ mất 2-3 phút tại quầy để ký tên.

### 2.2 Chức năng cốt lõi (Product Functions)
- Quản lý đa đối tượng: Cá nhân, Pháp nhân (Doanh nghiệp), Nhiều người cùng ký, Người nước ngoài.
- Tiếp nhận hồ sơ O2O (Hồ sơ nháp - Pending) qua kênh Online.
- Báo giá siêu tốc (Pre-quote) dựa trên cấu hình bảng giá động.
- Auto-generate Lời chứng: Tự động điền thông tin các bên vào Lời chứng chuẩn pháp lý.
- Quản lý tiến độ thanh toán và phát hành hóa đơn điện tử.
- Trigger Webhook Zalo OA để gửi tin nhắn CSKH sau khi hoàn tất.

### 2.3 Phân quyền người dùng (User Classes and Characteristics)
- **Lễ tân / Nhân viên tiếp nhận:** Thao tác tạo hồ sơ nhanh tại quầy, tra cứu thông tin khách hàng, báo phí và in Lời chứng.
- **Công chứng viên / Người tiếp nhận chứng thực:** Trực tiếp chứng kiến khách hàng ký tên và ký duyệt, đóng dấu.
- **Kế toán:** Đối soát tiền mặt/chuyển khoản, xuất biên lai và hóa đơn VAT.
- **Khách hàng (Tác nhân gián tiếp):** Ký tên trực tiếp tại quầy hoặc gửi file nháp qua Zalo từ trước.

### 2.4 Môi trường hoạt động (Operating Environment)
- Ứng dụng Web-based (Cloud-native), yêu cầu kết nối Internet.
- Hỗ trợ hiển thị trên máy tính (PC) tại quầy giao dịch.

### 2.5 Ràng buộc thiết kế và triển khai (Design and Implementation Constraints)
- Lời chứng phải tuyệt đối chính xác về mặt định dạng, khoảng cách, font chữ theo quy định pháp luật.
- Quy trình yêu cầu **khách hàng bắt buộc phải ký trước mặt người tiếp nhận**. Hệ thống không cho phép bỏ qua bước kiểm tra vật lý này.

### 2.6 Tài liệu hướng dẫn (User Documentation)
- Tài liệu hướng dẫn sử dụng ERP VPCC và các bộ mẫu template Lời chứng chuẩn.

### 2.7 Giả định và phụ thuộc (Assumptions and Dependencies)
- Giả định khách hàng cung cấp giấy tờ tùy thân hợp lệ và văn bản không có nội dung vi phạm pháp luật/trái đạo đức xã hội.
- Phụ thuộc vào API Zalo ZNS và API Hóa đơn điện tử.

### 2.8 Các trường hợp thực tế (Real World Cases)
> [!NOTE]
> Chứng thực chữ ký là một trong những nghiệp vụ diễn ra rất thường xuyên. Đặc điểm là quy trình diễn ra nhanh, khách hàng bắt buộc ký ngay tại quầy trước mặt người tiếp nhận hồ sơ.

#### Case 1: Cá nhân chứng thực giấy ủy quyền (Phổ biến nhất)
- **Bối cảnh:** Anh A đến văn phòng để chứng thực chữ ký trên "Giấy ủy quyền nhận lương hưu" cho người nhà.
- **Thực tế:** Anh A mang theo CCCD gốc và mẫu giấy ủy quyền tự viết hoặc in sẵn.
- **Yêu cầu hệ thống:** Nhập nhanh thông tin anh A, in Lời chứng chứng thực chữ ký (dành cho 1 người ký), đính kèm vào giấy ủy quyền.

#### Case 2: Nhiều người cùng ký trên một văn bản
- **Bối cảnh:** Hai vợ chồng (Anh B và Chị C) cùng đến ký trên văn bản cam kết tài sản chung.
- **Thực tế:** Cần lấy thông tin CCCD của cả 2 người.
- **Yêu cầu hệ thống:** Form tiếp nhận hồ sơ phải cho phép add thêm nhiều khách hàng vào chung một văn bản. Lời chứng xuất ra phải tự động hiển thị thông tin cả 2 vợ chồng vào mục "Người yêu cầu chứng thực".

#### Case 3: Doanh nghiệp chứng thực chữ ký trên đăng ký mẫu dấu
- **Bối cảnh:** Giám đốc công ty X đến chứng thực chữ ký để mở tài khoản ngân hàng.
- **Thực tế:** Người ký là Giám đốc, nhưng với tư cách pháp nhân là Công ty X. 
- **Yêu cầu hệ thống:** CRM phải lưu được thông tin khách hàng là tổ chức (Công ty X) và người đại diện pháp luật (Giám đốc). Lời chứng phải ghi rõ chức danh Giám đốc công ty X.

#### Case 4: Khách gửi hồ sơ Online và chỉ đến ký/nhận giấy tờ (O2O - Online to Offline)
- **Bối cảnh:** Khách hàng (hoặc đối tác ngân hàng/môi giới) muốn làm dịch vụ nhưng không muốn chờ đợi. Họ chụp ảnh/scan bản gốc và gửi file qua kênh Zalo/Web của VPCC trước.
- **Thực tế:** Nhân viên VPCC kiểm tra file ảnh hợp lệ, soạn sẵn lời chứng, tính phí và hẹn giờ khách qua. Khách đến chỉ cần chìa bản gốc ra đối chiếu, ký tên rồi lấy kết quả đi ngay (tiết kiệm 80% thời gian).
- **Yêu cầu hệ thống:** Hệ thống có tính năng tiếp nhận "Hồ sơ Online chờ xử lý". Nhân viên check file, lên báo giá, gửi lại Zalo cho khách chốt phí. Khi khách đến, chỉ cần đọc SĐT hoặc quét mã QR là phần mềm hiển thị ngay hồ sơ đã soạn sẵn, chuyển thẳng sang bước in ấn và ký kết.

### 2.9 Hành trình khách hàng & Luồng xử lý trên phần mềm (Customer Journey & System Flow)

#### 2.9.1 Luồng xử lý trực tiếp tại quầy (Offline)
Quy trình chuẩn từ lúc khách bước vào đến khi cầm hồ sơ đi về, **có luồng chốt báo giá trước khi ký để tránh rủi ro hủy dịch vụ**:

1. **Tiếp nhận và Khởi tạo hồ sơ:**
   - Khách đưa CCCD và yêu cầu chứng thực.
   - Lễ tân nhập số điện thoại -> Hệ thống tìm thấy khách quen -> Auto-fill thông tin.
   - Tự động sinh mã hồ sơ và chọn loại dịch vụ (số lượng bản).
2. **Báo giá và Xin xác nhận:**
   - Hệ thống tính phí tự động (VD: 3 bản x 10.000 + phụ phí bìa).
   - Lễ tân báo phí, khách đồng ý -> Checkbox `[x] Khách hàng đồng ý báo phí`.
3. **Quét giấy tờ và Soạn Lời chứng:**
   - Quét file gốc lưu vào hồ sơ.
   - Hệ thống tự động điền (Auto-merge data) Họ tên, CCCD vào mẫu Lời chứng chứng thực.
   - In Lời chứng kẹp vào văn bản.
4. **Ký chứng thực:**
   - Khách ký trước mặt Công chứng viên. CCV ký duyệt và đóng dấu giáp lai.
5. **Thu tiền và Xuất hóa đơn:**
   - Kế toán xác nhận thu tiền. Hệ thống gọi API xuất Hóa đơn điện tử.
6. **Hoàn tất (Zalo OA):**
   - Đổi trạng thái Hoàn tất. Hệ thống tự động gửi tin nhắn Zalo kèm link tra cứu hóa đơn.

#### 2.9.2 Luồng xử lý cho Hồ sơ đặt trước (O2O - Online to Offline)
Luồng này phục vụ khách hàng gửi tài liệu qua Zalo/Web trước để VPCC chuẩn bị, khách chỉ việc đến ký và lấy kết quả.

1. **Tiếp nhận Online:** Khách chụp ảnh/scan bản gốc gửi qua Zalo. Nhân viên tạo Hồ sơ nháp (Pending).
2. **Thẩm định & Báo giá Online:** Nhân viên xem trước file, phần mềm tính báo giá. Báo lại qua Zalo cho khách. Khách chat "Đồng ý".
3. **Chuẩn bị sẵn:** Lễ tân check `Đã chốt phí - Chờ khách đến`. Hệ thống soạn Lời chứng sẵn.
4. **Khách hàng đến quầy (Offline):** Khách đọc SĐT. Lễ tân gõ SĐT lấy ra Hồ sơ nháp, đối chiếu bản chính vật lý -> Cho khách Ký -> Đóng dấu -> Thu tiền. Tiết kiệm 80% thời gian chờ đợi.

## 3. Yêu cầu Giao diện bên ngoài (External Interface Requirements)
### 3.1 Giao diện người dùng (User Interfaces)
- Form tạo hồ sơ hỗ trợ chức năng `[+] Thêm người ký` linh hoạt.
- Ô search Khách hàng thiết kế dạng Dropdown suggest (tìm theo SĐT/CCCD).
- Màn hình quản lý riêng cho "Hồ sơ Online" (O2O) dạng danh sách Kanban (Chờ duyệt -> Đã chốt phí -> Chờ khách đến).

### 3.2 Giao diện phần cứng (Hardware Interfaces)
- Kết nối máy in laser để in Lời chứng trực tiếp lên giấy/văn bản của khách.
- Máy scan để lưu lại bản cứng có chữ ký/dấu đỏ.

### 3.3 Giao diện phần mềm (Software Interfaces)
- **Zalo OA API:** Lắng nghe webhook khi hồ sơ hoàn tất để gửi tin nhắn.
- **API Hóa đơn điện tử:** Gửi mảng Item (Phí dịch vụ, Phụ phí) để xuất hóa đơn.

### 3.4 Giao thức truyền thông (Communications Interfaces)
- Giao thức HTTPS.
- RESTful API giao tiếp giữa Frontend và Backend.

## 4. Tính năng Hệ thống (System Features)
### 4.1 UC-01: Tiếp Nhận & Khởi Tạo Hồ Sơ Chứng Thực
#### 4.1.1 Mô tả và Mức độ ưu tiên (Description and Priority)
- **Mô tả:** Tiếp nhận yêu cầu, tra cứu SĐT/CCCD để auto-fill thông tin khách hàng. Hỗ trợ nhiều trường hợp: Cá nhân, Nhiều người ký, Tổ chức.
- **Độ ưu tiên:** High

#### 4.1.2 Luồng xử lý / Tương tác (Stimulus/Response Sequences)
- *Action:* Lễ tân nhập SĐT vào ô tìm kiếm.
- *Response:* Hệ thống hiển thị Dropdown suggest. Khi click chọn, Auto-fill các trường thông tin.
- *Action:* Lễ tân bấm `[+] Thêm người ký`.
- *Response:* Hệ thống mở thêm block nhập liệu cho người thứ 2 (dành cho trường hợp 2 vợ chồng cùng ký).

#### 4.1.3 Yêu cầu chức năng chi tiết (Functional Requirements)
- `REQ-CTCK-01`: Ô search SĐT/CCCD phải là dạng Dropdown suggest, thời gian phản hồi < 1s.
- `REQ-CTCK-02`: Form hồ sơ cho phép gán $>1$ khách hàng vào chung 1 văn bản (Multi-signers).
- `REQ-CTCK-03`: Hỗ trợ form Tổ chức (có thêm trường Tên Công ty, Mã số thuế, Người đại diện pháp luật).
- `REQ-CTCK-04`: Hỗ trợ form bổ sung cho trường hợp đặc biệt: `[x] Điểm chỉ thay chữ ký`, `[x] Có người làm chứng`, `[x] Người nước ngoài` (có thêm phiên dịch).

### 4.2 UC-02: Báo Giá Siêu Tốc (Pre-quote)
#### 4.2.1 Mô tả và Mức độ ưu tiên (Description and Priority)
- **Mô tả:** Hệ thống tự động báo giá dựa trên số lượng chữ ký và loại văn bản. Bắt buộc chốt phí trước khi làm Lời chứng.
- **Độ ưu tiên:** High

#### 4.2.2 Luồng xử lý / Tương tác (Stimulus/Response Sequences)
- *Action:* Lễ tân nhập "Số lượng bản" = 3.
- *Response:* Hệ thống hiển thị khối Báo giá (3 bản x 10.000đ = 30.000đ).
- *Action:* Lễ tân thêm "Phụ phí: Bìa hồ sơ 5.000đ".
- *Response:* Tổng tiền cập nhật = 35.000đ. Hệ thống khóa nút "Tiếp tục" cho đến khi check `[x] Khách đồng ý`.

#### 4.2.3 Yêu cầu chức năng chi tiết (Functional Requirements)
- `REQ-FEE-01`: Cấu hình bảng giá động theo loại dịch vụ chứng thực chữ ký.
- `REQ-FEE-02`: Cho phép nhập tay Phụ phí tự do (Số tiền + Lý do).
- `REQ-FEE-03`: Bắt buộc tích `[x] Khách hàng đồng ý báo phí` mới được lưu sang bước in Lời chứng.

### 4.3 UC-03: Tự Động Sinh Lời Chứng & Ký Duyệt
#### 4.3.1 Mô tả và Mức độ ưu tiên (Description and Priority)
- **Mô tả:** Auto-merge dữ liệu từ form vào biểu mẫu Lời chứng. Hỗ trợ đa dạng template (Lời chứng 1 người, nhiều người, người dịch, điểm chỉ).
- **Độ ưu tiên:** High

#### 4.3.2 Luồng xử lý / Tương tác (Stimulus/Response Sequences)
- *Action:* Lễ tân bấm "Sinh lời chứng".
- *Response:* Hệ thống tự map các biến `{{Ten_Khach}}`, `{{CCCD}}`, `{{Chuc_Danh}}` vào template Word/PDF tương ứng.
- *Action:* Lễ tân in ra giấy kẹp vào văn bản để khách ký vật lý. Trạng thái chuyển thành "Chờ duyệt/Chờ đóng dấu".

#### 4.3.3 Yêu cầu chức năng chi tiết (Functional Requirements)
- `REQ-DOC-01`: Có kho quản lý Template Lời chứng linh hoạt.
- `REQ-DOC-02`: Tự động nhận diện chọn đúng mẫu Lời chứng (Ví dụ: Form có 2 người ký -> Dùng mẫu Lời chứng nhiều người; Có flag Điểm chỉ -> Dùng mẫu Lời chứng Điểm chỉ).
- `REQ-DOC-03`: Tự động lưu bản Lời chứng vừa sinh dưới dạng file đính kèm trong hồ sơ.

### 4.4 UC-04: Xử Lý Luồng Đặt Trước (O2O - Online to Offline)
#### 4.4.1 Mô tả và Mức độ ưu tiên (Description and Priority)
- **Mô tả:** Tiếp nhận file scan qua mạng, tạo hồ sơ nháp, báo giá trước qua chat. Khách đến chỉ cần cung cấp SĐT để rút hồ sơ.
- **Độ ưu tiên:** Medium

#### 4.4.2 Luồng xử lý / Tương tác (Stimulus/Response Sequences)
- *Action:* Khách gửi file PDF qua Zalo. Nhân viên upload lên hệ thống để tạo "Hồ sơ Online" (Pending).
- *Response:* Hệ thống tạo mã tạm thời. Nhân viên thẩm định và nhập số lượng để hệ thống tính báo giá.
- *Action:* Nhân viên chốt phí với khách qua Zalo và tích `Đã chốt phí - Chờ khách đến` trên CRM.
- *Action:* Khách đến quầy đọc SĐT. Lễ tân gõ SĐT và rút bộ hồ sơ ra, bấm chuyển thành Hồ sơ chính thức.

#### 4.4.3 Yêu cầu chức năng chi tiết (Functional Requirements)
- `REQ-O2O-01`: Màn hình quản lý riêng rẽ cho luồng Hồ sơ Online để không lẫn lộn với hồ sơ đang xếp hàng tại quầy.
- `REQ-O2O-02`: Hồ sơ Online được phép lưu file scan mà chưa bắt buộc nhập đầy đủ số CCCD nếu khách chưa cung cấp.
- `REQ-O2O-03`: Quy trình chuyển tiếp (Convert) từ Hồ sơ Online thành Hồ sơ Offline siêu tốc bằng 1 thao tác tìm kiếm SĐT.

### 4.5 UC-05: Thanh Toán & Tích Hợp Zalo OA
#### 4.5.1 Mô tả và Mức độ ưu tiên (Description and Priority)
- **Mô tả:** Thu tiền, xuất hóa đơn và tự động nhắn tin CSKH.
- **Độ ưu tiên:** High

#### 4.5.2 Functional Requirements
- `REQ-PAY-01`: Nút "Xác nhận thanh toán" gọi API đẩy mảng Item (Phí chính, Phụ phí) sang hệ thống Hóa đơn điện tử.
- `REQ-PAY-02`: Webhook lắng nghe sự kiện `Trạng thái hồ sơ == Hoàn tất`. Nếu hồ sơ có SĐT hợp lệ, gọi API Zalo ZNS để gửi tin nhắn kèm link tải hóa đơn.

## 5. Các Yêu cầu Phi chức năng khác (Other Nonfunctional Requirements)
### 5.1 Yêu cầu Hiệu năng (Performance Requirements)
- Tải file Lời chứng tự động (merge data) không vượt quá 3 giây.
- Tìm kiếm khách hàng bằng SĐT độ trễ dưới 500ms.

### 5.2 Yêu cầu An toàn (Safety Requirements)
- Hệ thống cần giữ lại toàn bộ lịch sử (versioning) của các file Lời chứng được sinh ra phòng trường hợp cần tra soát pháp lý.

### 5.3 Yêu cầu Bảo mật (Security Requirements)
- Mọi thao tác thu tiền và xuất Lời chứng phải ghi nhận lại tài khoản đăng nhập (Audit Trails).

### 5.4 Thuộc tính Chất lượng Phần mềm (Software Quality Attributes)
- **Usability:** Form tiếp nhận phải thiết kế đủ rộng để có thể thao tác nhanh bằng phím `Tab` mà không cần dùng chuột nhiều.

### 5.5 Quy tắc Nghiệp vụ (Business Rules)
- Bắt buộc phải có chữ ký trực tiếp của người yêu cầu chứng thực trước mặt người tiếp nhận hồ sơ. Hệ thống không thể thay thế bước đối chiếu vật lý này.
- Phí chứng thực chữ ký (phần phí nhà nước) áp dụng bảng giá niêm yết cố định trên mỗi chữ ký/bản.

## 6. Các yêu cầu khác (Other Requirements)
- Không có.

## Phụ lục A: Thuật ngữ (Glossary)
- **O2O:** Online to Offline (Giao dịch bắt đầu từ mạng internet và kết thúc tại quầy vật lý).
- **ZNS:** Zalo Notification Service.

## Phụ lục B: Mô hình phân tích (Analysis Models)
*(Tham khảo luồng O2O tại tài liệu UseCase_ChungThucChuKy.md gốc)*

## Phụ lục C: Danh sách các mục cần làm rõ (To Be Determined List - TBD)
- [TBD] Xin cấp quyền Webhook từ tài khoản Zalo OA của VPCC.
