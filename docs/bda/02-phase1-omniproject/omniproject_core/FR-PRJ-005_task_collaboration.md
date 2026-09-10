# Feature: Task Collaboration & Attachments (FR-PRJ-005)

**Mô tả:** Hệ thống hỗ trợ làm giàu nội dung Task qua việc đính kèm tài liệu, bình luận trao đổi và tag tên thành viên.

## 1. Đặc tả Kỹ thuật (FRD)

### 1.1 Business Logic & Rules
* **BL-PRJ-005.1 (Attachments):** Hỗ trợ đính kèm file (PDF, Image, Excel). File được upload qua Pre-signed URL của hệ thống lưu trữ (S3/GCS) để giảm tải cho backend.
* **BL-PRJ-005.2 (Mentions):** Khi người dùng bình luận có `@username`, hệ thống sẽ bóc tách và tạo Notification gửi qua WebSocket và Email cho người được tag.

---

## 2. Tiêu chí Chấp nhận (Acceptance Criteria)

**Là** Team Member,
**Tôi muốn** đính kèm file thiết kế và bình luận `@mention` đồng nghiệp trực tiếp trong thẻ Task,
**Để** giữ mọi tài liệu và lịch sử trao đổi ngữ cảnh tại một nơi duy nhất.

**Acceptance Criteria (Gherkin):**
```gherkin
Given tôi đang xem chi tiết một Task
When tôi gõ "@Lan" vào ô bình luận và lưu lại
Then hệ thống sẽ gửi Notification (In-app và Email) đến tài khoản của Lan
And bình luận của tôi được lưu kèm theo timestamp hiển thị trong Activity Log
```
