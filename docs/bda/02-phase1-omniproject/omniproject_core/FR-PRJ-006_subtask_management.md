# Feature: Subtask Management (FR-PRJ-006)

**Mô tả:** Khả năng chia nhỏ một công việc lớn thành nhiều công việc nhỏ (Subtasks) và theo dõi tiến độ tổng thể.

## 1. Đặc tả Kỹ thuật (FRD)

### 1.1 Business Logic & Rules
* **BL-PRJ-006.1 (Progress Roll-up):** Trạng thái hoàn thành của Task cha được tự động tính bằng phần trăm (%) số Subtask ở trạng thái `Done` chia cho tổng số Subtasks.
* **BL-PRJ-006.2 (Hierarchy Depth):** Để tránh phức tạp hóa vòng đời, chỉ cho phép tạo Subtask tối đa 1 cấp độ (Child task), không cho phép tạo Sub-subtask.

---

## 2. Tiêu chí Chấp nhận (Acceptance Criteria)

**Là** Developer,
**Tôi muốn** tạo các Subtask bên trong một Task lớn,
**Để** chia nhỏ công việc và dễ dàng theo dõi tiến độ từng phần.

**Acceptance Criteria (Gherkin):**
```gherkin
Given Task "Làm tính năng Login" đang có 4 Subtasks
When tôi check hoàn thành 2 Subtasks
Then thanh tiến độ (Progress bar) của Task cha tự động hiển thị "50%"
```
