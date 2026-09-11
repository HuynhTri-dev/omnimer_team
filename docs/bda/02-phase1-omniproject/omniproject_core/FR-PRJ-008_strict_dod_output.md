# Feature: Strict Definition of Done (DoD) & Output Contract (FR-PRJ-008)

**Mô tả:** Cơ chế chống "Vibe Code" (làm bừa, không có tài liệu bàn giao). Yêu cầu Task phải nộp đúng định dạng tài liệu đầu ra trước khi được phép chuyển sang trạng thái "Done".
**Priority:** P1 (High)

## 1. Đặc tả Kỹ thuật (FRD)

### 1.1 Data Contract Enhancement (Bổ sung JSON Schema)

```jsonc
{
  "task_id": "uuid",
  // ... other fields
  "output_contract_type": "string", // Enum: "NONE", "URL_LINK", "FILE_UPLOAD", "MERGE_REQUEST"
  "output_deliverable": "string"    // Dữ liệu nộp (URL hoặc File ID)
}
```

### 1.2 Business Logic & Rules

* **BL-PRJ-008.1 (Output Definition):** Khi tạo Task, người giao việc (Owner/Reporter) có quyền bắt buộc định dạng đầu ra. Nếu thiết lập `output_contract_type != "NONE"`, hệ thống sẽ kích hoạt "Khóa Trạng thái".
* **BL-PRJ-008.2 (Done Blocker):** Nếu `assignee_id` kéo Task sang cột `Done` (hoặc chuyển Status = Done), hệ thống kiểm tra trường `output_deliverable`. Nếu trống, ném lỗi `HTTP 403` và popup Modal yêu cầu nộp tài liệu (Submit Deliverables) trên UI.
* **BL-PRJ-008.3 (Knowledge Base Sync):** Ngay sau khi Task được lưu trạng thái Done thành công, tài liệu trong `output_deliverable` sẽ được đẩy một bản sao (Event-Driven) sang phân hệ Asset Governance để lưu trữ dài hạn.

---

## 2. Tiêu chí Chấp nhận (Acceptance Criteria)

**Là** Project Manager,
**Tôi muốn** buộc nhân viên phải đính kèm link thiết kế / link PR code khi hoàn thành Task,
**Để** chống lại việc nhân viên click "Done" bừa bãi mà không lưu lại tài liệu bàn giao, gây khó khăn cho việc đào tạo nhân sự sau này.

**Acceptance Criteria (Gherkin):**
```gherkin
Given Task "Thiết kế Banner" có yêu cầu đầu ra là "FILE_UPLOAD"
When Nhân viên cố gắng kéo Task đó sang cột "Done" trên bảng Kanban
Then Hệ thống giữ Task ở lại vị trí cũ và hiển thị Popup "Yêu cầu nộp tài liệu đầu ra"
And Nhân viên tải lên file .Figma thành công
Then Hệ thống tự động chuyển Task sang cột "Done" và lưu file vào Kho Tri Thức
```
