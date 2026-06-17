# Tài liệu Đặc tả Yêu cầu Phần mềm (Software Requirements Specification - SRS)
## Hệ thống ERP/CRM Văn phòng Công chứng (NotaryOS)

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
    - [2.4.3 Phân rã nhóm chức năng Tài chính & Xuất hóa đơn (Billing & Invoice)](#243-phân-rã-nhóm-chức-năng-tài-chính--xuất-hóa-đơn-billing--invoice)
  - [2.5 Quy trình nghiệp vụ (Business Processes)](#25-quy-trình-nghiệp-vụ-business-processes)
    - [2.5.1 Sơ đồ luồng hoạt động nghiệp vụ tổng quát (Activity Diagram)](#251-sơ-đồ-luồng-hoạt-động-nghiệp-vụ-tổng-quát-activity-diagram)
    - [2.5.2 Luồng xử lý chi tiết theo phân hệ (Sub-system Workflows)](#252-luồng-xử-lý-chi-tết-theo-phân-hệ-sub-system-workflows)
  - [2.6 Đặc tả các usecase (Use Case Specifications)](#26-đặc-tả-các-usecase-use-case-specifications)
    - [2.6.1 Nhóm Use Case Xác thực & Hệ thống (Auth & Admin)](#261-nhóm-use-case-xác-thực--hệ-thống-auth--admin)
      - [UC001: Đăng nhập hệ thống](#uc001-đăng-nhập-hệ-thống)
      - [UC002: Thay đổi mật khẩu](#uc002-thay-đổi-mật-khẩu)
      - [UC003: Quản lý & Cấp tài khoản nhân sự](#uc003-quản-lý--cấp-tài-khoản-nhân-sự)
      - [UC004: Phân quyền & Thiết lập vai trò (RBAC)](#uc004-phân-quyền--thiết-lập-vai-trò-rbac)
    - [2.6.2 Nhóm Use Case Nghiệp vụ (Dossier & Checklist)](#262-nhóm-use-case-nghiệp-vụ-dossier--checklist)
      - [UC005: Tiếp nhận khách hàng & Khởi tạo hồ sơ](#uc005-tiếp-nhận-khách-hàng--khởi-tạo-hồ-sơ)
      - [UC006: Thẩm định hồ sơ & Duyệt Checklist chặn](#uc006-thẩm-định-hồ-sơ--duyệt-checklist-chặn)
      - [UC007: Trộn dữ liệu & Soạn thảo Lời chứng tự động](#uc007-trộn-dữ-liệu--soạn-thảo-lời-chứng-tự-động)
      - [UC008: Quét & Lưu trữ hồ sơ điện tử đã đóng dấu](#uc008-quét--lưu-trữ-hồ-sơ-điện-tử-đã-đóng-dấu)
    - [2.6.3 Nhóm Use Case Tài chính & Chăm sóc (Billing & CRM)](#263-nhóm-use-case-tài-chính--chăm-sóc-billing--crm)
      - [UC009: Thu phí & Đối soát dòng tiền](#uc009-thu-phí--đối-soát-dòng-tiền)
      - [UC010: Xuất hóa đơn điện tử tự động (VNPT/Vĩnh Hy)](#uc010-xuất-hoa-đơn-điện-tử-tự-động-vnptvĩnh-hy)
      - [UC011: Chăm sóc khách hàng tự động qua Zalo OA](#uc011-chăm-sóc-khách-hàng-tự-động-qua-zalo-oa)

- **[Chương 3. Các yêu cầu phi chức năng (Non-functional Requirements)](#chương-3-các-yêu-cầu-phi-chức-năng-non-functional-requirements)**
  - [3.1 Giao diện người dùng (User Interfaces)](#31-giao-diện-người-dùng-user-interfaces)
  - [3.2 Tính bảo mật (Security & Safety)](#32-tính-bảo-mật-security--safety)
  - [3.3 Ràng buộc (Constraints & Business Rules)](#33-ràng-buộc-constraints--business-rules)

- **[Phụ lục A: Sơ đồ Thực thể Dữ liệu Cốt lõi (ERD Analysis Model)](#phụ-lục-a-sơ-đồ-thực-thể-dữ-liệu-cốt-lõi-erd-analysis-model)**
- **[Phụ lục B: Danh sách các mục cần làm rõ (To Be Determined List - TBD)](#phụ-lục-b-danh-sách-các-mục-cần-làm-rõ-to-be-determined-list---tbd)**
