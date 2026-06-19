# Tài liệu Đặc tả Yêu cầu Phần mềm (Software Requirements Specification - SRS)
## Hệ thống ERP/CRM Văn phòng Công chứng )

**Phiên bản:** 1.0  
**Đơn vị phát triển:** Danish Software  
**Người soạn thảo:** Vũ Minh Hoàng  
**Ngày tạo:** 17 tháng 06, 2026  

---

## Mục lục

- **[Chương 1. Giới thiệu (Introduction)](#chương-1-giới-thiệu-introduction)**
  - [1.1 Mục đích (Purpose)](#11-mục-đích-purpose)
  - [1.2 Phạm vi (Scope)](#12-phạm-vi-scope)
  - [1.3 Từ điển thuật ngữ (Glossary)](#13-từ-điển-thuật-ngữ-glossary)
  - [1.4 Tài liệu tham khảo (References)](#14-tài-liệu-tham-khảo-references)
  - [1.5 Tổng quát (Overview)](#15-tổng-quát-overview)

- **[Chương 2. Các yêu cầu chức năng (Functional Requirements)](#chương-2-các-yêu-cầu-chức-năng-functional-requirements)**
  - [2.1 Các tác nhân (Actors)](#21-các-tác-nhân-actors)
  - [2.2 Các chức năng của hệ thống (System Functions)](#22-các-chức-năng-của-hệ-thống-system-functions)
  - [2.3 Biểu đồ use case tổng quan (Overall Use Case Diagram)](#23-biểu-đồ-use-case-tổng-quan-overall-use-case-diagram)
  - [2.4 Biểu đồ use case phân rã (Decomposed Use Case Diagrams)](#24-biểu-đồ-use-case-phân-rã-decomposed-use-case-diagrams)
    - [2.4.1 Phân rã nhóm chức năng Xác thực & Quản trị (Auth & Admin)](#241-phân-rã-nhóm-chức-năng-xác-thực--quản-trị-auth--admin)
    - [2.4.2 Phân rã nhóm chức năng Nghiệp vụ Hồ sơ (Dossier Processing)](#242-phân-rã-nhóm-chức-năng-nghiệp-vụ-hồ-sơ-dossier-processing)
    - [2.4.3 Phân rã module Quản lý khách hàng (CRM)](#243-phân-rã-module-quản-lý-khách-hàng-crm)
    - [2.4.4 Phân rã module Lưu trữ hồ sơ điện tử (Document Archive)](#244-phân-rã-module-lưu-trữ-hồ-sơ-điện-tử-document-archive)
    - [2.4.5 Phân rã module Quản lý phí & Tài chính (Fee & Billing)](#245-phân-rã-module-quản-lý-phí--tài-chính-fee--billing)
  - [2.5 Quy trình sử dụng phần mềm (Software User Workflow)](#2.5-quy-trinh-su-dung-phan-mem)
    - [2.5.1 Quy trình Nghiệp vụ Sao y bản chính](#2.5.1-quy-trinh-nghiep-vu-sao-y-ban-chinh)
    - [2.5.2 Quy trình Nghiệp vụ Dịch thuật công chứng](#2.5.2-quy-trinh-nghiep-vu-dich-thuat-cong-chung)
    - [2.5.3 Quy trình Nghiệp vụ Chứng thực chữ ký](#2.5.3-quy-trinh-nghiep-vu-chung-thuc-chu-ky)
  - [2.6 Đặc tả các usecase (Use Case Specifications)](#2.6-dac-ta-cac-usecase)
    - [2.6.1 Nhóm Use Case Xác thực & Hệ thống (Auth & Admin)](#2.6.1-nhom-use-case-xac-thuc-he-thong)
      - [UC001: Đăng nhập hệ thống](#uc001-đăng-nhập-hệ-thống)
      - [UC002: Thay đổi mật khẩu](#uc002-thay-đổi-mật-khẩu)
      - [UC003: Quản lý & Cấp tài khoản nhân sự](#uc003-quản-lý--cấp-tài-khoản-nhân-sự)
      - [UC004: Phân quyền & Thiết lập vai trò (RBAC)](#uc004-phân-quyền--thiết-lập-vai-trò-rbac)
    - [2.6.2 Nhóm Use Case Nghiệp vụ (Dossier & Checklist)](#2.6.2-nhom-use-case-nghiep-vu)
      - [UC005: Tiếp nhận khách hàng & Khởi tạo hồ sơ](#uc005-tiếp-nhận-khách-hàng--khởi-tạo-hồ-sơ)
      - [UC006: Thẩm định hồ sơ & Duyệt Checklist chặn](#uc006-thẩm-định-hồ-sơ--duyệt-checklist-chặn)
      - [UC007: Soạn thảo Lời chứng tự động](#uc007-soạn-thảo-lời-chứng-tự-động)
      - [UC008: Quét & Lưu trữ hồ sơ điện tử đã đóng dấu](#uc008-quét--lưu-trữ-hồ-sơ-điện-tử-đã-đóng-dấu)
    - [2.6.3 Nhóm Use Case Tài chính & Chăm sóc (Billing & CRM)](#2.6.3-nhom-use-case-tai-chinh-cham-soc)
      - [UC009: Thu phí & Đối soát dòng tiền](#uc009-thu-phí--đối-soát-dòng-tiền)
      - [UC010: Xuất hóa đơn điện tử tự động (VNPT/Vĩnh Hy)](#uc010-xuất-hoa-đơn-điện-tử-tự-động-vnptvĩnh-hy)
      - [UC011: Chăm sóc khách hàng tự động qua Zalo OA](#uc011-chăm-sóc-khách-hàng-tự-động-qua-zalo-oa)
- **[Chương 3. Các kịch bản nghiệp vụ thực tế (Real-world Cases)](#3-cac-kich-ban-nghiep-vu-thuc-te)**
  - [3.1 Nghiệp vụ Sao y bản chính](#3.1-nghiep-vu-sao-y-ban-chinh)
    - [3.1.1 Case 1: Sao y CCCD / Giấy tờ tùy thân của cá nhân tại quầy (Siêu tốc)](#3.1.1-case-1-sao-y-cccd)
    - [3.1.2 Case 2: Sao y Sổ đỏ / Giấy tờ sở hữu tài sản có kiểm tra ngăn chặn (UCHI)](#3.1.2-case-2-sao-y-so-do)
    - [3.1.3 Case 3: Sao y số lượng lớn (Vượt trần quy định) & Tự động tách hóa đơn](#3.1.3-case-3-sao-y-so-luong-lon)
    - [3.1.4 Case 4: Doanh nghiệp sao y giấy phép & Yêu cầu hóa đơn VAT (B2B)](#3.1.4-case-4-doanh-nghiep-sao-y-giay-phep)
    - [3.1.5 Case 5: Sao y giấy tờ có yếu tố nước ngoài (Yêu cầu Hợp pháp hóa lãnh sự)](#3.1.5-case-5-sao-y-giay-to-nuoc-ngoai)
    - [3.1.6 Case 6: Từ chối sao y các giấy tờ bị cấm chứng thực (Tẩy xóa, đóng dấu MẬT, rách nát)](#3.1.6-case-6-tu-choi-sao-y)

---

## Chương 1. Giới thiệu (Introduction)

### 1.1 Mục đích (Purpose)
Tài liệu Đặc tả Yêu cầu Phần mềm (SRS) này xác định và đặc tả chi tiết toàn bộ các yêu cầu chức năng và bối cảnh hoạt động của **Hệ thống ERP/CRM Văn phòng Công chứng ** được triển khai độc lập tại một văn phòng công chứng. Tài liệu đóng vai trò là:
- **Bản căn cứ kỹ thuật và nghiệp vụ:** Giúp Ban quản lý Văn phòng Công chứng và Danish Software thống nhất phạm vi tính năng, làm cơ sở chính xác để nghiệm thu sản phẩm.
- **Tài liệu đặc tả cho đội ngũ phát triển:** Hướng dẫn lập trình viên hiểu đúng luồng xử lý và quy tắc nghiệp vụ để thiết kế cơ sở dữ liệu và viết mã nguồn.
- **Căn cứ xây dựng kịch bản kiểm thử:** Giúp kiểm thử viên (Testers) xây dựng các ca kiểm thử (Test Cases) tương ứng với các luồng hoạt động chính và ngoại lệ của hệ thống.


### 1.2 Phạm vi (Scope)
Giải pháp quản trị tổng thể cho Văn phòng công chứng, giúp số hóa toàn bộ hoạt động vận hành thủ công lên một nền tảng chung. Hệ thống bao quát 3 lớp vận hành chính:
1. **Lớp Khách hàng (CRM):**     
    - Trung tâm lưu trữ dữ liệu khách hàng, Tổ chức / Công ty.
    - Hỗ trợ trực tiếp cho quá trình tạo hồ sơ nhanh chóng.
    - Lưu vết và hiển thị toàn bộ lịch sử các giao dịch với khách hàng và thông tin của khách hàng.
2. **Lớp Nghiệp vụ:** Số hóa toàn bộ quy trình xử lý hồ sơ bao gồm:
   - Quy trình tiếp nhận, khởi tạo và theo dõi trạng thái hồ sơ.
   - Quản lý biểu mẫu, hợp đồng và các phiên bản văn bản (được cấu hình chi tiết theo từng nghiệp vụ cụ thể).
   - Quản lý tính phí (tự động tính phí gốc, phí dịch vụ thù lao thỏa thuận, theo dõi trạng thái thanh toán và tích hợp xuất hóa đơn điện tử tự động).
   - Hệ thống checklist kiểm soát lỗi nghiệp vụ động và tích hợp tra cứu ngăn chặn tài sản (UCHI).
3. **Lớp Quản trị:** Quản lý nhân sự, thiết lập tài khoản và phân quyền vai trò (RBAC) chi tiết, báo cáo thống kê hiệu suất/doanh thu và theo dõi tiến độ công việc chung của toàn văn phòng.

#### Nghiệp vụ cốt lõi (Core Scope):
Tài liệu này đặc tả toàn diện và chi tiết tất cả các yêu cầu chức năng cho toàn bộ hệ thống cũng như quy trình chi tiết của 3 nghiệp vụ cốt lõi được định nghĩa trong Chương 2:
- Phân hệ nghiệp vụ **Sao y bản chính**.
- Phân hệ nghiệp vụ **Dịch thuật công chứng** (Chứng thực chữ ký người dịch).
- Phân hệ nghiệp vụ **Chứng thực chữ ký** (Cá nhân, ủy quyền, tờ khai).

Tất cả các mô tả, sơ đồ quy trình và đặc tả use case chi tiết của 3 nghiệp vụ này được trình bày trực tiếp và duy nhất trong tài liệu này để đảm bảo tính tập trung.

### 1.3 Từ điển thuật ngữ (Glossary)
| Thuật ngữ | Định nghĩa |
| :--- | :--- |
| **VPCC** | Văn phòng Công chứng |
| **CCV** | Công chứng viên (người có thẩm quyền ký và đóng dấu lời chứng) |
| **UCHI** | Cơ sở dữ liệu ngăn chặn giao dịch và lịch sử công chứng tài sản của Sở Tư pháp |
| **CRM** | Customer Relationship Management - Hệ thống quản lý thông tin khách hàng |
| **ERP** | Enterprise Resource Planning - Hệ thống quản trị nguồn lực doanh nghiệp |
| **RBAC** | Role-Based Access Control - Phân quyền truy cập dựa trên vai trò |
| **Lời chứng** | Phần nội dung pháp lý do CCV ký ghi nhận việc công chứng/chứng thực |
| **Bản chính** | Giấy tờ gốc do cơ quan thẩm quyền cấp làm cơ sở đối chiếu |
| **Audit Log** | Nhật ký hệ thống tự động lưu lại các hành động của người dùng |
| **MST** | Mã số thuế (dùng cho doanh nghiệp B2B) |
| **Người dịch** | Cộng tác viên dịch thuật tài liệu đã đăng ký chữ ký mẫu tại VPCC phục vụ luồng dịch thuật công chứng |
| **Người yêu cầu** | Cá nhân hoặc đại diện tổ chức nộp hồ sơ yêu cầu sao y, dịch thuật hoặc chứng thực chữ ký |
| **Biên lai tạm thời** | Chứng từ in tạm kèm mã QR tra cứu phục vụ khi API hóa đơn điện tử gặp sự cố mất kết nối |

### 1.4 Tài liệu tham khảo (References)
- Quy chuẩn đặc tả phần mềm: *IEEE Recommended Practice for Software Requirements Specifications,* IEEE Std 830-1998.
- [Luật Công chứng số 51/2014/QH13](https://vanban.chinhphu.vn/?pageid=27160&docid=177893) - Cổng Thông tin điện tử Chính phủ.
- [Nghị định số 13/2023/NĐ-CP về Bảo vệ dữ liệu cá nhân](https://vanban.chinhphu.vn/?pageid=27160&docid=207767) - Cổng Thông tin điện tử Chính phủ.
- [Nghị định số 23/2015/NĐ-CP về cấp bản sao, chứng thực bản sao, chứng thực chữ ký](https://vanban.chinhphu.vn/?pageid=27160&docid=178657) - Cổng Thông tin điện tử Chính phủ.
- [Nghị định số 123/2020/NĐ-CP quy định về hóa đơn, chứng từ](https://vanban.chinhphu.vn/?pageid=27160&docid=201488) - Cổng Thông tin điện tử Chính phủ.

### 1.5 Tổng quát (Overview)
Dự án được phát triển nhằm mục tiêu xây dựng một hệ thống quản trị tổng thể (ERP/CRM) chuyên biệt cho văn phòng công chứng. Hệ thống số hóa toàn bộ quy trình tiếp nhận hồ sơ tại quầy, (thẩm định pháp lý) và kiểm soát lỗi qua checklist chặn, tra cứu dữ liệu ngăn chặn giao dịch (UCHI), quản lý dòng tiền hạch toán và tự động xuất hóa đơn VAT, cũng như chăm sóc khách hàng tự động qua Zalo OA. Dự án giúp tối ưu hóa hiệu suất làm việc liên phòng ban (Thư ký, Công chứng viên, Kế toán, Admin), giảm thiểu 95% sai sót nghiệp vụ và nâng cao trải nghiệm dịch vụ khách hàng.

---

## Chương 2. Các yêu cầu chức năng (Functional Requirements)

### 2.1 Các tác nhân (Actors)
Hệ thống định nghĩa 5 tác nhân (vai trò người dùng) trực tiếp tương tác và vận hành trên hệ thống:

1. **Thư ký nghiệp vụ (Secretary):**
   - **Mô tả:** Nhân sự chuyên môn trực tiếp làm việc với khách hàng và xử lý hồ sơ từ đầu đến cuối quy trình nghiệp vụ.
   - **Nhiệm vụ trên hệ thống:**
     - Tiếp nhận khách hàng, tra cứu định danh hoặc tạo mới thông tin khách hàng (CRM).
     - Kết nối phần cứng tại quầy (máy đọc chip CCCD, máy quét mã QR, máy scan) để thu thập thông tin khách hàng và tài liệu gốc.
     - Khởi tạo hồ sơ nghiệp vụ, nhập các thông số đầu vào (loại giấy tờ, số trang, số bản).
     - Xác nhận báo phí dịch vụ với khách hàng.
     - Thực hiện kiểm tra các đầu mục của checklist động tương ứng với loại giấy tờ.
     - Tra cứu thông tin ngăn chặn tài sản trên CSDL UCHI đối với các tài sản rủi ro (như Sổ đỏ).
     - Sinh và in Lời chứng hoặc biểu mẫu hợp đồng để trình Công chứng viên ký offline.
     - Thu phí dịch vụ của khách hàng tại quầy (Tiền mặt, chuyển khoản hoặc POS) và bấm "Xác nhận đã thu phí" trên hệ thống.
     - Chụp/scan bản cứng tài liệu đã ký đóng dấu đỏ vật lý để tải lên hệ thống mở khóa luồng đối soát của Kế toán.

2. **Công chứng viên (Notary Officer):**
   - **Mô tả:** Người có thẩm quyền tư pháp chịu trách nhiệm xem xét, phê duyệt tối cao và ký lời chứng.
   - **Nhiệm vụ trên hệ thống:**
     - Công chứng viên có toàn bộ quyền hạn của Thư ký nghiệp vụ trên hệ thống (có thể tiếp nhận, xử lý hồ sơ và thu phí dịch vụ tại quầy).
     - Thực hiện ký đóng dấu bản cứng offline sau khi đã đối chiếu và duyệt trên hệ thống (đây là quyền hạn độc quyền của CCV, Thư ký không được phép ký).

3. **Kế toán (Accountant):**
   - **Mô tả:** Nhân sự phụ trách đối soát tài chính và quản lý hóa đơn tại văn phòng công chứng. Kế toán không trực tiếp thu phí tại quầy.
   - **Nhiệm vụ trên hệ thống:**
     - Theo dõi danh sách giao dịch ở trạng thái "Chờ đối soát".
     - Thực hiện đối soát tài chính: đối chiếu dòng tiền thực nhận (két tiền mặt thực tế hoặc tài khoản ngân hàng của văn phòng) với thông tin thu phí do Thư ký/CCV đã xác nhận.
     - Bấm "Xác nhận đối soát" để hệ thống tự động ghi sổ cái bất biến và gọi API phát hành hóa đơn điện tử gửi cho khách hàng.

4. **Quản trị viên (Admin):**
   - **Mô tả:** Nhân sự quản trị kỹ thuật, cấu hình hệ thống.
   - **Nhiệm vụ trên hệ thống:**
     - Quản lý tài khoản nhân sự (tạo mới, khóa, mở khóa tài khoản).
     - Thiết lập ma trận phân quyền dựa trên vai trò (RBAC) cho nhân viên.
     - Quản lý kho mẫu lời chứng, biểu mẫu hợp đồng động.
     - Cấu hình biểu phí dịch vụ (phí gốc và thù lao dịch vụ khác).
5. **Cộng tác viên dịch thuật:**
   - **Mô tả:** Nhân viên làm việc tự do bên ngoài, có thể truy cập vào hệ thống để thực hiện các công việc liên quan đến dịch thuật.
   - **Nhiệm vụ trên hệ thống:**
     - Thực hiện dịch thuật tài liệu do Thư ký gửi tải lên hồ sơ.
     - Upload bản dịch đã hoàn thiện để trình Công chứng viên phê duyệt.
     - Nhận phản hồi và chỉnh sửa bản dịch nếu cần.

### 2.2 Các chức năng của hệ thống (System Functions)
Các chức năng cốt lõi của hệ thống được phân chia theo các nhóm vận hành chính:

#### A. Quản lý khách hàng (CRM)
Module trung tâm lưu trữ dữ liệu khách hàng, hỗ trợ trực tiếp cho quá trình tạo hồ sơ nhanh chóng:
- **Quản lý khách hàng:** Thêm mới, cập nhật và lưu trữ thông tin định danh của khách hàng cá nhân (CCCD, SĐT) và doanh nghiệp/tổ chức (Mã số thuế, địa chỉ trụ sở).
- **Auto-fill & Tra cứu nhanh:** Tự động điền thông tin khách hàng cũ dựa vào SĐT, Căn cước công dân (CCCD) khi tạo hồ sơ mới, giúp rút ngắn thời gian nhập liệu.
- **Lịch sử giao dịch:** Lưu vết và hiển thị toàn bộ lịch sử hồ sơ, giao dịch của từng khách hàng tại văn phòng.
- **Tương tác đa kênh:** Tự động gửi tin nhắn chăm sóc, thông báo nhận kết quả và link hóa đơn VAT qua Zalo OA.

#### B. Nghiệp vụ Hồ sơ (Dossier Processing)
- **Tiếp nhận & Tạo hồ sơ:** Khởi tạo hồ sơ nghiệp vụ, tự động cấp mã hồ sơ duy nhất, chọn dịch vụ (Sao y, Dịch thuật, Chứng thực chữ ký). Tích hợp tra cứu CRM để auto-fill thông tin khách hàng.
- **Checklist động & Kiểm soát lỗi:** Áp đặt các danh sách kiểm tra bắt buộc tùy thuộc vào loại giấy tờ để ngăn ngừa lỗi kỹ thuật của Thư ký.
- **Tra cứu ngăn chặn (UCHI):** Kết nối API hệ thống UCHI của Sở Tư pháp để tra cứu trạng thái phong tỏa của thửa đất/tài sản rủi ro cao.
- **Soạn thảo & Quản lý phiên bản:** Tự động điền dữ liệu hồ sơ vào biểu mẫu Lời chứng có sẵn, quản lý các phiên bản tài liệu (Nháp, Đang xử lý, Chờ ký, Đã ký).
- **Ký duyệt & Đóng dấu:** Công chứng viên ký duyệt và đóng dấu lời chứng vật lý (quyền hạn độc quyền).
- **Scan & Lưu trữ tài liệu:** Hỗ trợ quét và lưu trữ bản chụp dấu đỏ đã hoàn thành lên hệ thống đám mây.

#### C. Lưu trữ hồ sơ điện tử (Document Archive)
Module lưu trữ toàn bộ các hồ sơ tài liệu đã hoàn thành giao dịch (sau khi đã in, ký và thu phí):
- **Kho lưu trữ tập trung:** Lưu trữ an toàn toàn bộ file scan bản cứng dấu đỏ, lời chứng, hợp đồng và các tài liệu liên quan lên hệ thống đám mây.
- **Tra cứu & Trích lục hồ sơ:** Hỗ trợ tìm kiếm nhanh theo mã hồ sơ, tên khách hàng, CCCD, ngày tạo, loại nghiệp vụ. Phục vụ việc trích lục hồ sơ nhanh chóng cho các nghiệp vụ về sau.
- **Quản lý vòng đời tài liệu:** Theo dõi trạng thái lưu trữ (Đang hoạt động, Lưu kho, Hết hạn bảo quản) theo quy định pháp luật.

#### D. Quản lý phí theo dịch vụ (Fee Management)
Module cung cấp cơ sở dữ liệu đơn giá để các module dịch vụ gọi ra và tính tổng tiền cho hồ sơ:
- **Cấu hình biểu phí:** Thiết lập đơn giá phí gốc nhà nước và thù lao dịch vụ riêng biệt cho từng loại dịch vụ (Sao y, Chứng thực chữ ký, Dịch thuật công chứng...).
- **Công thức tính phí tự động:** Tự động tính phí gốc theo số trang/bản, bóc tách thù lao dịch vụ khác, áp dụng đúng đơn giá từ biểu phí đã cấu hình.
- **Tự động tách hóa đơn:** Phân tách hóa đơn con khi phí gốc vượt trần pháp luật quy định ($\le 200.000đ$).
- **Lịch sử thay đổi biểu phí:** Ghi nhận nhật ký mọi lần cập nhật biểu phí (ai thay đổi, thời gian, giá trị cũ/mới).

#### E. Tài chính & Xuất hóa đơn (Billing & Invoice)
- **Thu phí dịch vụ tại quầy:** Thư ký/CCV tiếp nhận thanh toán từ khách hàng (Tiền mặt, Chuyển khoản, POS) và xác nhận thu phí trên hệ thống.
- **Đối soát dòng tiền:** Kế toán đối chiếu dòng tiền thực nhận (két tiền mặt, tài khoản ngân hàng) với giao dịch thu phí trên hệ thống.
- **Xuất hóa đơn điện tử:** Hệ thống tự động gọi API VNPT/Vĩnh Hy phát hành hóa đơn VAT sau khi Kế toán xác nhận đối soát.
- **Chăm sóc khách hàng:** Tự động gửi tin nhắn ZNS cảm ơn và link hóa đơn qua Zalo OA.

#### F. Hệ thống & Quản trị (Auth & Admin)
- **Xác thực & Bảo mật:** Đăng nhập, thay đổi mật khẩu, chính sách độ phức tạp mật khẩu, và session timeout tự động.
- **Quản trị tài khoản & Nhân sự:** Tạo mới, khóa/mở khóa tài khoản nhân viên.
- **Phân quyền RBAC:** Cấu hình ma trận quyền chi tiết (Xem, Thêm, Sửa, Xóa, Duyệt) cho từng vai trò đối với từng chức năng.
- **Nhật ký hệ thống (Audit Trail):** Ghi nhận bất biến thao tác của toàn bộ người dùng trên hệ thống.
- **Quản lý biểu mẫu:** Cấu hình mẫu lời chứng động và các biểu mẫu hợp đồng.

### 2.3 Biểu đồ use case tổng quan (Overall Use Case Diagram)

Dưới đây là sơ đồ Use Case tổng quan phân bổ theo các phân hệ chức năng và các tác nhân tương tác. Nhằm tối ưu hóa khả năng đọc hiểu, thông tin được thể hiện qua cả **Sơ đồ trực quan (Mermaid Diagram)** và **Bảng ma trận vai trò (Use Case Matrix)** chi tiết.

#### A. Sơ đồ Use Case tổng quan

Sơ đồ dưới đây phân chia hệ thống thành các phân vùng (subgraphs) tương ứng với các nhóm chức năng chính, cùng với các tác nhân (Actors) có liên kết tương tác trực tiếp hoặc kế thừa quyền:

```mermaid
flowchart LR
    %% Actors Definition
    Sec(["📝 Thư ký nghiệp vụ"])
    CCV(["⚖️ Công chứng viên"])
    Admin(["📊 Quản trị viên"])
    Acc(["💰 Kế toán"])
    Sys(["🤖 Hệ thống tự động"])

    %% System Boundary
    subgraph System ["Hệ thống ERP/CRM Văn phòng Công chứng"]
        direction TB
        
        subgraph Admin_Auth ["Hệ thống & Quản trị"]
            UC001("UC001: Đăng nhập hệ thống")
            UC002("UC002: Thay đổi mật khẩu")
            UC003("UC003: Cấp tài khoản nhân sự")
            UC004("UC004: Phân quyền RBAC")
        end
        
        subgraph CRM_Module ["Quản lý khách hàng - CRM"]
            UC_CRM("Quản lý khách hàng")
        end
        
        subgraph Dossier_Module ["Nghiệp vụ Hồ sơ"]
            UC005("UC005: Tiếp nhận & Tạo hồ sơ")
            UC006("UC006: Thẩm định & Duyệt Checklist")
            UC007("UC007: Soạn thảo Lời chứng tự động")
            UC012("UC012: Ký duyệt & Đóng dấu lời chứng")
            UC008("UC008: Quét & Lưu trữ file scan")
        end
        
        subgraph Archive_Module ["Lưu trữ hồ sơ điện tử"]
            UC_ARCHIVE("Lưu trữ & Tra cứu trích lục hồ sơ")
        end
        
        subgraph Fee_Module ["Quản lý phí theo dịch vụ"]
            UC_FEE("Cấu hình đơn giá & Tính phí")
        end
        
        subgraph Finance_Module ["Tài chính & CRM"]
            UC009("UC009: Thu phí dịch vụ tại quầy")
            UC010("UC010: Đối soát & Xuất hóa đơn")
            UC011("UC011: Chăm sóc qua Zalo OA")
        end
    end

    %% Inheritances
    CCV -->|Kế thừa quyền| Sec

    %% Thư ký nghiệp vụ Links
    Sec --- UC001
    Sec --- UC002
    Sec --- UC_CRM
    Sec --- UC005
    Sec --- UC006
    Sec --- UC007
    Sec --- UC008
    Sec --- UC009
    Sec --- UC_ARCHIVE

    %% Công chứng viên Links
    CCV --- UC012

    %% Quản trị viên Links
    Admin --- UC001
    Admin --- UC002
    Admin --- UC003
    Admin --- UC004
    Admin --- UC_FEE

    %% Kế toán Links
    Acc --- UC001
    Acc --- UC002
    Acc --- UC010

    %% Hệ thống Links
    Sys --- UC010
    Sys --- UC011

    %% Module Dependencies
    UC005 -.->|Tra cứu & Auto-fill| UC_CRM
    UC005 -.->|Lấy đơn giá| UC_FEE
    UC008 -.->|Lưu trữ| UC_ARCHIVE
```

#### B. Ma trận vai trò - Use Case (Use Case Matrix)

Bảng ma trận dưới đây làm rõ quyền hạn chi tiết và điểm tương tác của từng vai trò (Actor) đối với từng Use Case cụ thể trong hệ thống:

| Phân hệ / Nhóm chức năng | Mã UC | Tên Use Case | Thư ký nghiệp vụ | Công chứng viên | Kế toán | Quản trị viên | Hệ thống tự động |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: | :---: |
| **Hệ thống & Quản trị** | **UC001** | Đăng nhập hệ thống | ✔️ | ✔️ | ✔️ | ✔️ | |
| | **UC002** | Thay đổi mật khẩu | ✔️ | ✔️ | ✔️ | ✔️ | |
| | **UC003** | Quản lý & Cấp tài khoản nhân sự | | | | ✔️ | |
| | **UC004** | Phân quyền & Thiết lập vai trò (RBAC) | | | | ✔️ | |
| **Quản lý khách hàng (CRM)** | — | Quản lý khách hàng (Lưu trữ, tra cứu, auto-fill) | ✔️ | ✔️ *(Kế thừa)* | | | |
| **Nghiệp vụ Hồ sơ** | **UC005** | Tiếp nhận & Khởi tạo hồ sơ | ✔️ | ✔️ *(Kế thừa)* | | | |
| | **UC006** | Thẩm định & Duyệt Checklist chặn | ✔️ | ✔️ *(Kế thừa)* | | | |
| | **UC007** | Soạn thảo Lời chứng tự động | ✔️ | ✔️ *(Kế thừa)* | | | |
| | **UC012** | Ký duyệt & Đóng dấu lời chứng | | ✔️ *(Độc quyền)* | | | |
| | **UC008** | Quét & Lưu trữ hồ sơ điện tử đã đóng dấu | ✔️ | ✔️ *(Kế thừa)* | | | |
| **Lưu trữ hồ sơ điện tử** | — | Lưu trữ & Tra cứu trích lục hồ sơ | ✔️ | ✔️ *(Kế thừa)* | | | |
| **Quản lý phí theo dịch vụ** | — | Cấu hình đơn giá & Tính phí theo dịch vụ | | | | ✔️ | |
| **Tài chính & CRM** | **UC009** | Thu phí dịch vụ tại quầy | ✔️ | ✔️ *(Kế thừa)* | | | |
| | **UC010** | Đối soát & Xuất hóa đơn | | | ✔️ | | ✔️ *(Gọi API)* |
| | **UC011** | Chăm sóc khách hàng tự động qua Zalo OA | | | | | ✔️ *(Tự động)* |

> **Ký hiệu & Quy ước:**
> - **✔️**: Tác nhân có quyền thực hiện trực tiếp Use Case này.
> - **Kế thừa**: Công chứng viên (CCV) kế thừa toàn bộ quyền hạn xử lý của Thư ký nghiệp vụ.
> - **Độc quyền**: Quyền hạn đặc thù của chức vụ đó, các tác nhân khác hoàn toàn không thể thực hiện.

### 2.4 Biểu đồ use case phân rã (Decomposed Use Case Diagrams)

#### 2.4.1 Phân rã nhóm chức năng đăng nhập & Quản trị (Auth & Admin)
Nhóm chức năng này phục vụ quản lý tài khoản nhân viên, thiết lập mật khẩu và phân quyền hoạt động trong hệ thống:

```mermaid
flowchart LR
    Admin(["📊 Quản trị viên"])
    Staff(["🧑‍💼 Nhân viên (Thư ký, CCV, Kế toán)"])

    subgraph Auth_Admin_Decomposed ["Phân rã đăng nhập & Quản trị"]
        UC001("UC001: Đăng nhập hệ thống")
        UC002("UC002: Thay đổi mật khẩu")
        UC003("UC003: Quản lý & Cấp tài khoản")
        UC004("UC004: Phân quyền & Thiết lập vai trò")
    end

    Staff --> UC001
    Staff --> UC002

    Admin --> UC001
    Admin --> UC002
    Admin --> UC003
    Admin --> UC004
```

#### 2.4.2 Phân rã nhóm chức năng Nghiệp vụ Hồ sơ (Dossier Processing)
Nhóm chức năng nghiệp vụ xử lý tài liệu do Thư ký phụ trách, có sự tham gia phê duyệt nội dung trực tiếp của Công chứng viên:

```mermaid
flowchart LR
    Sec(["📝 Thư ký nghiệp vụ"])
    CCV(["⚖️ Công chứng viên"])

    subgraph Dossier_Decomposed ["Phân rã Nghiệp vụ Hồ sơ"]
        UC005("UC005: Tiếp nhận & Khởi tạo hồ sơ")
        UC006("UC006: Thẩm định & Duyệt Checklist")
        UC007("UC007: Soạn thảo Lời chứng")
        UC008("UC008: Quét & Lưu trữ file scan")
        UC012("UC012: Ký duyệt & Đóng dấu lời chứng")
        
        UC_UCHI("Tra cứu ngăn chặn UCHI")
    end

    CCV --> Sec

    Sec --- UC005
    Sec --- UC006
    Sec --- UC007
    Sec --- UC008

    CCV --- UC012

    UC006 -.->|include| UC_UCHI
```

#### 2.4.3 Phân rã module Quản lý khách hàng (CRM)
Module trung tâm lưu trữ dữ liệu khách hàng cá nhân và tổ chức/doanh nghiệp, hỗ trợ trực tiếp cho quá trình tạo hồ sơ nhanh chóng:

```mermaid
flowchart LR
    Sec(["📝 Thư ký nghiệp vụ"])
    CCV(["⚖️ Công chứng viên"])

    subgraph CRM_Decomposed ["Phân rã Quản lý khách hàng (CRM)"]
        CRM_Add("Thêm mới khách hàng")
        CRM_Update("Cập nhật thông tin khách hàng")
        CRM_Search("Tra cứu & Auto-fill khách hàng")
        CRM_History("Xem lịch sử giao dịch")
    end

    CCV -->|Kế thừa quyền| Sec

    Sec --- CRM_Add
    Sec --- CRM_Update
    Sec --- CRM_Search
    Sec --- CRM_History
```

#### 2.4.4 Phân rã module Lưu trữ hồ sơ điện tử (Document Archive)
Module lưu trữ toàn bộ các hồ sơ tài liệu đã hoàn thành giao dịch, phục vụ việc tra cứu và trích lục hồ sơ nhanh chóng:

```mermaid
flowchart LR
    Sec(["📝 Thư ký nghiệp vụ"])
    CCV(["⚖️ Công chứng viên"])

    subgraph Archive_Decomposed ["Phân rã Lưu trữ hồ sơ điện tử"]
        ARC_Store("Lưu trữ hồ sơ hoàn tất")
        ARC_Search("Tra cứu & Trích lục hồ sơ")
        ARC_Lifecycle("Quản lý vòng đời tài liệu")
    end

    CCV -->|Kế thừa quyền| Sec

    Sec --- ARC_Store
    Sec --- ARC_Search
    Sec --- ARC_Lifecycle
```

#### 2.4.5 Phân rã module Quản lý phí & Tài chính (Fee & Billing)
Module quản lý tổng thể về phí dịch vụ và tài chính, bao gồm: cấu hình biểu phí, tính phí tự động, thu phí tại quầy, đối soát dòng tiền và xuất hóa đơn điện tử.

##### A. Quản lý phí theo dịch vụ (Fee Management)
Cung cấp cơ sở dữ liệu về đơn giá để các module dịch vụ gọi ra và tính tổng tiền cho hồ sơ. Tính phí rõ ràng và minh bạch theo từng loại dịch vụ:

```mermaid
flowchart LR
    Admin(["📊 Quản trị viên"])
    Sys(["🤖 Hệ thống tự động"])

    subgraph Fee_Decomposed ["Phân rã Quản lý phí theo dịch vụ"]
        FEE_Config("Cấu hình biểu phí theo dịch vụ")
        FEE_Calc("Tính phí tự động theo trang/bản")
        FEE_Split("Tách hóa đơn khi vượt trần")
        FEE_Log("Lịch sử thay đổi biểu phí")
    end

    Admin --- FEE_Config
    Admin --- FEE_Log
    
    Sys --- FEE_Calc
    Sys --- FEE_Split

    FEE_Calc -.->|Lấy đơn giá| FEE_Config
```

##### B. Tài chính & Xuất hóa đơn (Billing & Invoice)
Nhóm chức năng thu phí, đối soát dòng tiền và xuất hóa đơn điện tử tự động — sử dụng dữ liệu biểu phí từ module Quản lý phí:

```mermaid
flowchart LR
    Sec(["📝 Thư ký nghiệp vụ"])
    CCV(["⚖️ Công chứng viên"])
    Acc(["💰 Kế toán"])
    Sys(["🤖 Hệ thống tự động"])

    subgraph Billing_Decomposed ["Phân rã Tài chính & Xuất hóa đơn"]
        UC009("UC009: Thu phí dịch vụ tại quầy")
        UC010("UC010: Đối soát & Xuất hóa đơn")
        UC011("UC011: Chăm sóc qua Zalo OA")
        
        UC_Split("Tách hóa đơn tự động")
    end

    CCV -->|Kế thừa quyền| Sec

    Sec --- UC009
    Acc --- UC010
    Sys --- UC010
    Sys --- UC011
    
    UC010 -.->|include| UC_Split
```

<a id="2.5-quy-trinh-su-dung-phan-mem"></a>
### 2.5 Quy trình sử dụng phần mềm (Software User Workflow)

Phần này mô tả quy trình tương tác chi tiết từng bước trên phần mềm NotaryOS giữa các vai trò đối với 3 nghiệp vụ cốt lõi: **Sao y bản chính**, **Dịch thuật công chứng** và **Chứng thực chữ ký**. Vai trò nhập liệu và xử lý tại quầy được giao hoàn toàn cho **Thư ký nghiệp vụ**, không sử dụng vai trò Lễ tân.

#### A. Sơ đồ hoạt động phối hợp (Swimlanes Activity Diagram)

Dưới đây là sơ đồ thể hiện luồng hoạt động phối hợp giữa các vai trò trên hệ thống:

```mermaid
flowchart TD
    subgraph Roles ["CÁC VAI TRÒ TRONG HỆ THỐNG"]
        direction LR
        R_Sec["📝 Thư ký nghiệp vụ"]
        R_CTV["🧑‍💻 CTV Dịch thuật"]
        R_CCV["⚖️ Công chứng viên"]
        R_Acc["💰 Kế toán"]
        R_Sys["🤖 Hệ thống tự động"]
    end

    %% General Workflow Sequence
    Start([Bắt đầu tiếp nhận]) --> Input[1. Tiếp nhận & Tra cứu CRM]
    Input --> ChooseBranch{2. Chọn loại nghiệp vụ}

    %% Branch 1: Sao y
    ChooseBranch -- Sao y bản chính --> SY_Calc[3a. Cấu hình trang/bản & Tính phí]
    SY_Calc --> SY_Checklist[4a. Duyệt Checklist động & Tra cứu UCHI Sổ đỏ]
    SY_Checklist --> SY_Template[5a. Tự động điền biểu mẫu Lời chứng Sao y]
    SY_Template --> CCV_Sign_SY[6a. CCV ký đóng dấu bản cứng offline]
    CCV_Sign_SY --> SY_Scan[7a. Quét bản cứng dấu đỏ & Tải lên]

    %% Branch 2: Dịch thuật
    ChooseBranch -- Dịch thuật công chứng --> DT_Config[3b. Chọn ngôn ngữ & Chọn CTV]
    DT_Config --> DT_Assign[4b. CTV nhận việc & Ký NDA online]
    DT_Assign --> DT_Translate[5b. CTV dịch thuật & Upload bản dịch nháp]
    DT_Translate --> DT_Check[6b. Thư ký duyệt chất lượng & Sinh Lời chứng dịch]
    DT_Check --> CTV_Sign_DT[7b. CTV ký chữ ký mẫu & CCV ký đóng dấu offline]
    CTV_Sign_DT --> DT_Scan[8b. Quét bản dịch dấu đỏ & Tải lên]

    %% Branch 3: Chứng thực chữ ký
    ChooseBranch -- Chứng thực chữ ký --> CT_CRM[3c. Nhập danh sách người ký]
    CT_CRM --> CT_Template[4c. Chọn template Lời chứng & Tính phí]
    CT_Template --> CT_Checklist[5c. Duyệt Checklist & Đối chiếu định danh CCCD]
    CT_Checklist --> CT_Sign[6c. Khách hàng ký/điểm chỉ trực tiếp tại quầy]
    CT_Sign --> CCV_Sign_CT[7c. CCV ký Lời chứng & Đóng dấu offline]
    CCV_Sign_CT --> CT_Scan[8c. Quét bản cứng dấu đỏ & Tải lên]

    %% Common End Phase
    SY_Scan --> CollectFee[Thu phí tại quầy & Xác nhận trên PM]
    DT_Scan --> CollectFee
    CT_Scan --> CollectFee

    CollectFee --> AccReconcile[Đối soát dòng tiền thực nhận]
    AccReconcile --> SysInvoice[Tự động bóc tách VAT & Gọi API Xuất Hóa đơn]
    SysInvoice --> ZaloSend[Gửi link Hóa đơn VAT & Cảm ơn qua Zalo OA]
    ZaloSend --> EndNode([Hoàn tất hồ sơ])
```

<a id="2.5.1-quy-trinh-nghiep-vu-sao-y-ban-chinh"></a>
#### 2.5.1 Quy trình Nghiệp vụ Sao y bản chính (Certified Copying Workflow)

Quy trình sử dụng phần mềm đối với nghiệp vụ Sao y bản chính được thực hiện tuần tự như sau:

1. **Tiếp nhận & Định danh Khách hàng (CRM):**
   - Thư ký nghiệp vụ yêu cầu khách hàng cung cấp số điện thoại hoặc Căn cước công dân (CCCD).
   - Thư ký nhập thông tin vào ô tìm kiếm nhanh CRM trên phần mềm.
   - **Hệ thống tự động tra cứu:** Nếu khách hàng đã từng giao dịch, hệ thống tự động điền (Auto-fill) các thông tin: Họ tên, số định danh cá nhân, địa chỉ liên hệ. Nếu khách hàng mới, Thư ký nhập nhanh các trường thông tin và lưu vào cơ sở dữ liệu CRM.
2. **Khởi tạo Hồ sơ & Áp phí tự động:**
   - Thư ký chọn loại dịch vụ là "Sao y bản chính", chọn loại giấy tờ tương ứng từ danh sách cấu hình sẵn (CCCD, Sổ đỏ, Bằng đại học, Học bạ...).
   - Thư ký nhập số trang của tài liệu gốc và số bản sao y khách hàng yêu cầu.
   - **Hệ thống tự động tính toán:** Tính phí gốc theo quy định nhà nước ($Phí\ gốc = Số\ trang \times Số\ bản \times 2.000đ$).
   - Thư ký báo phí trọn gói với khách hàng (bao gồm cả phí dịch vụ photo, in ấn, bìa hồ sơ, tra cứu...). Nhập số tiền thỏa thuận thực thu vào trường "Tổng thực thu". Hệ thống tự động ghi nhận phần chênh lệch thù lao dịch vụ khác.
   - Thư ký tích chọn checkbox `Khách hàng đồng ý báo phí` và bấm "Lưu hồ sơ". Hệ thống tạo mã hồ sơ duy nhất (dạng `SY-YYYYMMDD-XXXXX`) ở trạng thái "Đang xử lý".
3. **Thực hiện Checklist & Tra cứu Ngăn chặn (UCHI):**
   - Hệ thống tải động danh sách Checklist kiểm soát lỗi nghiệp vụ tương ứng với loại giấy tờ đã chọn.
   - Thư ký thực hiện đối chiếu thực tế bản chính và tích chọn hoàn thành 100% các đầu mục bắt buộc trên giao diện phần mềm (kiểm tra rách nát, tẩy xóa, dấu giáp lai, thời hạn sử dụng...).
   - *Đối với các giấy tờ sở hữu tài sản (như Sổ đỏ/Sổ hồng):* Thư ký bắt buộc phải click vào nút "UCHI Search". Hệ thống gọi API thời gian thực đến CSDL ngăn chặn của Sở Tư pháp.
     - **Nếu có ngăn chặn:** Hệ thống khóa nút in Lời chứng, đổi trạng thái hồ sơ thành "Bị ngăn chặn" và gửi cảnh báo đỏ. Thư ký thực hiện trả hồ sơ cho khách.
     - **Nếu bình thường:** Hệ thống mở khóa bước tiếp theo.
4. **Tự động điền & Tạo Lời chứng:**
   - Thư ký nhấn nút "Sinh Lời chứng". Hệ thống tự động lấy thông tin từ hồ sơ điền vào biểu mẫu lời chứng tương ứng (Ví dụ: `TEMP-SAOY-01`).
   - Thư ký xem trước bản nháp Lời chứng trên màn hình, chỉnh sửa thủ công nếu cần, sau đó nhấn "In Lời chứng" để chuyển lệnh in đến máy in vật lý tại văn phòng. Hồ sơ chuyển trạng thái sang "Chờ ký (CCV)".
5. **Ký tên & Đóng dấu (Offline):**
   - Thư ký kẹp bản sao y và Lời chứng vừa in trình Công chứng viên (CCV).
   - CCV thực hiện đối chiếu vật lý bản chính và bản sao, ký tên và đóng dấu đỏ vật lý lên tài liệu.
6. **Scan số hóa & Mở luồng thanh toán:**
   - Thư ký đặt tài liệu đã có chữ ký, con dấu đỏ của CCV vào máy scan tại quầy và tải file scan (định dạng PDF/JPG, tối đa 25MB) lên hồ sơ phần mềm.
   - Thư ký nhấn nút "Hoàn tất xử lý hồ sơ". Hệ thống chuyển trạng thái hồ sơ sang "Chờ thu phí".
7. **Thu phí tại quầy:**
   - Thư ký nhận tiền mặt, quẹt thẻ POS hoặc cho khách quét mã QR động chuyển khoản hiển thị trên màn hình.
   - Chọn phương thức thanh toán tương ứng trên phần mềm và nhấn "Xác nhận nhận đủ tiền". Trạng thái hồ sơ chuyển sang "Chờ đối soát".
8. **Đối soát & Phát hành Hóa đơn:**
   - Kế toán đối chiếu tiền mặt thực thu hoặc kiểm tra biến động số dư tài khoản ngân hàng, nhấn "Xác nhận đối soát".
   - **Hệ thống tự động xử lý tài chính:** Ghi nhận sổ cái bất biến, tự động tách hóa đơn nếu phí gốc vượt trần $200.000đ$ theo quy định pháp luật lệ phí, gọi API VNPT/Vĩnh Hy phát hành hóa đơn điện tử VAT gửi trực tuyến cho khách hàng. Trạng thái hồ sơ chuyển sang "Đã hoàn tất".
9. **Chăm sóc Khách hàng:**
   - Hệ thống tự động gửi tin nhắn Zalo OA chứa lời cảm ơn và link tra cứu/tải hóa đơn VAT cho khách hàng. Nếu khách hàng không đăng ký Zalo, hệ thống gửi SMS fallback.

<a id="2.5.2-quy-trinh-nghiep-vu-dich-thuat-cong-chung"></a>
#### 2.5.2 Quy trình Nghiệp vụ Dịch thuật công chứng (Certified Translation Workflow)

Quy trình sử dụng phần mềm đối với nghiệp vụ Dịch thuật công chứng (chứng thực chữ ký người dịch) gồm các bước sau:

1. **Tiếp nhận & CRM:**
   - Thư ký nghiệp vụ tiếp nhận bản chính tài liệu cần dịch từ khách hàng, thu thập thông tin khách hàng nhập vào CRM để auto-fill hoặc tạo mới thông tin.
2. **Cấu hình dịch thuật & Tính phí:**
   - Thư ký chọn ngôn ngữ nguồn (ví dụ: Tiếng Việt) và ngôn ngữ đích (ví dụ: Tiếng Anh). Nhập số trang tài liệu cần dịch.
   - Thư ký chọn Cộng tác viên dịch thuật (CTV) phù hợp từ danh sách CTV đã đăng ký chữ ký mẫu tại VPCC.
   - **Hệ thống tự động tính toán phí:** Tính toán phí gốc chứng thực chữ ký người dịch ($15.000đ/chữ\ ký \times Số\ chữ\ ký$) và thù lao dịch thuật thỏa thuận dựa trên đơn giá ngôn ngữ đã cấu hình.
   - Thư ký báo phí trọn gói với khách hàng, tích checkbox `Khách hàng đồng ý báo phí` và nhấn "Lưu hồ sơ". Trạng thái hồ sơ chuyển sang "Đang dịch".
3. **Phân công & Dịch thuật ngầm (Collaborative Translation):**
   - Hệ thống gửi thông báo phân công công việc đến tài khoản của CTV dịch thuật.
   - CTV đăng nhập hệ thống, ký cam kết bảo mật thông tin (NDA) trực tuyến dành riêng cho hồ sơ này, tải file tài liệu cần dịch xuống.
   - Sau khi hoàn thành bản dịch, CTV upload file dịch nháp (.docx) lên hệ thống.
4. **Kiểm tra chất lượng & Sinh Lời chứng dịch:**
   - Thư ký tải file dịch nháp về kiểm tra chất lượng. Nếu chưa đạt, gửi yêu cầu sửa kèm ghi chú cho CTV trên phần mềm.
   - Khi bản dịch đạt yêu cầu, Thư ký nhấn nút "Duyệt bản dịch". Hệ thống tự động tải Checklist dịch thuật (đối chiếu tên riêng, số liệu, định dạng...).
   - Thư ký tích chọn hoàn thành checklist, nhấn nút "Sinh Lời chứng dịch". Hệ thống tự động điền thông tin hồ sơ và thông tin CTV dịch thuật vào biểu mẫu lời chứng chứng thực chữ ký người dịch (Ví dụ: `TEMP-DICH-01`).
   - Thư ký in lời chứng kẹp bản dịch. Trạng thái hồ sơ chuyển sang "Chờ ký (CCV)".
5. **Ký chứng thực & Đóng dấu (Offline):**
   - CTV đến văn phòng ký trực tiếp vào lời chứng dịch thuật trước mặt CCV (hoặc xác thực chữ ký số nếu được cấu hình).
   - CCV ký tên xác nhận chữ ký người dịch và đóng dấu đỏ vật lý lên tài liệu dịch thuật công chứng.
6. **Scan số hóa & Thu phí:**
   - Thư ký scan bản cứng đã ký đóng dấu của CCV và CTV, tải file scan lên hệ thống. Nhấn "Hoàn tất xử lý". Trạng thái chuyển sang "Chờ thu phí".
   - Thư ký thu phí tại quầy (Tiền mặt/Chuyển khoản/POS) và nhấn "Xác nhận nhận đủ tiền". Trạng thái chuyển sang "Chờ đối soát".
7. **Đối soát & Xuất hóa đơn:**
   - Kế toán kiểm tra dòng tiền thực nhận, nhấn "Xác nhận đối soát".
   - Hệ thống bóc tách doanh thu dịch vụ, gọi API VNPT/Vĩnh Hy xuất hóa đơn điện tử VAT gửi cho khách hàng. Trạng thái đổi thành "Đã hoàn tất".
8. **Chăm sóc Khách hàng:**
   - Hệ thống tự động gửi tin nhắn Zalo OA/SMS cảm ơn kèm liên kết tải hóa đơn điện tử cho khách hàng.

<a id="2.5.3-quy-trinh-nghiep-vu-chung-thuc-chu-ky"></a>
#### 2.5.3 Quy trình Nghiệp vụ Chứng thực chữ ký (Signature Certification Workflow)

Quy trình sử dụng phần mềm đối với nghiệp vụ Chứng thực chữ ký (tờ khai, giấy ủy quyền, sơ yếu lý lịch...) gồm các bước sau:

1. **Tiếp nhận & CRM:**
   - Thư ký tiếp nhận yêu cầu chứng thực chữ ký từ khách hàng.
   - Thư ký nhập thông tin định danh của người yêu cầu vào CRM. Nếu văn bản yêu cầu nhiều người ký (ví dụ: vợ chồng cùng ủy quyền), Thư ký bấm "Thêm người ký" trên hệ thống để nhập định danh của tất cả các chủ thể cùng tham gia ký.
2. **Cấu hình & Báo phí:**
   - Thư ký chọn loại văn bản cần chứng thực và chọn mẫu Lời chứng phù hợp (Ví dụ: Lời chứng chữ ký cá nhân, Lời chứng điểm chỉ, Lời chứng người đại diện tổ chức...).
   - Nhập số bản cần chứng thực chữ ký.
   - **Hệ thống tự động tính phí:** Tính toán phí gốc chứng thực chữ ký ($15.000đ/chữ\ ký \times Số\ chữ\ ký \times Số\ bản$).
   - Thư ký báo phí trọn gói với khách hàng, tích checkbox `Khách hàng đồng ý báo phí` và bấm "Lưu hồ sơ". Trạng thái hồ sơ chuyển sang "Đang lý".
3. **Thực hiện Checklist & Đối chiếu định danh:**
   - Hệ thống tải động Checklist nghiệp vụ chứng thực chữ ký (kiểm tra năng lực hành vi dân sự, giấy tờ tùy thân còn hạn, văn bản không vi phạm điều cấm của pháp luật, không có nội dung hợp đồng chuyển dịch quyền sở hữu tài sản bắt buộc phải công chứng...).
   - Thư ký đối khớp khuôn mặt khách hàng với ảnh trên CCCD vật lý và tích chọn hoàn thành checklist trên phần mềm.
4. **Ký tên/Điểm chỉ trực tiếp & CCV ký đóng dấu:**
   - Khách hàng ký tên hoặc điểm chỉ trực tiếp lên văn bản giấy trước sự chứng kiến của Thư ký và CCV.
   - Thư ký in Lời chứng tương ứng đã được hệ thống tự động điền dữ liệu, dán kẹp vào văn bản.
   - CCV ký tên xác nhận và đóng dấu đỏ vật lý lên văn bản kẹp Lời chứng.
5. **Scan số hóa & Thu phí tại quầy:**
   - Thư ký scan bản văn bản đã ký đóng dấu đầy đủ, tải file scan lên hệ thống và bấm "Hoàn tất xử lý". Hồ sơ chuyển sang "Chờ thu phí".
   - Thư ký thu tiền mặt/chuyển khoản/POS tại quầy từ khách hàng, nhấn "Xác nhận nhận đủ tiền". Trạng thái hồ sơ chuyển sang "Chờ đối soát".
6. **Đối soát & Xuất hóa đơn:**
   - Kế toán đối soát dòng tiền thực tế, nhấn "Xác nhận đối soát".
   - Hệ thống ghi sổ cái bất biến, tự động bóc tách thuế VAT thù lao dịch vụ, gọi API VNPT/Vĩnh Hy xuất hóa đơn điện tử gửi cho khách hàng. Trạng thái đổi thành "Đã hoàn tất".
7. **Chăm sóc Khách hàng:**
   - Hệ thống tự động gửi tin nhắn Zalo OA/SMS cảm ơn kèm liên kết tải hóa đơn điện tử cho khách hàng.

<a id="2.6-dac-ta-cac-usecase"></a>
### 2.6 Đặc tả các usecase (Use Case Specifications)

<a id="2.6.1-nhom-use-case-xac-thuc-he-thong"></a>
#### 2.6.1 Nhóm Use Case Xác thực & Hệ thống (Auth & Admin)

##### UC001: Đăng nhập hệ thống
| Đặc tả Use Case | Chi tiết |
| :--- | :--- |
| **Mã Use Case** | UC001 |
| **Tên Use Case** | Đăng nhập hệ thống |
| **Tác nhân** | Thư ký nghiệp vụ, Công chứng viên, Kế toán, Quản trị viên (Tất cả nhân sự) |
| **Mô tả** | Người dùng đăng nhập vào hệ thống bằng tài khoản (Email) và mật khẩu để bắt đầu phiên làm việc. |
| **Sự kiện kích hoạt** | Người dùng truy cập đường dẫn hệ thống và nhấn nút Đăng nhập. |
| **Tiền điều kiện** | Người dùng đã được cấp tài khoản hoạt động trên hệ thống. |
| **Luồng sự kiện chính (Thành công)** | **STT \| Thực hiện bởi \| Hành động** <br>1. Người dùng \| Nhập Email và Mật khẩu vào form đăng nhập. <br>2. Người dùng \| Nhấn nút "Đăng nhập". <br>3. Hệ thống \| Kiểm tra tính hợp lệ của định dạng Email và sự tồn tại của tài khoản. <br>4. Hệ thống \| Xác thực mật khẩu đã mã hóa một chiều trong cơ sở dữ liệu. <br>5. Hệ thống \| Khởi tạo phiên làm việc (JWT Session), phân quyền theo vai trò người dùng. <br>6. Hệ thống \| Điều hướng người dùng về trang Dashboard tương ứng với vai trò của họ. |
| **Luồng sự kiện thay thế / Ngoại lệ** | **STT \| Thực hiện bởi \| Hành động** <br>**[ERR-AUTH-01] Nhập thiếu thông tin:** <br>3a. Hệ thống phát hiện bỏ trống Email hoặc Mật khẩu -> Hiển thị thông báo: "Vui lòng nhập đầy đủ thông tin". <br>**[ERR-AUTH-02] Tài khoản bị khóa:** <br>3b. Hệ thống phát hiện tài khoản đang bị khóa (Deactivated) -> Từ chối đăng nhập và hiển thị: "Tài khoản của bạn đã bị khóa, vui lòng liên hệ Admin". <br>**[ERR-AUTH-03] Sai mật khẩu:** <br>4a. Hệ thống phát hiện sai mật khẩu -> Hiển thị: "Email hoặc mật khẩu không chính xác" và tăng số lần đăng nhập sai của tài khoản lên 1. <br>**[ERR-AUTH-04] Khóa tài khoản do sai quá 5 lần:** <br>4b. Hệ thống phát hiện số lần nhập sai liên tiếp đạt 5 lần -> Tự động khóa tài khoản tạm thời trong 15 phút và hiển thị: "Tài khoản đã bị tạm khóa 15 phút do nhập sai quá 5 lần". |
| **Hậu điều kiện** | Phiên làm việc được tạo thành công; người dùng truy cập được Dashboard phân quyền. |

##### Bảng dữ liệu đầu vào của Use Case UC001:
| STT | Trường dữ liệu | Mô tả | Bắt buộc? | Điều kiện hợp lệ | Ví dụ |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Email | Tên đăng nhập của nhân viên | Có | Đúng định dạng email tiêu chuẩn | secretary@notary.vn |
| 2 | Mật khẩu | Mật khẩu truy cập | Có | Độ dài tối thiểu 8 ký tự | P@ssw0rd123 |

---

##### UC002: Thay đổi mật khẩu
| Đặc tả Use Case | Chi tiết |
| :--- | :--- |
| **Mã Use Case** | UC002 |
| **Tên Use Case** | Thay đổi mật khẩu |
| **Tác nhân** | Thư ký nghiệp vụ, Công chứng viên, Kế toán, Quản trị viên (Tất cả nhân sự) |
| **Mô tả** | Người dùng tự thay đổi mật khẩu hiện tại của mình để nâng cao tính bảo mật cho tài khoản. |
| **Sự kiện kích hoạt** | Người dùng nhấn vào nút "Đổi mật khẩu" trong phần cấu hình cá nhân. |
| **Tiền điều kiện** | Người dùng đã đăng nhập thành công vào hệ thống. |
| **Luồng sự kiện chính (Thành công)** | **STT \| Thực hiện bởi \| Hành động** <br>1. Người dùng \| Nhập mật khẩu hiện tại, mật khẩu mới và xác nhận mật khẩu mới. <br>2. Người dùng \| Nhấn nút "Lưu thay đổi". <br>3. Hệ thống \| Xác thực mật khẩu hiện tại có trùng khớp với dữ liệu lưu trữ. <br>4. Hệ thống \| Kiểm tra mật khẩu mới có đạt độ phức tạp yêu cầu (8 ký tự, chữ hoa, thường, số, ký tự đặc biệt). <br>5. Hệ thống \| Kiểm tra mật khẩu mới và xác nhận mật khẩu mới phải khớp nhau. <br>6. Hệ thống \| Mã hóa mật khẩu mới và lưu đè vào CSDL. <br>7. Hệ thống \| Hiển thị thông báo "Đổi mật khẩu thành công" và yêu cầu đăng nhập lại. |
| **Luồng sự kiện thay thế / Ngoại lệ** | **STT \| Thực hiện bởi \| Hành động** <br>**[ERR-PWD-01] Sai mật khẩu hiện tại:** <br>3a. Hệ thống phát hiện mật khẩu hiện tại không khớp -> Báo lỗi: "Mật khẩu hiện tại không chính xác". <br>**[ERR-PWD-02] Mật khẩu mới không đạt độ phức tạp:** <br>4a. Hệ thống phát hiện mật khẩu mới yếu -> Báo lỗi: "Mật khẩu phải từ 8 ký tự trở lên, gồm chữ hoa, thường, số và ký tự đặc biệt". <br>**[ERR-PWD-03] Xác nhận mật khẩu mới không khớp:** <br>5a. Hệ thống phát hiện mật khẩu mới và mật khẩu xác nhận không khớp -> Báo lỗi: "Xác nhận mật khẩu mới không trùng khớp". |
| **Hậu điều kiện** | Mật khẩu tài khoản được cập nhật; toàn bộ phiên đăng nhập cũ trên các thiết bị khác bị hủy bỏ. |

##### Bảng dữ liệu đầu vào của Use Case UC002:
| STT | Trường dữ liệu | Mô tả | Bắt buộc? | Điều kiện hợp lệ | Ví dụ |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Mật khẩu hiện tại | Mật khẩu đang sử dụng | Có | Khớp với mật khẩu hiện tại trong CSDL | P@ssw0rd123 |
| 2 | Mật khẩu mới | Mật khẩu mới mong muốn | Có | Tối thiểu 8 ký tự, đủ hoa/thường/số/đặc biệt | NewP@ss2026 |
| 3 | Xác nhận mật khẩu | Nhập lại mật khẩu mới để đối khớp | Có | Trùng khít hoàn toàn với trường "Mật khẩu mới" | NewP@ss2026 |

---

##### UC003: Quản lý & Cấp tài khoản nhân sự
| Đặc tả Use Case | Chi tiết |
| :--- | :--- |
| **Mã Use Case** | UC003 |
| **Tên Use Case** | Quản lý & Cấp tài khoản nhân sự |
| **Tác nhân** | Quản trị viên (Admin) |
| **Mô tả** | Admin thực hiện các thao tác quản lý vòng đời tài khoản của nhân viên: Cấp mới tài khoản, khóa hoặc mở khóa tài khoản. |
| **Sự kiện kích hoạt** | Admin truy cập mục "Quản lý nhân sự" và chọn "Thêm nhân viên" hoặc click nút "Khóa/Mở khóa" trên một tài khoản hiện có. |
| **Tiền điều kiện** | Admin đã đăng nhập thành công vào hệ thống. |
| **Luồng sự kiện chính (Thành công - Tạo tài khoản):** | **STT \| Thực hiện bởi \| Hành động** <br>1. Admin \| Nhập thông tin nhân viên mới: Họ tên, Email, Số điện thoại và chọn vai trò mặc định ban đầu. <br>2. Admin \| Nhấn nút "Tạo tài khoản". <br>3. Hệ thống \| Kiểm tra tính duy nhất của Email và Số điện thoại trong CSDL. <br>4. Hệ thống \| Tạo bản ghi tài khoản mới ở trạng thái "Chờ kích hoạt". <br>5. Hệ thống \| Tự động sinh mật khẩu ngẫu nhiên đạt chuẩn an toàn. <br>6. Hệ thống \| Gửi một email kích hoạt tự động chứa thông tin tài khoản và mật khẩu tạm thời kèm liên kết kích hoạt đến email nhân viên. <br>7. Hệ thống \| Hiển thị thông báo "Tạo tài khoản nhân viên thành công". |
| **Luồng sự kiện thay thế / Ngoại lệ** | **STT \| Thực hiện bởi \| Hành động** <br>**[ERR-ACC-01] Email hoặc SĐT đã tồn tại:** <br>3a. Hệ thống phát hiện Email hoặc SĐT đã được đăng ký bởi nhân viên khác -> Báo lỗi: "Email hoặc Số điện thoại đã tồn tại trên hệ thống". <br>**[Luồng phụ 1] Khóa tài khoản:** <br>1. Admin click nút "Khóa tài khoản" trên tài khoản nhân viên đang hoạt động. <br>2. Hệ thống chuyển trạng thái tài khoản sang "Bị khóa" (Deactivated). Toàn bộ JWT token hiện tại của tài khoản đó bị hủy lập tức, nhân viên bị logout và không thể đăng nhập. <br>**[Luồng phụ 2] Mở khóa tài khoản:** <br>1. Admin click nút "Mở khóa tài khoản" trên tài khoản đang bị khóa. <br>2. Hệ thống chuyển trạng thái tài khoản sang "Đang hoạt động" (Active), cho phép nhân viên đăng nhập bình thường. |
| **Hậu điều kiện** | Tài khoản nhân sự mới được tạo ở trạng thái Chờ kích hoạt hoặc tài khoản hiện tại được Khóa/Mở khóa thành công. |

##### Bảng dữ liệu đầu vào của Use Case UC003:
| STT | Trường dữ liệu | Mô tả | Bắt buộc? | Điều kiện hợp lệ | Ví dụ |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Họ và tên | Họ tên của nhân viên mới | Có | Chuỗi ký tự chữ | Trần Văn B |
| 2 | Email | Email công việc của nhân viên | Có | Định dạng email, chưa tồn tại trong hệ thống | tranvanb@notary.vn |
| 3 | Số điện thoại | SĐT liên hệ | Có | Gồm 10 số, chưa tồn tại trong hệ thống | 0987654321 |
| 4 | Vai trò | Vai trò phân quyền ban đầu | Có | Chọn 1 trong các vai trò (Thư ký, CCV, Kế toán, Admin) | Thư ký nghiệp vụ |

---

##### UC004: Phân quyền & Thiết lập vai trò (RBAC)
| Đặc tả Use Case | Chi tiết |
| :--- | :--- |
| **Mã Use Case** | UC004 |
| **Tên Use Case** | Phân quyền & Thiết lập vai trò (RBAC) |
| **Tác nhân** | Quản trị viên (Admin) |
| **Mô tả** | Admin cấu hình ma trận quyền hạn (Quyền Xem, Thêm, Sửa, Xóa mềm, Phê duyệt) cho từng vai trò trên từng module chức năng của hệ thống. |
| **Sự kiện kích hoạt** | Admin truy cập màn hình "Cấu hình phân quyền" trên hệ thống. |
| **Tiền điều kiện** | Admin đã đăng nhập thành công vào hệ thống. |
| **Luồng sự kiện chính (Thành công)** | **STT \| Thực hiện bởi \| Hành động** <br>1. Admin \| Chọn vai trò cần cấu hình (ví dụ: Thư ký nghiệp vụ). <br>2. Hệ thống \| Hiển thị danh sách các module chức năng và ma trận các quyền check/uncheck tương ứng. <br>3. Admin \| Thực hiện tích chọn hoặc bỏ tích chọn các quyền chi tiết cho vai trò đó. <br>4. Admin \| Nhấn nút "Lưu cấu hình quyền". <br>5. Hệ thống \| Kiểm tra tính hợp lệ của thiết lập quyền và ghi nhận cấu hình mới vào CSDL. <br>6. Hệ thống \| Áp dụng quyền mới ngay lập tức cho toàn bộ các tài khoản thuộc vai trò đó. <br>7. Hệ thống \| Ghi nhận hành động thay đổi phân quyền vào nhật ký hệ thống (Audit Log) (ID Admin, vai trò bị sửa đổi, danh sách quyền cũ/mới). <br>8. Hệ thống \| Thông báo "Cập nhật ma trận phân quyền thành công". |
| **Luồng sự kiện thay thế / Ngoại lệ** | **STT \| Thực hiện bởi \| Hành động** <br>**[ERR-RBAC-01] Tự tước quyền Admin:** <br>5a. Hệ thống phát hiện Admin bỏ chọn quyền "Quản lý phân quyền" của chính vai trò Admin -> Chặn lưu và báo lỗi: "Không thể tự tước quyền quản trị phân quyền của vai trò Admin hệ thống". |
| **Hậu điều kiện** | Ma trận phân quyền của hệ thống được cập nhật; Audit Log được ghi nhận chi tiết. |

##### Bảng dữ liệu đầu vào của Use Case UC004:
| STT | Trường dữ liệu | Mô tả | Bắt buộc? | Điều kiện hợp lệ | Ví dụ |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Vai trò | Vai trò cần cấu hình quyền | Có | Phải tồn tại trong danh mục vai trò hệ thống | Thư ký nghiệp vụ |
| 2 | Ma trận quyền | Tập hợp các checkbox quyền (Read, Create, Update, Delete, Approve) theo từng module | Có | Mảng các giá trị Boolean | `[{ module: "CRM", read: true, create: true, update: false }]` |

---

<a id="2.6.2-nhom-use-case-nghiep-vu"></a>
#### 2.6.2 Nhóm Use Case Nghiệp vụ (Dossier & Checklist)

##### UC005: Tiếp nhận khách hàng & Khởi tạo hồ sơ
| Đặc tả Use Case | Chi tiết |
| :--- | :--- |
| **Mã Use Case** | UC005 |
| **Tên Use Case** | Tiếp nhận khách hàng & Khởi tạo hồ sơ |
| **Tác nhân** | Thư ký nghiệp vụ |
| **Mô tả** | Thư ký tiếp nhận yêu cầu chứng thực từ khách hàng, tra cứu/nhập thông tin định danh và khởi tạo hồ sơ nghiệp vụ trên hệ thống. |
| **Sự kiện kích hoạt** | Thư ký nhấn nút "Tạo hồ sơ mới" trên Dashboard nghiệp vụ. |
| **Tiền điều kiện** | Thư ký nghiệp vụ đã đăng nhập thành công vào hệ thống. |
| **Luồng sự kiện chính (Thành công)** | **STT \| Thực hiện bởi \| Hành động** <br>1. Thư ký \| Nhập Số điện thoại/CCCD (Cá nhân) hoặc Mã số thuế (Doanh nghiệp) vào ô tìm kiếm. <br>2. Hệ thống \| Tìm kiếm trong CRM: Nếu có dữ liệu cũ, tự động điền (Auto-fill) thông tin định danh. Nếu chưa có, mở form thêm mới khách hàng. <br>3. Thư ký \| Chọn loại nghiệp vụ (Sao y bản chính, Chứng thực chữ ký, Dịch thuật công chứng). <br>4. Thư ký \| Chọn loại giấy tờ (CCCD, Sổ đỏ, Bằng cấp, Giấy phép kinh doanh,...) từ danh sách dropdown. <br>5. Thư ký \| Nhập các thông số kỹ thuật (Số trang gốc, Số bản cần làm). <br>6. Hệ thống \| Tự động tính phí gốc theo công thức của Nhà nước. <br>7. Thư ký \| Nhập số tiền thực tế thống nhất thu vào trường "Tổng thực thu" và báo phí cho khách. <br>8. Thư ký \| Tích chọn checkbox `Khách hàng đồng ý báo phí` và nhấn "Lưu hồ sơ". <br>9. Hệ thống \| Khởi tạo hồ sơ, tự động sinh Mã hồ sơ duy nhất, đặt trạng thái hồ sơ thành "Đang xử lý". |
| **Luồng sự kiện thay thế / Ngoại lệ** | **STT \| Thực hiện bởi \| Hành động** <br>**[ERR-DOS-01] Tổng thực thu nhỏ hơn Phí gốc:** <br>7a. Hệ thống phát hiện số thực thu nhỏ hơn phí gốc tính toán -> Hiển thị cảnh báo đỏ và chặn không cho lưu. <br>**[ERR-DOS-02] Kết nối API Thuế lỗi khi nhập MST:** <br>2a. Hệ thống gọi API thuế bị timeout -> Báo lỗi: "Mất kết nối API Thuế, vui lòng nhập tay thông tin doanh nghiệp" và mở khóa các ô tên công ty, địa chỉ để Thư ký nhập thủ công. <br>**[Luồng phụ 1] Chứng thực chữ ký người dịch:** <br>3a. Thư ký chọn loại "Dịch thuật công chứng" -> Hệ thống hiển thị thêm trường tìm kiếm "Người dịch (Cộng tác viên)". Thư ký nhập thông tin Người dịch để hệ thống liên kết chữ ký mẫu. |
| **Hậu điều kiện** | Bản ghi hồ sơ được tạo thành công trên hệ thống với trạng thái "Đang xử lý". |

##### Bảng dữ liệu đầu vào của Use Case UC005:
| STT | Trường dữ liệu | Mô tả | Bắt buộc? | Điều kiện hợp lệ | Ví dụ |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Số điện thoại | SĐT của khách hàng | Có | Gồm 10 chữ số | 0912345678 |
| 2 | Họ và tên | Tên khách hàng | Có | Chuỗi ký tự chữ | Nguyễn Văn A |
| 3 | Loại nghiệp vụ | Phân loại hồ sơ | Có | Thuộc danh mục (Sao y, Dịch thuật, Chứng thực) | Sao y bản chính |
| 4 | Loại giấy tờ | Danh mục giấy tờ hệ thống | Có | Phải chọn từ danh sách cấu hình sẵn | Sổ đỏ / Giấy chứng nhận |
| 5 | Số trang | Số trang tài liệu gốc | Có | Số nguyên dương > 0 | 4 |
| 6 | Số bản | Số bản cần chứng thực | Có | Số nguyên dương > 0 | 5 |
| 7 | Tổng thực thu | Tiền thu thỏa thuận | Có | Số tiền $\ge$ Phí gốc nhà nước | 100000 |
| 8 | Người dịch | ID của Cộng tác viên dịch thuật | Chỉ khi là Dịch thuật | Phải tồn tại trong CSDL cộng tác viên | CTV-002 |

---

##### UC006: Thẩm định hồ sơ & Duyệt Checklist chặn
| Đặc tả Use Case | Chi tiết |
| :--- | :--- |
| **Mã Use Case** | UC006 |
| **Tên Use Case** | Thẩm định hồ sơ & Duyệt Checklist chặn |
| **Tác nhân** | Thư ký nghiệp vụ |
| **Mô tả** | Thư ký đối chiếu tài liệu vật lý và thực hiện tích chọn đầy đủ checklist nghiệp vụ tương ứng và tra cứu trạng thái ngăn chặn tài sản (nếu có). |
| **Sự kiện kích hoạt** | Thư ký mở một hồ sơ ở trạng thái "Đang xử lý". |
| **Tiền điều kiện** | Hồ sơ đã được tạo thành công (UC005). |
| **Luồng sự kiện chính (Thành công)** | **STT \| Thực hiện bởi \| Hành động** <br>1. Thư ký \| Kiểm tra các tài liệu đính kèm. Hệ thống tự động tải bộ Checklist động theo loại giấy tờ đã chọn. <br>2. Thư ký \| Tích chọn hoàn thành lần lượt 100% các đầu mục trong checklist bắt buộc. <br>3. Thư ký \| Nhấn nút "UCHI Search" để hệ thống tự động gọi API kiểm tra ngăn chặn trên CSDL của Sở Tư pháp (nếu là giấy tờ tài sản như Sổ đỏ). <br>4. Hệ thống \| Trả về kết quả "Không có ngăn chặn". <br>5. Thư ký \| Nhấn nút "Xác nhận hoàn thành thẩm định". <br>6. Hệ thống \| Ghi nhận log hoàn tất thẩm định (Timestamp, ID Thư ký, checklist được chọn) và mở khóa tính năng in Lời chứng (UC007). |
| **Luồng sự kiện thay thế / Ngoại lệ** | **STT \| Thực hiện bởi \| Hành động** <br>**[ERR-CHK-01] Phát hiện giấy tờ giả mạo/lỗi vật lý:** <br>2a. Thư ký phát hiện lỗi vật lý -> Nhấn nút "Từ chối hồ sơ", nhập lý do từ chối. Hệ thống cập nhật hồ sơ thành "Đã hủy" và lưu log. <br>**[ERR-CHK-02] UCHI phát hiện tài sản đang bị ngăn chặn:** <br>4a. API UCHI trả về cờ "Đang bị ngăn chặn giao dịch" -> Hệ thống lập tức hiển thị cảnh báo đỏ, khóa nút in Lời chứng, đổi trạng thái hồ sơ sang "Bị ngăn chặn" và gửi cảnh báo về màn hình Quản lý. <br>**[ERR-CHK-03] Mất mạng / API UCHI lỗi:** <br>4b. API UCHI lỗi kết nối -> Hệ thống hiển thị: "UCHI offline, yêu cầu kiểm tra thủ công". Thư ký kiểm tra sổ ngăn chặn vật lý và tích chọn checklist bổ sung: `Xác nhận kiểm tra thủ công và chịu trách nhiệm`. Hệ thống ghi nhận log override. |
| **Hậu điều kiện** | Hệ thống xác thực hoàn tất thẩm định, ghi log an toàn và mở khóa quyền in Lời chứng. |

##### Bảng dữ liệu đầu vào của Use Case UC006:
| STT | Trường dữ liệu | Mô tả | Bắt buộc? | Điều kiện hợp lệ | Ví dụ |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Checklist trạng thái | Tập hợp các checkbox nghiệp vụ bắt buộc | Có | 100% phần tử phải nhận giá trị True | `[True, True, True]` |
| 2 | UCHI API Response | Kết quả trả về từ CSDL ngăn chặn | Chỉ khi check tài sản | Mã phản hồi thành công và không bị block | `{ blocked: false }` |
| 3 | Lý do override | Lý do kiểm tra thủ công khi mất mạng | Chỉ khi UCHI offline | Chuỗi văn bản mô tả nguyên nhân | "UCHI lỗi kết nối, đã check sổ ngăn chặn số 12" |

---

##### UC007: Soạn thảo Lời chứng tự động
| Đặc tả Use Case | Chi tiết |
| :--- | :--- |
| **Mã Use Case** | UC007 |
| **Tên Use Case** | Soạn thảo Lời chứng tự động |
| **Tác nhân** | Thư ký nghiệp vụ |
| **Mô tả** | Hệ thống tự động lấy thông tin khách hàng, số trang, số bản điền vào biểu mẫu Lời chứng (hoặc mẫu hợp đồng) tương ứng để Thư ký in ra giấy kẹp hồ sơ trình CCV. |
| **Sự kiện kích hoạt** | Thư ký click vào nút "Tạo Lời chứng" trong giao diện xử lý hồ sơ. |
| **Tiền điều kiện** | Hồ sơ đã vượt qua bước thẩm định checklist bắt buộc (UC006). |
| **Luồng sự kiện chính (Thành công)** | **STT \| Thực hiện bởi \| Hành động** <br>1. Thư ký \| Click chọn "Tạo Lời chứng" (hoặc chọn template hợp đồng tương ứng). <br>2. Hệ thống \| Tự động truy vấn thông tin khách hàng, thông tin nghiệp vụ và thông tin CCV phụ trách. <br>3. Hệ thống \| Điền tự động (Auto-fill) các dữ liệu trên vào biểu mẫu Lời chứng. <br>4. Hệ thống \| Hiển thị bản nháp Lời chứng trên màn hình cho Thư ký kiểm tra. <br>5. Thư ký \| Nhấn nút "In Lời chứng". <br>6. Hệ thống \| Chuyển lệnh in tới máy in tại văn phòng và đổi trạng thái hồ sơ sang "Chờ ký (CCV)". |
| **Luồng sự kiện thay thế / Ngoại lệ** | **STT \| Thực hiện bởi \| Hành động** <br>**[ERR-PRT-01] Lỗi máy in vật lý:** <br>6a. Máy in mất kết nối hoặc kẹt giấy -> Hệ thống hiển thị cảnh báo: "Lỗi kết nối máy in, vui lòng kiểm tra thiết bị" và cho phép Thư ký tải về file PDF Lời chứng để thực hiện in thủ công từ thiết bị khác. |
| **Hậu điều kiện** | Bản Lời chứng được in thành công; trạng thái hồ sơ chuyển sang "Chờ ký (CCV)". |

##### Bảng dữ liệu đầu vào của Use Case UC007:
| STT | Trường dữ liệu | Mô tả | Bắt buộc? | Điều kiện hợp lệ | Ví dụ |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Template ID | Mã biểu mẫu cần điền dữ liệu | Có | Phải thuộc kho mẫu lời chứng hệ thống | TEMP-SAOY-01 |

---

##### UC008: Quét & Lưu trữ hồ sơ điện tử đã đóng dấu
| Đặc tả Use Case | Chi tiết |
| :--- | :--- |
| **Mã Use Case** | UC008 |
| **Tên Use Case** | Quét & Lưu trữ hồ sơ điện tử đã đóng dấu |
| **Tác nhân** | Thư ký nghiệp vụ, Công chứng viên |
| **Mô tả** | Sau khi CCV ký tên đóng dấu vật lý offline, Thư ký hoặc CCV thực hiện quét (scan)/chụp bản dấu đỏ và tải file lên hệ thống để lưu trữ điện tử và mở khóa luồng thu phí cho Thư ký/CCV tại quầy. |
| **Sự kiện kích hoạt** | Thư ký hoặc CCV nhấn nút "Tải lên bản scan dấu đỏ" trong giao diện hồ sơ. |
| **Tiền điều kiện** | Hồ sơ ở trạng thái "Chờ ký (CCV)" và đã được CCV ký đóng dấu vật lý hoàn tất. |
| **Luồng sự kiện chính (Thành công)** | **STT \| Thực hiện bởi \| Hành động** <br>1. Thư ký / CCV \| Đặt tài liệu đã đóng dấu vào máy scan kết nối hoặc chụp hình tài liệu. <br>2. Thư ký / CCV \| Click chọn file scan (PDF hoặc hình ảnh) từ thiết bị và tải lên hệ thống. <br>3. Hệ thống \| Kiểm tra dung lượng và định dạng file tải lên. <br>4. Hệ thống \| Lưu trữ file an toàn lên cloud storage và ghi URL vào hồ sơ. <br>5. Thư ký / CCV \| Nhấn nút "Hoàn tất xử lý hồ sơ". <br>6. Hệ thống \| Cập nhật hồ sơ thành trạng thái "Chờ thu phí", mở khóa tính năng thu phí trên màn hình nghiệp vụ của Thư ký/CCV. |
| **Luồng sự kiện thay thế / Ngoại lệ** | **STT \| Thực hiện bởi \| Hành động** <br>**[ERR-SCAN-01] Sai định dạng hoặc file quá nặng:** <br>3a. File tải lên không phải PDF/PNG/JPG hoặc dung lượng > 25MB -> Hệ thống báo lỗi và từ chối nhận file. <br>**[ERR-SCAN-02] Chưa tải file đã bấm hoàn tất:** <br>5a. Thư ký/CCV bấm hoàn tất khi chưa có file đính kèm -> Hệ thống báo lỗi đỏ: "Bắt buộc phải tải file scan bản cứng dấu đỏ để tiếp tục quy trình", khóa nút gửi. |
| **Hậu điều kiện** | Hồ sơ số hóa được lưu trữ thành công; hồ sơ được mở chặn để Thư ký/CCV thu phí dịch vụ. |

##### Bảng dữ liệu đầu vào của Use Case UC008:
| STT | Trường dữ liệu | Mô tả | Bắt buộc? | Điều kiện hợp lệ | Ví dụ |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | File tài liệu scan | File chụp hoặc scan của tài liệu có con dấu đỏ của CCV | Có | Định dạng PDF, PNG, JPG; dung lượng < 25MB | signed_dossier_0918.pdf |

---

<a id="2.6.3-nhom-use-case-tai-chinh-cham-soc"></a>
#### 2.6.3 Nhóm Use Case Tài chính & Chăm sóc (Billing & CRM)

##### UC009: Thu phí dịch vụ
| Đặc tả Use Case | Chi tiết |
| :--- | :--- |
| **Mã Use Case** | UC009 |
| **Tên Use Case** | Thu phí dịch vụ |
| **Tác nhân** | Thư ký nghiệp vụ, Công chứng viên |
| **Mô tả** | Thư ký nghiệp vụ hoặc Công chứng viên tiếp nhận thanh toán từ khách hàng tại quầy, thực hiện xác nhận nhận tiền thực thu và ghi nhận giao dịch thu phí lên hệ thống. |
| **Sự kiện kích hoạt** | Thư ký hoặc CCV chọn một hồ sơ trong danh sách "Chờ thu phí" trên giao diện nghiệp vụ tại quầy. |
| **Tiền điều kiện** | Hồ sơ đã được Thư ký upload file scan dấu đỏ vật lý thành công (UC008). |
| **Luồng sự kiện chính (Thành công)** | **STT \| Thực hiện bởi \| Hành động** <br>1. Thư ký / CCV \| Kiểm tra thông tin phí cần thu của hồ sơ. <br>2. Thư ký / CCV \| Chọn phương thức thanh toán thực tế của khách hàng (Tiền mặt, Chuyển khoản ngân hàng, Quẹt thẻ POS). <br>3. Thư ký / CCV \| Nhấn nút "Xác nhận nhận đủ tiền". <br>4. Hệ thống \| Ghi nhận giao dịch thu phí của hồ sơ và chuyển trạng thái hồ sơ sang "Chờ đối soát". |
| **Luồng sự kiện thay thế / Ngoại lệ** | **STT \| Thực hiện bởi \| Hành động** <br>**[ERR-PAY-01] Thiếu file scan dấu đỏ:** <br>1a. Hệ thống phát hiện hồ sơ chưa có file scan dấu đỏ -> Khóa nút xác nhận thanh toán và báo lỗi: "Hồ sơ chưa có file scan dấu đỏ, không thể thu tiền". |
| **Hậu điều kiện** | Giao dịch thu phí được ghi nhận tạm thời; hồ sơ chuyển sang trạng thái chờ đối soát dòng tiền của Kế toán. |

##### Bảng dữ liệu đầu vào của Use Case UC009:
| STT | Trường dữ liệu | Mô tả | Bắt buộc? | Điều kiện hợp lệ | Ví dụ |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Phương thức thanh toán | Hình thức thanh toán của khách | Có | Thuộc danh mục (Cash, Bank Transfer, POS) | Bank Transfer |
| 2 | Xác nhận nhận tiền | Trạng thái thu phí tại quầy | Có | Click chọn nút xác nhận thu phí | True |

---

##### UC010: Đối soát & Xuất hóa đơn điện tử tự động (VNPT/Vĩnh Hy)
| Đặc tả Use Case | Chi tiết |
| :--- | :--- |
| **Mã Use Case** | UC010 |
| **Tên Use Case** | Đối soát & Xuất hóa đơn điện tử tự động (VNPT/Vĩnh Hy) |
| **Tác nhân** | Kế toán, Hệ thống tự động |
| **Mô tả** | Kế toán thực hiện đối soát dòng tiền thực nhận (đối chiếu két tiền mặt hoặc tài khoản ngân hàng thực tế) với giao dịch hệ thống, sau đó bấm xác nhận đối soát để ghi nhận sổ cái bất biến và gọi API VNPT/Vĩnh Hy phát hành hóa đơn điện tử VAT tương ứng cho khách hàng. |
| **Sự kiện kích hoạt** | Kế toán chọn một hồ sơ trong danh sách "Chờ đối soát" trên Dashboard kế toán. |
| **Tiền điều kiện** | Giao dịch thu phí của hồ sơ đã được Thư ký hoặc CCV xác nhận nhận tiền thành công (UC009). |
| **Luồng sự kiện chính (Thành công)** | **STT \| Thực hiện bởi \| Hành động** <br>1. Kế toán \| Kiểm tra phương thức thanh toán và số tiền thực thu, đối chiếu với nguồn dòng tiền thực tế (tài khoản ngân hàng/két tiền mặt). <br>2. Kế toán \| Nhấn nút "Xác nhận đối soát & Xuất hóa đơn". <br>3. Hệ thống \| Ghi bản ghi giao dịch tài chính bất biến vào Sổ cái tài chính (không cho phép sửa/xóa). <br>4. Hệ thống \| Tự động bóc tách dòng tiền: Phí gốc nhà nước (miễn thuế) và Thù lao dịch vụ khác (đã tính thuế VAT). <br>5. Hệ thống \| Gọi API nhà cung cấp hóa đơn điện tử (VNPT/Vĩnh Hy), truyền các thông tin hóa đơn và định danh khách hàng. <br>6. Hệ thống \| Nhận phản hồi thành công từ API chứa Số hóa đơn chính thức và link tải file hóa đơn (PDF/XML). <br>7. Hệ thống \| Ghi nhận Số hóa đơn và URL file hóa đơn vào sổ cái tài chính. <br>8. Hệ thống \| Đổi trạng thái hồ sơ sang "Đã hoàn tất". <br>9. Hệ thống \| Tự động kích hoạt gọi API Zalo OA để gửi thông báo cho khách hàng (UC011). |
| **Luồng sự kiện thay thế / Ngoại lệ** | **STT \| Thực hiện bởi \| Hành động** <br>**[ERR-INV-01] API hóa đơn mất kết nối / Timeout:** <br>5a. API hóa đơn gặp lỗi -> Hệ thống tự động chuyển giao dịch hóa đơn vào hàng đợi xử lý ngầm (Offline Queue). <br>5b. Hệ thống tạo và cho phép Kế toán/Thư ký in **Biên lai tạm thời** chứa mã QR tra cứu tạm cho khách. <br>5c. Tiến trình cron job chạy ngầm tự động thực hiện lệnh gọi lại (retry) phát hành hóa đơn điện tử khi API hóa đơn trực tuyến hoạt động lại bình thường. <br>**[Luồng phụ 1] Tự động tách hóa đơn khi vượt trần:** <br>4a. Hệ thống phát hiện phí gốc vượt trần $200.000đ$ -> Tự động chia nhỏ thành các yêu cầu gọi xuất hóa đơn con độc lập có giá trị phí gốc mỗi hóa đơn $\le 200.000đ$. |
| **Hậu điều kiện** | Hóa đơn điện tử phát hành thành công hoặc được đưa vào hàng đợi xử lý offline; hồ sơ đổi thành trạng thái "Đã hoàn tất". |

##### Bảng dữ liệu đầu vào của Use Case UC010:
| STT | Trường dữ liệu | Mô tả | Bắt buộc? | Điều kiện hợp lệ | Ví dụ |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | E-Invoice API Response | Phản hồi từ nhà cung cấp hóa đơn điện tử | Có (Tự động) | Định dạng JSON hợp lệ chứa Số hóa đơn và Link PDF | `{ "invoiceNo": "VNPT-2026-0012", "pdfUrl": "..." }` |

---

##### UC011: Chăm sóc khách hàng tự động qua Zalo OA
| Đặc tả Use Case | Chi tiết |
| :--- | :--- |
| **Mã Use Case** | UC011 |
| **Tên Use Case** | Chăm sóc khách hàng tự động qua Zalo OA |
| **Tác nhân** | Hệ thống tự động |
| **Mô tả** | Hệ thống tự động gửi tin nhắn ZNS qua Zalo OA của VPCC để gửi lời cảm ơn và đường dẫn tải hóa đơn điện tử cho khách hàng. |
| **Sự kiện kích hoạt** | Trạng thái hồ sơ chuyển sang "Đã hoàn tất" sau khi phát hành hóa đơn (UC010). |
| **Tiền điều kiện** | Hóa đơn điện tử đã được cấp số hóa đơn và link tải PDF thành công. |
| **Luồng sự kiện chính (Thành công)** | **STT \| Thực hiện bởi \| Hành động** <br>1. Hệ thống \| Lấy số điện thoại định danh khách hàng, tên khách hàng và link hóa đơn điện tử PDF. <br>2. Hệ thống \| Gọi API Zalo OA (Zalo Notification Service - ZNS) truyền thông tin tin nhắn. <br>3. Hệ thống \| Nhận phản hồi gửi thành công từ Zalo. <br>4. Hệ thống \| Ghi nhận timestamp gửi tin nhắn thành công vào lịch sử hồ sơ. |
| **Luồng sự kiện thay thế / Ngoại lệ** | **STT \| Thực hiện bởi \| Hành động** <br>**[ERR-ZAL-01] Khách hàng không đăng ký Zalo:** <br>3a. API Zalo OA báo lỗi số điện thoại không đăng ký Zalo -> Hệ thống tự động kích hoạt cổng fallback gửi tin nhắn SMS truyền thống chứa nội dung tương tự. |
| **Hậu điều kiện** | Tin nhắn cảm ơn kèm đường dẫn hóa đơn được gửi thành công tới số điện thoại khách hàng. |

##### Bảng dữ liệu đầu vào của Use Case UC011:
| STT | Trường dữ liệu | Mô tả | Bắt buộc? | Điều kiện hợp lệ | Ví dụ |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Zalo API Response | Phản hồi kết quả gửi tin từ Zalo | Có (Tự động) | JSON phản hồi thành công | `{ "status": "success", "msgId": "msg-091" }` |

---

<a id="3-cac-kich-ban-nghiep-vu-thuc-te"></a>
## Chương 3. Các kịch bản nghiệp vụ thực tế (Real-world Cases)

<a id="3.1-nghiep-vu-sao-y-ban-chinh"></a>
### 3.1 Nghiệp vụ Sao y bản chính

Dưới đây là các kịch bản nghiệp vụ thực tế của phân hệ **Sao y bản chính** thường gặp trong vận hành hàng ngày của Văn phòng công chứng, nhằm cụ thể hóa các Use Case chung đã nêu trên:

<a id="3.1.1-case-1-sao-y-cccd"></a>
#### 3.1.1 Case 1: Sao y CCCD / Giấy tờ tùy thân của cá nhân tại quầy (Siêu tốc)
- **Bối cảnh:** Anh A đến văn phòng yêu cầu sao y 3 bản CCCD lấy ngay.
- **Hành vi thực tế:** Anh A đưa bản gốc CCCD. Thư ký quét nhanh SĐT của anh A.
- **Luồng xử lý trên hệ thống:**
  - Thư ký nhập SĐT -> Hệ thống tìm thấy thông tin anh A và tự động điền (Auto-fill) Họ tên, CCCD, Địa chỉ.
  - Thư ký chọn loại giấy tờ: **CCCD (Chip-based)**, hệ thống ghi nhận số trang gốc mặc định là 2 (tương ứng với 2 mặt trước và sau của thẻ). Số bản sao y mặc định ban đầu là 1, thư ký điều chỉnh lại thành 3 bản theo yêu cầu của khách.
  - Thư ký điền số bản cần sao y: 3 bản.
  - Hệ thống tính Phí Gốc nhà nước: $2 \text{ trang} \times 3 \text{ bản} \times 2.000đ = 12.000đ$.
  - Thư ký báo phí trọn gói dịch vụ cho khách là $20.000đ$ và nhập số tiền này vào ô "Tổng thực thu".
  - Hệ thống tự động hạch toán phần chênh lệch $8.000đ$ vào mục "Thù lao dịch vụ khác" (phí photo, bìa hồ sơ).
  - Thư ký tích chọn `Khách hàng đồng ý báo phí` và nhấn "Lưu & Chuyển xử lý".
  - Thư ký nhận tài liệu, photo bản sao, thực hiện đối khớp ảnh chân dung, kiểm tra hạn dùng CCCD và khớp mặt trước/sau. Thư ký in lời chứng tự động, trình CCV ký đóng dấu bản cứng offline.
  - Thư ký scan bản cứng đã ký đóng dấu tải lên hệ thống. Hệ thống tự động chuyển hồ sơ sang trạng thái Chờ thu phí.
  - Thư ký nhận tiền mặt $20.000đ$ tại quầy và bấm xác nhận thu phí trên hệ thống. Kế toán thực hiện đối soát tài chính, hệ thống tự động gọi API VNPT xuất hóa đơn điện tử gửi Zalo OA cho anh A.

<a id="3.1.2-case-2-sao-y-so-do"></a>
#### 3.1.2 Case 2: Sao y Sổ đỏ / Giấy tờ sở hữu tài sản có kiểm tra ngăn chặn (UCHI)
- **Bối cảnh:** Chị B mang bản gốc Sổ đỏ đến sao y 2 bản để làm hồ sơ vay vốn thế chấp ngân hàng.
- **Hành vi thực tế:** Tài sản liên quan đến đất đai có rủi ro giả mạo và ngăn chặn giao dịch cao.
- **Luồng xử lý trên hệ thống:**
  - Thư ký tiếp nhận, nhập SĐT chị B, chọn loại giấy tờ: **Sổ đỏ / Giấy chứng nhận quyền sử dụng đất** (4 trang, 2 bản).
  - Phí Gốc: $4 \text{ trang} \times 2 \text{ bản} \times 2.000đ = 16.000đ$. Thực thu thỏa thuận: $50.000đ$ (chênh lệch $34.000đ$ phí thù lao dịch vụ và phí tra cứu ngăn chặn).
  - Chuyển hồ sơ sang bước Thẩm định. **Thư ký bắt buộc phải click vào liên kết "UCHI Search" trên màn hình** để gọi API tra cứu trạng thái ngăn chặn của thửa đất trên CSDL UCHI của Sở Tư pháp.
  - *Nhánh rẽ 1 (Hợp lệ):* CSDL trả về trạng thái "Bình thường". Thư ký tích chọn checklist (UCHI kiểm tra sạch, đối khớp chủ sở hữu, không tẩy xóa), in Lời chứng trình CCV ký đóng dấu vật lý. Thư ký scan bản cứng có dấu đỏ tải lên hệ thống để mở chặn thanh toán.
  - *Nhánh rẽ 2 (Ngăn chặn):* CSDL trả về trạng thái "Đang bị ngăn chặn giao dịch" (do tranh chấp hoặc kê biên). Hệ thống lập tức khóa nút in lời chứng, hiển thị cảnh báo đỏ nổi bật, tự động ghi nhận lỗi ngăn chặn vào log và Thư ký thực hiện trả lại hồ sơ cho khách.

<a id="3.1.3-case-3-sao-y-so-luong-lon"></a>
#### 3.1.3 Case 3: Sao y số lượng lớn (Vượt trần quy định) & Tự động tách hóa đơn
- **Bối cảnh:** Công ty X mang 5 bộ hồ sơ thầu (mỗi bộ 250 trang) đến sao y bản chính. Tổng số trang sao y: 1250 trang.
- **Hành vi thực tế:** Theo luật Phí và Lệ phí, phí sao y/chứng thực bản sao tối đa không quá $200.000đ/\text{lần yêu cầu}$ (hoặc theo mức trần quy định của địa phương). Nếu xuất một hóa đơn phí gốc 1250 trang x 2.000đ = 2.500.000đ sẽ vi phạm quy định pháp lý về phí lệ phí.
- **Luồng xử lý trên hệ thống:**
  - Thư ký nhập số trang 250, số bản 5. Phí tính toán ban đầu là $2.500.000đ$.
  - Hệ thống phát hiện số tiền vượt mức trần $200.000đ$ cho một giao dịch độc lập.
  - Khi Thư ký nhấn "Lưu", hệ thống tự động tách hồ sơ thầu thành 13 bản ghi giao dịch (transaction records) con độc lập trên hệ thống (mỗi bản ghi tối đa 100 trang sao y trị giá $200.000đ$ hoặc tương đương) để khi kế toán xuất hóa đơn điện tử, hóa đơn sẽ tự động được phân tách thành 13 hóa đơn hợp lệ có giá trị mỗi hóa đơn $\le 200.000đ$, đảm bảo tuân thủ 100% quy định pháp luật thuế và phí lệ phí.

<a id="3.1.4-case-4-doanh-nghiep-sao-y-giay-phep"></a>
#### 3.1.4 Case 4: Doanh nghiệp sao y giấy phép & Yêu cầu hóa đơn VAT (B2B)
- **Bối cảnh:** Đại diện Công ty X đến sao y Giấy đăng ký kinh doanh và Giấy phép môi trường, yêu cầu xuất hóa đơn điện tử B2B gửi về email doanh nghiệp để làm báo cáo thuế.
- **Hành vi thực tế:** Cần thông tin chính xác của doanh nghiệp (Mã số thuế, Tên doanh nghiệp, Địa chỉ trụ sở chính) và đối chiếu tính hiệu lực hoạt động của pháp nhân.
- **Luồng xử lý trên hệ thống:**
  - Thư ký tạo hồ sơ, tích chọn toggle `Xuất hóa đơn doanh nghiệp (B2B)`.
  - Thư ký nhập Mã số thuế: `0314456789`. Hệ thống gọi API Tổng cục Thuế, tự động điền Tên công ty: "Công ty Cổ phần Đầu tư X" và địa chỉ trụ sở chính vào hóa đơn.
  - Thư ký nhận việc, thực hiện checklist nghiệp vụ doanh nghiệp: Truy vấn nhanh trên Cổng thông tin Quốc gia về Đăng ký Doanh nghiệp xem Công ty X có đang hoạt động bình thường hay đã giải thể/ngừng hoạt động.
  - Thư ký đối khớp con dấu doanh nghiệp trên bản chính, in Lời chứng trình CCV ký offline. Scan tải lên hệ thống.
  - Kế toán chọn thanh toán bằng "Chuyển khoản ngân hàng", đối soát tiền về tài khoản VPCC, bấm "Xác nhận & Phát hành".
  - Hệ thống gọi API VNPT xuất hóa đơn điện tử, đồng thời tự động gửi email chứa hóa đơn XML/PDF và tin nhắn Zalo OA cảm ơn đến số điện thoại của người đại diện công ty.

<a id="3.1.5-case-5-sao-y-giay-to-nuoc-ngoai"></a>
#### 3.1.5 Case 5: Sao y giấy tờ có yếu tố nước ngoài (Yêu cầu Hợp pháp hóa lãnh sự)
- **Bối cảnh:** Ông C mang bằng đại học do trường nước ngoài cấp bằng tiếng Anh đến sao y.
- **Hành vi thực tế:** Giấy tờ do cơ quan/tổ chức nước ngoài cấp phải được hợp pháp hóa lãnh sự trước khi chứng thực sao y bản chính tại Việt Nam (trừ trường hợp được miễn trừ theo điều ước quốc tế).
- **Luồng xử lý trên hệ thống:**
  - Thư ký tạo hồ sơ, chọn loại giấy tờ: **Giấy tờ nước ngoài / Song ngữ**.
  - Hệ thống tự động kích hoạt checklist động dành riêng cho tài liệu nước ngoài, bao gồm mục kiểm tra bắt buộc: `Đã kiểm tra tem và con dấu Hợp pháp hóa lãnh sự của Bộ Ngoại giao Việt Nam`.
  - Thư ký tiếp nhận tài liệu, đối chiếu bản chính. Nếu bản chính chưa có tem hợp pháp hóa lãnh sự và không thuộc diện miễn trừ:
    - Thư ký tích chọn "Không đủ điều kiện" -> Hệ thống tự động khóa tính năng in Lời chứng.
    - Thư ký bấm "Từ chối tiếp nhận" -> Hệ thống hiển thị popup cho phép chọn in "Phiếu hướng dẫn hoàn thiện hồ sơ" (trong đó ghi rõ yêu cầu hợp pháp hóa lãnh sự trước khi sao y) để gửi cho khách hàng.
  - Nếu bản chính đã được hợp pháp hóa lãnh sự hợp lệ: Thư ký tích chọn hoàn thành checklist, in Lời chứng trình CCV ký, chụp/scan tài liệu tải lên hệ thống để chuyển thanh toán bình thường.

<a id="3.1.6-case-6-tu-choi-sao-y"></a>
#### 3.1.6 Case 6: Từ chối sao y các giấy tờ bị cấm chứng thực (Tẩy xóa, đóng dấu MẬT, rách nát)
- **Bối cảnh:** Bà D mang một quyết định hành chính có đóng dấu "MẬT" hoặc một học bạ bị tẩy xóa điểm số, rách nát mất chữ đến yêu cầu sao y.
- **Hành vi thực tế:** Tuân thủ Điều 22 Nghị định 23/2015/NĐ-CP, cấm chứng thực bản sao từ bản chính đối với giấy tờ bị tẩy xóa, sửa chữa, rách nát hư hỏng không xác định được nội dung, hoặc có đóng dấu mật/cấm sao chụp.
- **Luồng xử lý trên hệ thống:**
  - Thư ký tiếp nhận và kiểm tra bản gốc tài liệu của bà D, phát hiện tài liệu bị tẩy xóa hoặc đóng dấu "MẬT".
  - Thư ký truy cập hồ sơ trên hệ thống, bấm nút **Từ chối hồ sơ**.
  - Hệ thống hiển thị form yêu cầu chọn lý do từ chối luật định:
    1. Bản chính bị tẩy xóa, sửa chữa, thêm, bớt nội dung không hợp lệ.
    2. Bản chính bị hư hỏng, rách nát, không xác định được nội dung.
    3. Bản chính đóng dấu mật hoặc ghi rõ không được sao chụp.
    4. Bản chính có nội dung trái pháp luật, đạo đức xã hội.
    5. Lý do khác (cho phép nhập tay).
  - Thư ký chọn lý do tương ứng (ví dụ: "Bản chính đóng dấu mật").
  - Hệ thống ghi nhận trạng thái hồ sơ là **Đã hủy (Từ chối nghiệp vụ)**, tự động lưu nhật ký hệ thống (Audit Log) chứa thông tin Thư ký từ chối, lý do từ chối và timestamp.
  - Hệ thống hỗ trợ in **Phiếu từ chối chứng thực** tự động chứa căn cứ pháp lý của Điều 22 Nghị định 23/2015/NĐ-CP để gửi cho khách hàng.
