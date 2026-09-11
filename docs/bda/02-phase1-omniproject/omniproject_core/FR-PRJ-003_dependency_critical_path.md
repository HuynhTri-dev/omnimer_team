# Feature: Dependency & Critical Path (FR-PRJ-003)

**Mô tả:** Liên kết các Task (Finish-to-Start) và tự động tính toán Đường găng.

## 1. Đặc tả Kỹ thuật (FRD)

### 1.1 Business Logic & Thuật toán

* **BL-PRJ-003.1 (Auto-Scheduling Ripple Effect):** Khi Task A (Tiền nhiệm) đổi `end_date` sang `T+X` ngày, mọi Task phụ thuộc (B, C) chưa hoàn thành đều phải cộng thêm `X` ngày vào `start_date` và `end_date`.
  * *Tech Spec (Đệ quy):* Cập nhật này mang tính đệ quy (Recursive). Nếu B trễ, dẫn đến C trễ, dẫn đến D trễ. DB Trigger hoặc Background Worker phải duyệt qua toàn bộ Sub-graph từ node A để cập nhật hàng loạt.
* **BL-PRJ-003.2 (Critical Path Algorithm CPM):** Hệ thống tính toán đường dẫn dài nhất qua mạng lưới dự án. Task thuộc đường găng là Task có khoảng thời gian dự trữ (Total Float) = 0.

### 1.2 Edge Cases, Rủi ro Kỹ thuật & Hiệu năng

* **EC-02 (Circular Dependency - Vòng lặp phụ thuộc):**
  * *Kịch bản:* User nối A -> B -> C -> A.
  * *Xử lý:* API ném lỗi HTTP 409 Conflict. Backend sử dụng thuật toán dò chu trình (Cycle detection) trên đồ thị có hướng (DAG) trước khi lưu DB.
* **EC-03 (Deep Recursion Auto-Scheduling Limit):** 
  * *Kịch bản:* Thay đổi Task A gây ảnh hưởng lan truyền tới hơn 5,000 tasks phụ thuộc phía sau, gây khóa DB (Deadlock/Timeout).
  * *Xử lý:* Bất kỳ tác vụ Auto-scheduling nào ảnh hưởng > 50 tasks phải được đẩy xuống **Background Job / Queue** (ví dụ Celery/Redis). API phản hồi ngay lập tức `202 Accepted` (Processing). Khi job hoàn thành, Backend push Event `AUTO_SCHEDULE_COMPLETED` qua WebSocket để Client vẽ lại Gantt chart hàng loạt.

---

## 2. Tiêu chí Chấp nhận (Acceptance Criteria)

**Là** Project Manager,
**Tôi muốn** nối các task bằng liên kết Finish-to-Start trên Gantt Chart,
**Để** hệ thống tự động đẩy lùi lịch các task phía sau nếu task trước bị trễ và báo đỏ đường găng.

**Acceptance Criteria (Gherkin):**
```gherkin
Given Task B phụ thuộc vào Task A (Finish-to-Start)
When tôi kéo dài thời hạn Task A thêm 2 ngày
Then hệ thống tự động đẩy Ngày Bắt Đầu của Task B thêm 2 ngày
And các Task nằm trên đường găng (Critical Path) sẽ tự động sáng viền đỏ
```
