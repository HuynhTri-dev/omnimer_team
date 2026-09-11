# Feature: Scrum & Sprint Management (FR-PRJ-009)

**Mô tả:** Quản lý vòng đời phát triển theo mô hình Scrum (Agile), chia dự án thành các vòng lặp (Sprint) ngắn hạn.
**Priority:** P1 (High)

## 1. Đặc tả Kỹ thuật (FRD)

### 1.1 Data Contract (Sprint Schema)

```jsonc
{
  "sprint_id": "uuid",
  "project_id": "uuid",
  "name": "string",
  "goal": "string",
  "start_date": "ISO8601",
  "end_date": "ISO8601",
  "status": "string" // Enum: "PLANNED", "ACTIVE", "CLOSED"
}
```
*(Trong Schema của Task ở FR-PRJ-001 cần bổ sung thêm trường `sprint_id`)*

### 1.2 Business Logic & Rules

* **BL-PRJ-009.1 (Active Sprint Constraint):** Tại một thời điểm trong một dự án, chỉ có tối đa **1 Sprint** được phép ở trạng thái `ACTIVE`. Nếu PM bấm "Start Sprint" khi đang có một Sprint khác `ACTIVE`, API trả về `HTTP 409 Conflict`.
* **BL-PRJ-009.2 (Task & Sprint Relationship):** Một Task chỉ có thể nằm trong 1 Sprint. Nếu kéo Task từ Backlog vào Sprint A, `sprint_id` của Task cập nhật thành ID của Sprint A.
* **BL-PRJ-009.3 (Closed Sprint Immutability):** Nếu Sprint chuyển sang trạng thái `CLOSED`, toàn bộ metadata của Sprint đó bị khóa. Không ai được phép kéo Task mới vào Sprint đã Closed.
* **BL-PRJ-009.4 (Unfinished Tasks Rollover):** Khi đóng một `ACTIVE` Sprint, hệ thống sẽ gom tất cả các Task có trạng thái khác `Done`, bật Popup hỏi PM: "Chuyển các task chưa xong này về Backlog, hay đẩy sang Sprint kế tiếp?".

---

## 2. Tiêu chí Chấp nhận (Acceptance Criteria)

**Là** Scrum Master,
**Tôi muốn** gom các Task từ Backlog vào một Sprint và nhấn Start,
**Để** team tập trung giải quyết khối lượng công việc đó trong 2 tuần mà không bị phân tâm.

**Acceptance Criteria (Gherkin):**
```gherkin
Given Dự án đang có Sprint 1 ở trạng thái ACTIVE
When Tôi bấm "Start Sprint" cho Sprint 2
Then Hệ thống báo lỗi "Bạn phải hoàn thành Sprint 1 trước khi bắt đầu Sprint 2"
```

```gherkin
Given Tôi đang đóng Sprint 1 nhưng còn 2 Tasks chưa hoàn thành
When Tôi nhấn nút "Complete Sprint"
Then Popup xuất hiện yêu cầu tôi chọn nơi chứa 2 Tasks chưa hoàn thành này (Backlog hoặc New Sprint)
And Sau khi xác nhận, Sprint 1 chuyển sang CLOSED và không thể thay đổi nữa
```
