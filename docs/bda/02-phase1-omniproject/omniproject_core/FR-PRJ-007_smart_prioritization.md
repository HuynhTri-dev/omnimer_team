# Feature: Smart Prioritization & Delegation Chain (FR-PRJ-007)

**Mô tả:** Hệ thống hỗ trợ giao việc phân cấp nhiều tầng (Delegation Chain) và tự động tính toán điểm ưu tiên (Action Score) dựa trên thuật toán Eisenhower thay vì nhãn thủ công (Low/Medium/High).
**Priority:** P1 (High)

## 1. Đặc tả Kỹ thuật (FRD)

### 1.1 Data Contract Enhancement (Bổ sung JSON Schema)

```jsonc
{
  "task_id": "uuid",
  "title": "string",
  "owner_id": "uuid",      // Người chịu trách nhiệm cuối cùng (ví dụ: Team Lead)
  "assignee_id": "uuid",   // Người trực tiếp thực thi (ví dụ: Staff)
  "importance": "integer", // Trọng số quan trọng (Từ 1 đến 10)
  "due_date": "ISO8601",
  "action_score": "float"  // Field tính toán tự động
}
```

### 1.2 Business Logic & Rules

* **BL-PRJ-007.1 (Delegation Accountability):** `owner_id` (Lead) có quyền giao việc cho `assignee_id` (Staff). Nếu Task trễ hạn, hệ thống tính lỗi (KPI Penalty) cho cả hai, nhưng `owner_id` chịu trách nhiệm báo cáo.
* **BL-PRJ-007.2 (Smart Action Score):** Điểm ưu tiên được hệ thống tính toán (hoặc recalculate mỗi ngày) bằng công thức: 
  $\text{Action Score} = \text{Importance} \times \left( \frac{1}{\text{Days to Deadline}} \right)$. 
  Task có Action Score càng cao thì càng nằm trên cùng của danh sách To-Do.
* **BL-PRJ-007.3 (Deadline Lock Anti-Gaming):** Chỉ người tạo Task (`reporter_id`) hoặc `owner_id` mới được phép chỉnh sửa `due_date`. `assignee_id` (Người thực thi) không có quyền tự lùi deadline để làm giảm Action Score.

---

## 2. Tiêu chí Chấp nhận (Acceptance Criteria)

**Là** Nhân viên (Staff),
**Tôi muốn** hệ thống tự động sắp xếp danh sách công việc mỗi sáng dựa trên độ gấp và độ quan trọng,
**Để** tôi biết chính xác việc gì cần làm trước mà không phải băn khoăn chọn lựa.

**Acceptance Criteria (Gherkin):**
```gherkin
Given tôi có 2 task: Task A (Quan trọng: 8, Deadline: 5 ngày nữa) và Task B (Quan trọng: 5, Deadline: 1 ngày nữa)
When tôi mở màn hình "My Work" vào buổi sáng
Then hệ thống tự động tính Action Score của Task B cao hơn Task A
And hiển thị Task B ở vị trí ưu tiên số 1
```

```gherkin
Given tôi là Assignee của một Task
When tôi cố gắng đổi ngày "Due Date" sang tuần sau
Then hệ thống chặn lại và hiển thị thông báo "Chỉ Owner hoặc Project Manager mới có quyền thay đổi Deadline"
```
