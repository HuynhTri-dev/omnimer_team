# OmniMer Enterprise PMIS - Business Data Analysis (BDA)

Chào mừng bạn đến với tài liệu phân tích nghiệp vụ (BDA) của dự án **OmniMer Enterprise PMIS**. Hệ thống tài liệu ở đây được tổ chức theo từng giai đoạn (Phase) để giúp team dễ dàng theo dõi từ yêu cầu nghiệp vụ tổng quan đến đặc tả chức năng chi tiết.

## 🧭 Triết lý cốt lõi
Hệ thống OmniMer được xây dựng dựa trên nguyên tắc **Chống "Vibe Coding"**, quản trị bằng truy vết (Traceability) và Quản lý bằng ngoại lệ (Management by Exception). Mục tiêu là mọi thành viên từ Dev, QA đến Lãnh đạo đều hiểu rõ mục đích của từng dòng code và tình trạng sức khỏe của dự án.

---

## 📂 Cấu trúc Tài liệu

Tài liệu được chia thành các thư mục sau để bạn dễ dàng tìm kiếm:

### [01. Bối cảnh Kinh doanh & Tầm nhìn](./01-business-context/)
Bắt đầu đọc ở đây nếu bạn mới tham gia dự án.
- **[BRD (Business Requirements Document)](./01-business-context/1-BRD.md)**: Định nghĩa các vấn đề kinh doanh và mục tiêu chiến lược.
- **[Vision & Scope](./01-business-context/2-VISION_AND_SCOPE.md)**: Tầm nhìn sản phẩm và phạm vi của từng Phase.
- **[Sơ đồ Use Case Tổng quan](./01_global_use_case_diagram.md)**: Bức tranh toàn cảnh về cách các Actor tương tác với hệ thống.

---

### [02. Phase 1: OmniProject & OmniChannel](./02-phase1-omniproject/PHASE1_OMNIPROJECT_MERGED.md)
*Giai đoạn nền tảng: Thực thi dự án và hợp nhất giao tiếp.*
- Quản lý Board linh hoạt (Kanban, Scrum, Gantt).
- Dependency & Critical Path.
- Tích hợp Zalo/Telegram (Unified Inbox).
- Trợ lý AI OPAgent (Text/Voice-to-Task).
- **Tài liệu gộp**: Chứa Đặc tả Yêu cầu Chức năng (FRD), Tiêu chí Chấp nhận (AC), và Sơ đồ Trình tự (Sequence Diagram).

---

### [03. Phase 2: Control & Analytics](./03-phase2-control-analytics/PHASE2_CONTROL_ANALYTICS_MERGED.md)
*Giai đoạn kiểm soát: Nguồn lực, KPI và Tài chính.*
- Động cơ chấm điểm KPI tự động, chống gian lận.
- Cảnh báo quá tải (Overload) và điểm nghẽn (Bus Factor).
- Dashboard EVM (Earned Value Management).
- Đồng bộ dữ liệu sang HRM/Payroll.
- **Tài liệu gộp**: Chứa FRD, AC, và Sơ đồ Trình tự.

---

### [04. Phase 3: Governance & Traceability](./04-phase3-governance/PHASE3_GOVERNANCE_MERGED.md)
*Giai đoạn quản trị: Chống lạm phát phạm vi (Scope Creep) và kiểm soát chất lượng.*
- Hệ thống truy vết vạn vật (End-to-End Traceability).
- Cổng bàn giao bắt buộc (Mandatory Handover Gates).
- Hội đồng Kiểm soát Thay đổi (Change Control Board - CCB).
- **Tài liệu gộp**: Chứa FRD, AC, và Sơ đồ Trình tự.

---

### [05. Ma trận Truy vết (Traceability)](./05-traceability/)
- **[RTM.csv](./05-traceability/RTM.csv)**: File theo dõi sự liên kết từ Mục tiêu kinh doanh (Objective) xuống tận Use Story và Test Case.

---

## 🛠 Hướng dẫn cho Developer & QA
1. **Tuyệt đối tuân thủ**: Các file FRD là hợp đồng bắt buộc. Nếu phát hiện thiếu sót (Edge Cases), hãy yêu cầu BA cập nhật tài liệu trước, không tự ý code theo cảm tính.
2. **Cách đọc**: Khi được giao làm một tính năng thuộc Phase 1, bạn chỉ cần vào thư mục `02-phase1-omniproject/` và đọc file duy nhất trong đó. Mọi logic, luật business, và tiêu chí nghiệm thu (AC) đều nằm chung một chỗ.
