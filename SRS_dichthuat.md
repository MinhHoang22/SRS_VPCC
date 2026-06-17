# TÀI LIỆU ĐẶC TẢ YÊU CẦU PHẦN MỀM (SRS) – DỰ ÁN NOTARYOS
## Nghiệp vụ: Dịch Thuật Công Chứng & Chứng Thực Chữ Ký Người Dịch

**Phiên bản:** 1.0 - Chi tiết Kỹ thuật  
**Tác giả:** Vũ Minh Hoàng  
**Ngày hoàn thiện:** 17 tháng 06, 2026  

---

## 1. GIỚI THIỆU (INTRODUCTION)

### 1.1 Phạm vi sản phẩm (Product Scope)
**NotaryOS** là giải pháp phần mềm lõi (ERP) điều phối toàn bộ luồng vận hành của văn phòng công chứng (VPCC). Nghiệp vụ Dịch thuật Công chứng được thiết kế nhằm số hóa quy trình quản lý cộng tác viên dịch thuật (CTV), quản lý bản dịch nháp, kiểm soát tính chính xác của bản dịch, tự động tính phí dịch thuật dựa trên ngôn ngữ nguồn/đích, và tổ chức chứng thực chữ ký người dịch (chữ ký của CTV). Hệ thống đóng vai trò như một chốt chặn tài chính nghiêm ngặt, tích hợp hóa đơn điện tử và tương tác khách hàng qua Zalo OA.

