# Feature: OPAgent NLP Text/Voice-to-Task (FR-AGT-001)

**Mô tả:** Phân tích câu lệnh bằng LLM để tự điền dữ liệu.

## 1. Đặc tả Kỹ thuật (FRD)

### 1.1 AI Extraction Schema (Output từ LLM)
LLM (GPT-4 / Claude) phải trả về chuẩn JSON Schema sau qua Function Calling / Structured Output:
```json
{
  "task_title": "string",
  "description": "string (markdown)",
  "assignee_name_hint": "string | null",
  "deadline_iso": "ISO8601 | null",
  "extracted_subtasks": ["string", "string"]
}
```

### 1.2 Business Logic & Rules
*   **BL-AGT-001.1 (Human-in-the-Loop):** Không bao giờ INSERT trực tiếp JSON từ AI vào Table Task. Phải lưu vào một bảng tạm `draft_tasks` và push WebSocket tới User để xác nhận (Accept/Edit/Reject).
*   **BL-AGT-001.2 (Assignee Resolution):** AI chỉ trả về `assignee_name_hint` (ví dụ: "Lan"). Backend dùng thuật toán Fuzzy Search hoặc Vector DB để map "Lan" với `user_id` thật trong Project. Nếu trùng nhiều tên (Lan Anh, Ngọc Lan), hiển thị Dropdown cho PM chọn.

---

## 2. Tiêu chí Chấp nhận (Acceptance Criteria)

**Là** Project Manager,
**Tôi muốn** gõ một câu lệnh tự nhiên (VD: "Giao Lan design banner trước thứ 6"),
**Để** OPAgent tự động tạo nháp Task với đầy đủ Assignee, Deadline, Title.

**Acceptance Criteria (Gherkin):**
```gherkin
Given tôi gõ "Giao Lan làm báo cáo SEO, deadline chiều thứ 6" vào thanh tạo task nhanh
When OPAgent (AI) xử lý xong
Then hệ thống hiện popup Confirm với các thông tin đã bóc tách:
   - Title: Làm báo cáo SEO
   - Assignee: Lan
   - Deadline: [Ngày thứ 6 tuần này lúc 17:00]
And tôi có thể chỉnh sửa lại trước khi nhấn "Tạo chính thức"
```
