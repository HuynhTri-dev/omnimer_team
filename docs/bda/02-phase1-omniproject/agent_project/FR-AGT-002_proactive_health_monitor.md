# Feature: Proactive Health Monitor (FR-AGT-002)

**Mô tả:** AI tự động quét rủi ro dự án.

## 1. Đặc tả Kỹ thuật (FRD)

### 1.1 Business Logic & Thuật toán
*   **BL-AGT-002.1 (Risk Detection Rule):** Hệ thống chạy Cron Job mỗi 4 giờ quét toàn bộ Task `Status != Done`. Nếu `DueDate - CurrentDate < 48h` VÀ Task vẫn nằm ở cột đầu tiên (To Do / Backlog) $\rightarrow$ Đẩy cảnh báo qua Telegram DM cho Assignee.
*   **BL-AGT-002.2 (Standup Aggregation):** 18:00 hàng ngày, AI tóm tắt: "Hôm nay Team đã Done X tasks, Đang làm Y tasks, Bị Block Z tasks" và gửi vào Group Telegram của Project.

*(Lưu ý: Tính năng này chưa có Acceptance Criteria chi tiết trong tài liệu hiện tại).*