### 1.2 Từ điển thuật ngữ (Glossary)
| Thuật ngữ | Định nghĩa |
|---|---|
| **VPCC** | Văn phòng Công chứng |
| **CTV** | Cộng tác viên dịch thuật (External Translator) |
| **CCV** | Công chứng viên (Notary Officer) |
| **CCCD** | Căn cước công dân |
| **Zalo OA** | Zalo Official Account - tài khoản chính thức của văn phòng |
| **B2B** | Business-to-Business (Giao dịch liên quan đến khách hàng doanh nghiệp) |
| **Lời chứng dịch** | Phần văn bản chứng thực chữ ký người dịch (translator's signature certification) theo mẫu pháp luật |

### 1.3 Tổng quát
Tài liệu này tập trung làm rõ luồng đi của hồ sơ Dịch thuật Công chứng qua 4 giai đoạn tương ứng với 4 Use Case chính: Tiếp nhận phân loại (Lễ tân), Phân công & Dịch thuật (Thư ký & CTV), Kiểm soát luồng & Ký đóng dấu (Thư ký & CCV offline), và Chốt chặn tài chính (Kế toán).

---

## 2. MÔ TẢ TỔNG QUAN (OVERALL DESCRIPTION)

### 2.1 Mô hình Kiến trúc và Phân quyền Người dùng
Hệ thống vận hành trên môi trường Web/Mobile, sử dụng kiến trúc vi dịch vụ (microservices). Quyền hạn trên hệ thống được phân tách nghiêm ngặt dựa trên vai trò (Role-based Access Control):
* **Lễ tân (Reception Clerk):** Tiếp nhận bản gốc tài liệu, nhập thông tin khách hàng, tính phí dự kiến, và tạo hồ sơ nháp.
* **Thư ký nghiệp vụ (Notary Secretary):** Phân công hồ sơ cho CTV, kiểm tra chất lượng bản dịch, chuẩn bị lời chứng bản dịch, trình CCV và người dịch ký offline, scan tài liệu hoàn tất tải lên hệ thống.
* **Cộng tác viên dịch thuật (CTV / Translator):** Đăng nhập tài khoản dành riêng cho CTV, nhận hồ sơ được phân công, tải tài liệu gốc, thực hiện dịch thuật và tải file dịch nháp (Word/PDF) lên hệ thống.
* **Công chứng viên (Notary Officer):** Ký tên và đóng dấu bản cứng thực tế (offline) xác nhận chữ ký người dịch. CCV không cần thao tác trực tiếp trên phần mềm đối với luồng dịch thuật.
* **Kế toán (Financial Accountant):** Đối soát doanh thu bóc tách (phí dịch, phí chứng thực chữ ký dịch), thu tiền và phát hành hóa đơn điện tử.

### 2.2 Sơ đồ Thực thể Dữ liệu Cốt lõi (ERD Entities)
* **CUSTOMER (Khách hàng):** Lưu trữ thông tin định danh (SĐT, Họ tên, CCCD, Email, MST nếu doanh nghiệp).
* **TRANSACTION_FILE (Hồ sơ giao dịch):** Lưu trạng thái dịch thuật, số trang gốc, ngôn ngữ nguồn/đích, ID thư ký phụ trách.
* **TRANSLATION_ASSIGNMENT (Phân công dịch thuật):** Lưu trữ liên kết giữa Hồ sơ giao dịch với ID CTV, mức thù lao trả cho CTV, hạn chót hoàn thành (deadline), và URL tập tin dịch nháp.
* **CHECKLIST_LOG (Nhật ký quy trình):** Lưu trạng thái kiểm tra (Đối khớp bản dịch, Chữ ký CTV vật lý, File scan bản cứng dấu đỏ).
* **BILLING_LEDGER (Sổ cái tài chính):** Bản ghi bất biến hạch toán chi tiết Phí dịch thuật (có thuế), Phí chứng thực chữ ký (miễn thuế), Phụ phí khác.

### 2.3 Sơ đồ Use Case Tổng quan nghiệp vụ Dịch thuật
```mermaid
flowchart TD
    Customer(["🧑‍💼 Khách hàng"])
    Receptionist(["👩‍💼 Lễ tân"])
    Secretary(["📝 Thư ký nghiệp vụ"])
    CTV(["🔤 Cộng tác viên"])
    Accountant(["💰 Kế toán"])

    subgraph NotaryOS_Dich_Thuat ["Phân hệ Dịch Thuật Công Chứng"]
        UC01("UC-01: Tiếp Nhận & Tính Phí Dịch Thuật")
        UC02("UC-02: Phân Công & Thực Hiện Dịch Thuật")
        UC03("UC-03: Kiểm Soát Luồng & Chứng Thực")
        UC04("UC-04: Chốt Chặn Kế Toán & Xuất Hóa Đơn")
    end

    Customer -->|Nộp bản gốc| Receptionist
    Receptionist --> UC01
    Secretary --> UC02
    CTV --> UC02
    Secretary --> UC03
    Accountant --> UC04
```

### 2.4 Sơ đồ Luồng hoạt động Nghiệp vụ (Activity Diagram)
```mermaid
  stateDiagram-v2
      [*] --> Tiếp_nhận
      Tiếp_nhận --> Khởi_tạo_hồ_sơ_dịch_thuật : Lễ tân
      Khởi_tạo_hồ_sơ_dịch_thuật --> Phân_công_cho_CTV : Thư ký
      Phân_công_cho_CTV --> Thực_hiện_dịch_và_tải_file_nháp : CTV
      Thực_hiện_dịch_và_tải_file_nháp --> Kiểm_tra_bản_dịch_và_checklist : Thư ký
      Kiểm_tra_bản_dịch_và_checklist --> Trình_CTV_và_CCV_ký_đóng_dấu_offline : Thư ký
      Trình_CTV_và_CCV_ký_đóng_dấu_offline --> Tải_file_scan_dấu_đỏ_lên_hệ_thống : Thư ký
      Tải_file_scan_dấu_đỏ_lên_hệ_thống --> Kế_toán_thu_tiền_và_bóc_tách_phí
      Kế_toán_thu_tiền_và_bóc_tách_phí --> Phát_hành_hóa_đơn_ĐT
      Phát_hành_hóa_đơn_ĐT --> Gửi_Zalo_OA
      Gửi_Zalo_OA --> [*]
```

### 2.5 Các trường hợp thực tế (Real Cases)

#### Case 1: Dịch thuật tài liệu cá nhân thông thường sang tiếng Anh (Phổ biến)
* **Bối cảnh:** Chị A mang Giấy khai sinh bản gốc đến yêu cầu dịch sang tiếng Anh và công chứng 2 bản lấy trong ngày.
* **Luồng xử lý trên hệ thống:**
  * Lễ tân tiếp nhận, nhập SĐT chị A (Hệ thống Auto-fill thông tin cá nhân). Lễ tân chọn Ngôn ngữ nguồn: **Tiếng Việt**, Ngôn ngữ đích: **Tiếng Anh**.
  * Lễ tân chọn loại tài liệu: **Giấy khai sinh** (1 trang gốc). Số bản cần dịch công chứng: 2 bản.
  * Hệ thống tự động áp đơn giá biểu phí: $50.000đ/\text{trang dịch tiếng Anh}$. Phí dịch gốc: $50.000đ$.
  * Phí chứng thực chữ ký người dịch (Nhà nước): $10.000đ/\text{chữ ký/bản} \times 2 \text{ bản} = 20.000đ$.
  * Tổng tính toán hệ thống: $70.000đ$. Lễ tân báo phí trọn gói $70.000đ$ và tích chọn `Khách hàng đồng ý báo phí`.
  * Thư ký phân công việc cho CTV dịch tiếng Anh in-house. CTV dịch xong, tải file dịch nháp (Word) lên NotaryOS.
  * Thư ký tải file nháp về kiểm tra, hệ thống tự động điền Lời chứng bản dịch. Thư ký in ra, trình CTV ký tên trực tiếp và CCV đóng dấu xác nhận chữ ký offline.
  * Thư ký scan bản cứng đã ký đóng dấu, tải lên hệ thống để mở chặn thanh toán. Kế toán thu $70.000đ$ tiền mặt và xuất hóa đơn điện tử tự động.

#### Case 2: Dịch thuật tài liệu doanh nghiệp chuyên ngành phức tạp sang tiếng Đức (B2B)
* **Bối cảnh:** Đại diện Công ty Y mang 1 tài liệu "Báo cáo tài chính" (15 trang) đến yêu cầu dịch sang tiếng Đức và chứng thực chữ ký dịch để gửi đối tác nước ngoài. Yêu cầu xuất hóa đơn doanh nghiệp gửi về email công ty.
* **Luồng xử lý trên hệ thống:**
  * Lễ tân bật toggle `Xuất hóa đơn doanh nghiệp (B2B)`, nhập MST của Công ty Y để tự động điền Tên công ty, Địa chỉ đăng ký.
  * Lễ tân chọn Ngôn ngữ nguồn: **Tiếng Việt**, Ngôn ngữ đích: **Tiếng Đức**. Nhập số trang gốc: 15 trang.
  * Hệ thống tự động áp đơn giá dịch tiếng Đức (ngôn ngữ hiếm): $150.000đ/\text{trang}$. Phí dịch gốc: $15 \times 150.000đ = 2.250.000đ$.
  * Lễ tân thỏa thuận thù lao dịch thuật chuyên ngành phức tạp và nhập "Tổng thực thu" là $2.500.000đ$ (chênh lệch $250.000đ$ là phụ phí thù lao dịch vụ tăng thêm). Hệ thống tự động hạch toán phần chênh lệch này vào mục "Phí dịch vụ khác".
  * Thư ký chỉ định một CTV chuyên dịch tài chính tiếng Đức trong danh sách liên kết. CTV nhận việc, ký cam kết bảo mật (NDA) trên hệ thống trước khi được phép tải bản scan tài liệu gốc.
  * CTV hoàn thành bản dịch, tải file dịch lên hệ thống. Thư ký kiểm tra, in bản dịch kèm lời chứng. CTV đến văn phòng ký tên offline trước mặt Thư ký và CCV đóng dấu xác nhận.
  * Thư ký scan bản cứng có dấu đỏ tải lên hệ thống. Kế toán xác nhận nhận chuyển khoản $2.500.000đ$, bấm phát hành hóa đơn B2B. Hệ thống gọi API xuất hóa đơn điện tử VAT gửi thẳng vào email Công ty Y.

#### Case 3: Dịch thuật công chứng đặt trước Online (O2O)
* **Bối cảnh:** Anh B chụp ảnh bản gốc Bằng tốt nghiệp đại học gửi qua tài khoản Zalo OA của văn phòng yêu cầu dịch sẵn sang tiếng Pháp để tiết kiệm thời gian chờ đợi.
* **Luồng xử lý trên hệ thống:**
  * Thư ký nhận được tin nhắn Zalo OA, lưu file ảnh và tạo một **Hồ sơ nháp (Pending)** trên NotaryOS.
  * Thư ký phân công ngay cho CTV dịch tiếng Pháp dịch trước. CTV tải file ảnh từ hồ sơ nháp, dịch xong và upload file dịch nháp lên hệ thống.
  * Thư ký chuẩn bị sẵn Lời chứng bản dịch in ra chờ sẵn.
  * Chiều cùng ngày, anh B đến văn phòng, cung cấp SĐT. Lễ tân nhập SĐT, hệ thống lấy ra ngay hồ sơ đặt trước. Thư ký đối chiếu bằng gốc vật lý của anh B với file ảnh trên hệ thống. 
  * Xác nhận khớp -> Cho CTV ký bản dịch offline, CCV đóng dấu. Thư ký scan file dấu đỏ tải lên. Kế toán thu tiền và đóng hồ sơ trong vòng 3 phút.

#### Case 4: Dịch thuật công chứng đa ngôn ngữ cho một bộ hồ sơ
* **Bối cảnh:** Chị C mang 1 bộ học bạ cấp 3 (5 trang) yêu cầu dịch sang cả **tiếng Anh** và **tiếng Pháp** để làm hồ sơ du học.
* **Luồng xử lý trên hệ thống:**
  * Lễ tân tạo hồ sơ, chọn Ngôn ngữ nguồn: Tiếng Việt, và chọn nhiều Ngôn ngữ đích: **Tiếng Anh** và **Tiếng Pháp** cùng lúc.
  * Hệ thống tự động tách hồ sơ thầu thành 2 hồ sơ giao dịch con độc lập:
    * Hồ sơ con 1: Dịch Tiếng Anh (5 trang, phí gốc 250.000đ).
    * Hồ sơ con 2: Dịch Tiếng Pháp (5 trang, phí gốc 400.000đ).
  * Hai hồ sơ con được gán cho 2 CTV khác nhau thực hiện dịch độc lập trên hệ thống.
  * Tuy nhiên, hệ thống tự động gom chung dữ liệu tài chính của 2 hồ sơ này dưới 1 mã thanh toán duy nhất có Tổng thực thu là $670.000đ$ để kế toán chỉ cần thực hiện thu tiền và xuất 1 hóa đơn tổng duy nhất cho chị C.

---

## 3. ĐẶC TẢ USE CASE CHI TIẾT (USE CASE SPECIFICATIONS)

### 3.1 UC-01: Tiếp Nhận & Tính Phí Dịch Thuật (Translation Reception)

#### 3.1.1 Đặc tả chi tiết
| Mã Use Case | UC-01 |
|---|---|
| **Tên Use Case** | Tiếp Nhận & Tính Phí Dịch Thuật |
| **Tác nhân chính** | Lễ tân (Reception Clerk) |
| **Mô tả** | Tiếp nhận tài liệu gốc từ khách hàng, chọn ngôn ngữ nguồn/đích, nhập số lượng trang gốc, tự động tính phí dịch thuật theo biểu giá và lưu hồ sơ dịch thuật. |
| **Sự kiện kích hoạt** | Lễ tân nhấn nút "Tạo hồ sơ Dịch thuật" trên màn hình Dashboard. |
| **Tiền điều kiện** | Lễ tân đã đăng nhập hệ thống; Khách hàng cung cấp tài liệu gốc. |
| **Hậu điều kiện** | Hồ sơ dịch thuật được tạo thành công trên hệ thống với trạng thái "Chờ phân công". |

##### Luồng sự kiện chính (Thành công):
| STT | Thực hiện bởi | Hành động |
|---|---|---|
| 1 | Lễ tân | Nhập số điện thoại khách hàng vào trường tìm kiếm để Auto-fill hoặc tạo mới profile khách. |
| 2 | Lễ tân | Chọn Ngôn ngữ nguồn (ví dụ: Tiếng Việt) và Ngôn ngữ đích (ví dụ: Tiếng Anh, Tiếng Pháp, Tiếng Đức). |
| 3 | Lễ tân | Nhập số trang gốc của tài liệu và số bản dịch công chứng cần xuất ra. |
| 4 | Hệ thống | Truy vấn bảng biểu phí ngôn ngữ, tự động tính phí dịch gốc: $Phí\_Dịch = Số\_trang \times Đơn\_giá\_ngôn\_ngữ$ và phí chứng thực chữ ký dịch: $10.000đ \times Số\_bản$. |
| 5 | Lễ tân | Nhập tổng số tiền thỏa thuận thực tế với khách vào trường "Tổng thực thu". |
| 6 | Hệ thống | Tự động tính phụ phí chênh lệch (nếu có) và lưu vào mục "Phí dịch vụ khác". |
| 7 | Lễ tân | Xác nhận báo phí với khách hàng và tích chọn checkbox `Khách hàng đồng ý báo phí`. |
| 8 | Lễ tân | Nhấn nút "Lưu và Chuyển xử lý". Hồ sơ được khởi tạo và gửi sang hàng đợi của Thư ký. |

##### Luồng sự kiện thay thế (Ngoại lệ):
* **5a. Tổng thực thu nhỏ hơn tổng phí gốc quy định:** Hệ thống hiển thị cảnh báo đỏ và khóa nút lưu (Tổng thực thu không được thấp hơn Phí dịch + Phí chứng thực nhà nước).
* **7a. Khách hàng yêu cầu hóa đơn doanh nghiệp (B2B):** Lễ tân bật toggle B2B và nhập MST doanh nghiệp. Hệ thống tự động gọi API Tổng cục Thuế để lấy tên và địa chỉ công ty đính kèm vào thông tin hóa đơn.

#### 3.1.2 Sơ đồ Luồng xử lý kỹ thuật (Sequence Diagram)
```mermaid
sequenceDiagram
    autonumber
    actor Staff as Lễ tân
    participant App as NotaryOS Client
    participant API as CRM & Billing API
    participant Tax as Tax API (GDT)

    Staff->>App: Nhập SĐT khách hàng & thông tin định danh
    App->>API: Truy vấn thông tin CRM
    API-->>App: Trả về thông tin khách hàng (Auto-fill)

    Staff->>App: Chọn ngôn ngữ nguồn/đích, số trang & số bản
    App->>API: Lấy đơn giá dịch thuật của cặp ngôn ngữ
    API-->>App: Trả về đơn giá trang dịch tương ứng
    App->>App: Tính phí dịch gốc & phí chứng thực chữ ký dịch
    Staff->>App: Nhập tổng số tiền thực thu thỏa thuận
    App->>App: Hạch toán thù lao dịch vụ khác = Thực thu - Phí gốc
    
    alt Yêu cầu hóa đơn B2B
        Staff->>App: Bật toggle B2B & nhập MST
        App->>Tax: Query MST doanh nghiệp
        Tax-->>App: Trả về tên, địa chỉ doanh nghiệp
    end

    Staff->>App: Tích chọn "Khách đồng ý báo phí" & bấm Lưu
    App->>API: Gửi yêu cầu tạo hồ sơ dịch thuật
    API-->>App: Trả về Mã hồ sơ giao dịch (Trạng thái: Chờ phân công)
```

#### 3.1.3 Bảng dữ liệu đầu vào (Input Data Specification)
| STT | Trường dữ liệu | Mô tả | Bắt buộc? | Điều kiện hợp lệ | Ví dụ |
|---|---|---|---|---|---|
| 1 | Số điện thoại | SĐT liên lạc của khách hàng | Có | Chỉ nhập số, độ dài 10 ký tự | 0909123456 |
| 2 | Họ và tên | Tên khách hàng cá nhân | Có | Chuỗi ký tự chữ | Nguyễn Văn A |
| 3 | Ngôn ngữ nguồn | Ngôn ngữ gốc của tài liệu | Có | Dropdown chọn từ danh sách | Tiếng Việt |
| 4 | Ngôn ngữ đích | Ngôn ngữ cần dịch sang | Có | Dropdown chọn từ danh sách | Tiếng Đức |
| 5 | Số trang gốc | Số trang tài liệu gốc | Có | Số nguyên dương > 0 | 15 |
| 6 | Số bản công chứng | Số bản dịch công chứng cần ra | Có | Số nguyên dương > 0 | 2 |
| 7 | Tổng thực thu | Số tiền thực tế thỏa thuận thu | Có | Số tiền $\ge$ Phí Gốc tính toán | 2500000 |
| 8 | Mã số thuế | MST của doanh nghiệp | Chỉ khi B2B=ON | Chuỗi ký tự số (10 hoặc 13 số) | 0314456789 |

---

### 3.2 UC-02: Phân Công & Thực Hiện Dịch Thuật (Assignment & Translation)

#### 3.2.1 Đặc tả chi tiết
| Mã Use Case | UC-02 |
|---|---|
| **Tên Use Case** | Phân Công & Thực Hiện Dịch Thuật |
| **Tác nhân chính** | Thư ký nghiệp vụ (Notary Secretary), Cộng tác viên dịch thuật (CTV / Translator) |
| **Mô tả** | Thư ký lựa chọn và phân công hồ sơ dịch thuật cho CTV phù hợp; CTV nhận việc, dịch thuật tài liệu và tải bản dịch nháp lên hệ thống. |
| **Sự kiện kích hoạt** | Thư ký mở hồ sơ "Chờ phân công" và chọn CTV. |
| **Tiền điều kiện** | Hồ sơ dịch thuật đã được tạo thành công ở UC-01. |
| **Hậu điều kiện** | Bản dịch nháp (Word/PDF) được tải lên hệ thống; hồ sơ chuyển sang trạng thái "Chờ kiểm tra". |

##### Luồng sự kiện chính (Thành công):
| STT | Thực hiện bởi | Hành động |
|---|---|---|
| 1 | Thư ký | Mở hồ sơ dịch thuật ở trạng thái "Chờ phân công". |
| 2 | Thư ký | Chọn Cộng tác viên dịch thuật (CTV) từ danh sách gợi ý của hệ thống (lọc theo cặp ngôn ngữ) và đặt thời hạn hoàn thành (deadline). |
| 3 | Thư ký | Nhấn nút "Giao việc". |
| 4 | Hệ thống | Gửi thông báo công việc mới đến tài khoản của CTV trên hệ thống. |
| 5 | CTV | Đăng nhập hệ thống, nhấn "Nhận việc" và tải bản scan tài liệu gốc về máy. |
| 6 | CTV | Thực hiện dịch thuật offline và lưu dưới dạng tập tin (.docx hoặc .pdf). |
| 7 | CTV | Tải tập tin dịch nháp lên hệ thống NotaryOS và nhấn "Hoàn thành bản dịch". |
| 8 | Hệ thống | Lưu file dịch nháp vào hồ sơ giao dịch, chuyển trạng thái hồ sơ sang "Chờ kiểm tra" và gửi thông báo cho Thư ký phụ trách. |

##### Luồng sự kiện thay thế (Ngoại lệ):
* **2a. Không tìm thấy CTV phù hợp trong danh mục:** Thư ký có thể chọn hình thức "Dịch In-house" và tự phân công hồ sơ cho chính tài khoản của Thư ký đó để thực hiện dịch trực tiếp.
* **5a. CTV không phản hồi/Từ chối nhận việc:** Hệ thống cho phép Thư ký thu hồi lệnh phân công sau 30 phút không phản hồi và thực hiện tái phân công hồ sơ cho CTV khác.

#### 3.2.2 Sơ đồ Luồng xử lý kỹ thuật (Sequence Diagram)
```mermaid
sequenceDiagram
    autonumber
    actor Sec as Thư ký nghiệp vụ
    actor CTV as Cộng tác viên dịch thuật
    participant App as NotaryOS Client
    participant API as Assignment API
    participant Storage as File Storage Service

    Sec->>App: Mở hồ sơ "Chờ phân công"
    App->>API: Lấy danh sách CTV theo cặp ngôn ngữ phù hợp
    API-->>App: Trả về danh sách CTV khả dụng
    Sec->>App: Chọn CTV & đặt deadline hoàn thành
    Sec->>App: Nhấn "Giao việc"
    App->>API: Gửi thông tin phân công dịch thuật
    API-->>CTV: Gửi thông báo công việc mới (Zalo/Email/In-App)
    
    CTV->>App: Đăng nhập & Bấm "Nhận việc"
    App->>API: Cập nhật trạng thái công việc (Đang thực hiện)
    CTV->>App: Tải bản scan tài liệu gốc về máy
    Note over CTV: CTV thực hiện dịch thuật offline sang file Word/PDF
    CTV->>App: Upload file dịch nháp lên hệ thống
    App->>Storage: Lưu trữ file dịch nháp
    Storage-->>App: Trả về file URL
    CTV->>App: Nhấn "Hoàn thành bản dịch"
    App->>API: Gửi yêu cầu cập nhật trạng thái (Chờ kiểm tra) & file URL
    API-->>Sec: Thông báo hồ sơ đã dịch xong
```

#### 3.2.3 Bảng dữ liệu đầu vào (Input Data Specification)
| STT | Trường dữ liệu | Mô tả | Bắt buộc? | Điều kiện hợp lệ | Ví dụ |
|---|---|---|---|---|---|
| 1 | ID Cộng tác viên | Mã định danh CTV được phân công | Có | CTV phải ở trạng thái "Hoạt động" | CTV-2026-009 |
| 2 | Thời hạn hoàn thành | Hạn chót nộp bản dịch (Deadline) | Có | Thời gian phải sau thời điểm hiện tại | 18/06/2026 17:00 |
| 3 | File dịch nháp | Tập tin chứa bản dịch của tài liệu | Có | Định dạng PDF hoặc DOCX; dung lượng < 25MB | ban_dich_khai_sinh.docx |

---

### 3.3 UC-03: Kiểm Soát Luồng & Chứng Thực Chữ Ký Người Dịch (Review & Certification)

#### 3.3.1 Đặc tả chi tiết
| Mã Use Case | UC-03 |
|---|---|
| **Tên Use Case** | Kiểm Soát Luồng & Chứng Thực Chữ Ký Người Dịch |
| **Tác nhân chính** | Thư ký nghiệp vụ (Notary Secretary) |
| **Mô tả** | Thư ký kiểm tra bản dịch nháp của CTV, in bản dịch kèm Lời chứng tự động điền, lấy chữ ký người dịch (CTV) và con dấu CCV offline, scan bản cứng dấu đỏ tải lên hệ thống để mở chặn thanh toán. |
| **Sự kiện kích hoạt** | Thư ký mở hồ sơ ở trạng thái "Chờ kiểm tra" trên Dashboard. |
| **Tiền điều kiện** | CTV đã upload bản dịch nháp lên hệ thống thành công (UC-02). |
| **Hậu điều kiện** | Bản scan dấu đỏ được tải lên hệ thống thành công; hồ sơ tự động chuyển sang trạng thái "Chờ thanh toán". |

##### Luồng sự kiện chính (Thành công):
| STT | Thực hiện bởi | Hành động |
|---|---|---|
| 1 | Thư ký | Mở hồ sơ dịch thuật, kiểm tra đối khớp nội dung bản dịch nháp với bản gốc. |
| 2 | Thư ký | Tích chọn checklist xác nhận: `[x] Bản dịch chính xác`, `[x] Đúng định dạng mẫu`. |
| 3 | Hệ thống | Tự động điền (Auto-fill) thông tin người dịch (Họ tên, bằng cấp ngôn ngữ của CTV), thông tin khách hàng vào biểu mẫu **Lời chứng bản dịch** tương ứng. |
| 4 | Thư ký | In bản dịch kèm Lời chứng ra giấy bản cứng. |
| 5 | Thư ký | Trình bản cứng cho CTV ký tên trực tiếp lên Lời chứng bản dịch (offline). |
| 6 | Thư ký | Trình bản cứng đã có chữ ký người dịch cho Công chứng viên (CCV) ký duyệt đóng dấu xác nhận chữ ký (offline). |
| 7 | Thư ký | Nhận lại bản cứng hoàn chỉnh có dấu đỏ, tiến hành chụp/scan và tải file scan lên hệ thống. |
| 8 | Thư ký | Nhấn nút "Hoàn thành & Chuyển kế toán". Hệ thống ghi nhận timestamp và tự động chuyển hồ sơ sang trạng thái "Chờ thanh toán" của Kế toán. |

##### Luồng sự kiện thay thế (Ngoại lệ):
* **1a. Phát hiện bản dịch bị sai sót nội dung:** Thư ký nhấn nút "Yêu cầu dịch lại", nhập ghi chú lỗi sai. Hệ thống tự động chuyển hồ sơ về trạng thái "Đang thực hiện" của CTV đó và gửi thông báo yêu cầu chỉnh sửa gấp cho CTV.
* **8a. Chưa hoàn thành checklist hoặc thiếu file scan dấu đỏ:** Hệ thống chặn không cho phép nhấn nút Hoàn thành, hiển thị cảnh báo đỏ và ghi nhận lỗi vi phạm quy trình vào báo cáo hiệu suất (Workflow KPI) của Thư ký.

#### 3.3.2 Sơ đồ Luồng xử lý kỹ thuật (Sequence Diagram)
```mermaid
sequenceDiagram
    autonumber
    actor Sec as Thư ký nghiệp vụ
    participant App as NotaryOS Client
    participant API as Workflow API
    participant Storage as File Storage Service

    Note over Sec, App: CCV và CTV thực hiện ký tên & đóng dấu vật lý offline
    Sec->>App: Mở hồ sơ "Chờ kiểm tra"
    Sec->>App: Đánh dấu tích hoàn tất checklist kiểm tra bản dịch
    App->>App: Tự động điền dữ liệu người dịch/khách hàng vào Lời chứng dịch thuật
    Sec->>App: In bản dịch và Lời chứng
    Sec->>Sec: Trình người dịch (CTV) ký tên offline
    Sec->>Sec: Trình CCV ký duyệt & đóng dấu đỏ offline
    Sec->>App: Scan bản cứng hoàn chỉnh có dấu đỏ & tải lên
    App->>Storage: Tải lên file scan (PDF/Image)
    Storage-->>App: Trả về URL file scan
    
    Sec->>App: Nhấn nút "Hoàn thành & Chuyển kế toán"
    App->>API: Gửi yêu cầu hoàn tất & file URL
    alt Checklist thiếu hoặc chưa upload file scan
        API-->>App: Từ chối, hiển thị cảnh báo đỏ, ghi log KPI vi phạm
    else Checklist và file scan hợp lệ
        API->>API: Ghi nhận dấu timestamp & file URL
        API-->>App: Thành công (Trạng thái: Chờ thanh toán)
    end
```

#### 3.3.3 Bảng dữ liệu đầu vào (Input Data Specification)
| STT | Trường dữ liệu | Mô tả | Bắt buộc? | Điều kiện hợp lệ | Ví dụ |
|---|---|---|---|---|---|
| 1 | Checklist Bản dịch | Xác nhận bản dịch chính xác | Có | Giá trị Boolean (True/False) | True |
| 2 | Checklist Định dạng | Xác nhận bản in đúng định dạng | Có | Giá trị Boolean (True/False) | True |
| 3 | File scan bản cứng | File scan tài liệu hoàn chỉnh có dấu đỏ | Có | Định dạng PDF, PNG, JPG; dung lượng < 25MB | scan_dich_thuat_hoan_thanh.pdf |

---

### 3.4 UC-04: Chốt Chặn Kế Toán & Phát Hành Hóa Đơn Tự Động (Accounting Gateway)

#### 3.4.1 Đặc tả chi tiết
| Mã Use Case | UC-04 |
|---|---|
| **Tên Use Case** | Chốt Chặn Kế Toán & Phát Hành Hóa Đơn Tự Động |
| **Tác nhân chính** | Kế toán (Financial Accountant) |
| **Mô tả** | Bóc tách dòng tiền doanh thu dịch vụ dịch thuật và lệ phí chứng thực chữ ký dịch của nhà nước, xác nhận thanh toán của khách hàng, gọi API xuất hóa đơn điện tử tự động và gửi Zalo OA cảm ơn. |
| **Sự kiện kích hoạt** | Kế toán chọn hồ sơ từ màn hình danh sách "Chờ thanh toán & Xuất hóa đơn". |
| **Tiền điều kiện** | Hồ sơ đã được Thư ký hoàn thành checklist kiểm soát và tải lên bản scan có dấu đỏ thành công (UC-03). |
| **Hậu điều kiện** | Dữ liệu tài chính được lưu bất biến vào sổ cái; hóa đơn điện tử được phát hành; Zalo OA gửi thành công. |

##### Luồng sự kiện chính (Thành công):
| STT | Thực hiện bởi | Hành động |
|---|---|---|
| 1 | Kế toán | Xem thông tin bóc tách chi phí tự động trên màn hình thanh toán. |
| 2 | Hệ thống | Tách biệt các mục doanh thu trên hóa đơn: Phí dịch thuật (doanh nghiệp thu, tính thuế VAT), Phí chứng thực chữ ký người dịch (Lệ phí nhà nước, miễn thuế). |
| 3 | Kế toán | Chọn phương thức thanh toán của khách hàng: Tiền mặt, Chuyển khoản, hoặc Quẹt thẻ POS. |
| 4 | Kế toán | Nhấn nút "Xác nhận Thanh toán & Xuất Hóa đơn". |
| 5 | Hệ thống | Gọi API tự động đồng bộ sang nhà cung cấp hóa đơn điện tử (VNPT/Vĩnh Hy) và nhận về Số hóa đơn chính thức cùng file hóa đơn PDF. |
| 6 | Hệ thống | Ghi bản ghi tài chính bất biến vào sổ cái hệ thống (không cho phép sửa đổi hay xóa). |
| 7 | Hệ thống | Kích hoạt gọi API Zalo OA, tự động gửi tin nhắn kèm link tải hóa đơn VAT và lời cảm ơn đến số điện thoại của khách hàng. |

##### Luồng sự kiện thay thế (Ngoại lệ):
* **5a. Mất kết nối API nhà cung cấp hóa đơn điện tử:**
  * 1. Hệ thống hiển thị cảnh báo "Mất kết nối với nhà cung cấp hóa đơn điện tử".
  * 2. Hệ thống lưu giao dịch thanh toán vào hàng đợi xử lý ngầm (Offline Queue).
  * 3. Hệ thống tạo và cho phép kế toán in một Biên lai tạm thời (Temporary Receipt) có chứa mã QR tra cứu tạm thời cho khách.
  * 4. Khi kết nối Internet / API khôi phục, tiến trình chạy ngầm (cron job) tự động thực hiện lại lệnh gọi (retry) để xuất hóa đơn điện tử và gửi Zalo OA cho khách hàng.
* **7a. Khách hàng không đăng ký Zalo:** Hệ thống tự động phát hiện gửi tin nhắn Zalo thất bại và thực hiện fallback tự động chuyển sang gửi tin nhắn SMS truyền thống.

#### 3.4.2 Sơ đồ Luồng xử lý kỹ thuật (Sequence Diagram)
```mermaid
sequenceDiagram
    autonumber
    actor Acc as Kế toán
    participant App as NotaryOS Client
    participant API as Billing & E-Invoice API
    participant Invoice as E-Invoice System (VNPT/Vĩnh Hy)
    participant Zalo as Zalo OA API

    Acc->>App: Chọn hồ sơ "Chờ thanh toán"
    App->>App: Hiển thị bóc tách phí dịch (có thuế) & phí chứng thực chữ ký (miễn thuế)
    Acc->>App: Chọn phương thức (Tiền mặt/Chuyển khoản/POS)
    Acc->>App: Nhấn "Xác nhận Thanh toán & Xuất Hóa đơn"
    App->>API: Gửi lệnh thanh toán & xuất hóa đơn
    
    API->>Invoice: Gửi thông tin xuất hóa đơn
    alt API hóa đơn hoạt động tốt
        Invoice-->>API: Trả về Số hóa đơn & PDF URL
        API->>API: Ghi bản ghi bất biến vào Sổ cái tài chính
        API->>Zalo: Gửi tin nhắn kèm hóa đơn cho khách hàng
        Zalo-->>API: Gửi thành công
    else API hóa đơn mất kết nối
        API-->>App: Trả về cảnh báo mất kết nối
        API->>API: Lưu giao dịch vào hàng đợi Offline (Cache)
        API->>API: Tạo Biên lai tạm thời (Temporary Receipt) có mã QR
        App->>Acc: In Biên lai tạm thời giao cho khách
        API->>API: Khởi chạy cron job tự động retry khi có mạng
    end
    API-->>App: Cập nhật thành công (Trạng thái: Hoàn tất)
```

#### 3.4.3 Bảng dữ liệu đầu vào (Input Data Specification)
| STT | Trường dữ liệu | Mô tả | Bắt buộc? | Điều kiện hợp lệ | Ví dụ |
|---|---|---|---|---|---|
| 1 | Phương thức thanh toán | Lựa chọn cách thức thanh toán | Có | Phải thuộc danh mục (Cash, Bank Transfer, POS) | Bank Transfer |
| 2 | Xác nhận thanh toán | Nút bấm xác thực đã nhận đủ tiền | Có | Giá trị Boolean khi nhấn xác nhận | True |
| 3 | API E-Invoice Response | Chuỗi dữ liệu trả về từ API hóa đơn | Có (tự động) | Phải chứa Số hóa đơn hợp lệ từ VNPT/Vĩnh Hy | VNPT-2026-00918 |

---

## 4. CÁC YÊU CẦU PHI CHỨC NĂNG (NON-FUNCTIONAL REQUIREMENTS)

### 4.1 Giao diện người dùng (User Interface)
* Thiết kế chế độ tối (Dark mode) sang trọng, giảm mỏi mắt cho nhân viên làm việc liên tục tại quầy.
* Bảng Dashboard điều phối dịch thuật của Thư ký phải hiển thị danh sách các hồ sơ "Chờ phân công" và "Chờ kiểm tra" trực quan, hỗ trợ lọc theo ngôn ngữ để phân công công việc nhanh gọn.
* CTV có giao diện tối giản trên cả Web và Mobile để nhận việc và upload tập tin dễ dàng.

### 4.2 Tính bảo mật và Toàn vẹn tài chính (Security & Financial Integrity)
* File dịch nháp của doanh nghiệp (B2B) chỉ được tải về bởi CTV được phân công sau khi đã tích xác nhận cam kết bảo mật (NDA).
* Sổ cái kế toán ghi nhận giao dịch thanh toán là bất biến (Read-only sau khi đã lưu). Nghiêm cấm mọi hành vi chỉnh sửa trực tiếp vào cơ sở dữ liệu.
* Lịch sử tác động (Audit Log) ghi nhận chi tiết: Ai đã tiếp nhận (Lễ tân), Thư ký nào phân công cho CTV nào, CTV nào upload file dịch, Thư ký nào kiểm tra và scan dấu đỏ, Kế toán nào bấm xuất hóa đơn, kèm theo mốc thời gian (timestamp) chính xác.

### 4.3 Ràng buộc (Constraints)
* Hệ thống bắt buộc phải có kết nối Internet để đồng bộ dữ liệu UCHI, API Tổng cục Thuế và API hóa đơn điện tử.
* Trong trường hợp ngoại tuyến, hệ thống chỉ cho phép lưu trữ tạm thời hồ sơ dịch thuật và in biên lai tạm, khóa tất cả luồng phê duyệt hợp đồng hoặc giao dịch pháp lý phức tạp khác.
