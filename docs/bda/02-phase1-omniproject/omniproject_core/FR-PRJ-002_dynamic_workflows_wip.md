# Feature: Dynamic Workflows & WIP Limits (FR-PRJ-002)

**Mô tả:** Định nghĩa luồng trạng thái tùy chỉnh cho dự án và kiểm soát khối lượng công việc đang xử lý (Work In Progress).

## 1. Đặc tả Kỹ thuật (FRD)

### 1.1 Business Logic & Rules

* **BL-PRJ-002.1 (WIP Block):** Nếu cột "In Progress" có giới hạn WIP = 3, khi kéo Task thứ 4 vào, UI hiển thị màu Đỏ cảnh báo.
* **BL-PRJ-002.2 (Override Privilege):** Chỉ PM (Project Manager) mới có quyền xác nhận "Override WIP Limit" (Vượt rào). Nếu member kéo thả, hệ thống ném HTTP 403 Forbidden kèm message.

*(Lưu ý: Tính năng này chưa có Acceptance Criteria chi tiết trong tài liệu hiện tại).*
