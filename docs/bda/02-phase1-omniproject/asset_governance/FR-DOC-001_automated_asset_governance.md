# Feature: Automated Asset Governance (FR-DOC-001)

**Mô tả:** Hệ thống Kho Tri thức (Knowledge Base) tự động phân loại, gắn thẻ và lưu trữ các tài liệu đầu ra từ Task để phục vụ đào tạo (Training), bảo trì (Maintenance) và chuyển giao (Onboarding) cho nhân viên mới.
**Priority:** P1 (High)

## 1. Đặc tả Kỹ thuật (FRD)

### 1.1 Data Contract (Asset Document Schema)

```jsonc
{
  "asset_id": "uuid",
  "project_id": "uuid",
  "source_task_id": "uuid",
  "author_id": "uuid",       // Người nộp tài liệu (Assignee của Task)
  "asset_type": "string",    // Phân loại: CODE_PR, DESIGN_FIGMA, FRD_DOC, SPREADSHEET, IMAGE
  "url": "string",           // S3 Link hoặc External URL
  "created_at": "ISO8601"
}
```

### 1.2 Business Logic & Rules

* **BL-DOC-001.1 (Auto-Tagging Pipeline):** Khi nhận event `TaskDone_WithOutput` từ OmniProject Core, hệ thống tự động bóc tách thông tin: Tên Project, ID người làm (Author), Ngày hoàn thành (Timestamp) để lưu metadata cho Asset mà không cần User nhập thủ công.
* **BL-DOC-001.2 (Asset Retrieval & Filtering):** Cung cấp giao diện tìm kiếm (Search UI) cho phép lọc tài liệu theo đa chiều. Ví dụ: "Tìm tất cả DESIGN_FIGMA do nhân viên A tạo trong năm 2026 thuộc Project B".
* **BL-DOC-001.3 (Onboarding Export):** PM có quyền gom nhiều Assets lại thành một "Onboarding Package" (Gói bàn giao) dưới dạng 1 link chia sẻ duy nhất để gửi cho nhân viên mới đọc hiểu hệ thống.

---

## 2. Tiêu chí Chấp nhận (Acceptance Criteria)

**Là** Project Manager / Admin,
**Tôi muốn** mọi tài liệu đầu ra của dự án được lưu trữ tập trung và tự động phân loại theo người làm và ngày tháng,
**Để** khi một nhân sự cứng nghỉ việc, tôi có sẵn trọn bộ tài liệu chi tiết (đã chống vibe code) để gửi cho nhân sự mới tự học (training).

**Acceptance Criteria (Gherkin):**
```gherkin
Given Nhân viên A vừa hoàn thành Task "Viết API Login" và nộp kèm link PR (Pull Request)
When Tôi vào màn hình "Knowledge Base" của Dự án
Then Hệ thống hiển thị 1 thẻ tài liệu mới với nhãn [Type: CODE_PR], [Author: Nhân viên A], [Time: Vừa xong]
And Khi tôi click vào thẻ đó, hệ thống trỏ thẳng đến link PR gốc
```
