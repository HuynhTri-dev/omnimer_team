# Functional Requirements Document (FRD)

> Focus on: WHAT the system must DO. Mỗi FR có input/output rõ ràng và liên kết với Business Rules.

## 1. Functional Requirements List

### Module: Multi-View Engine (FR-PRJ-001)
**Mô tả:** Hệ thống hỗ trợ hiển thị một tập hợp các Task dưới 4 dạng (Kanban, Scrum, Gantt, Table) trên cùng một nguồn dữ liệu thật (Single Source of Truth).

| FR ID | Requirement Description | Input | Output | Associated Business Rule | Priority |
|---|---|---|---|---|---|
| **FR-PRJ-001.1** | **Chuyển đổi View (View Switcher):** Hệ thống cho phép người dùng chuyển đổi qua lại giữa 4 góc nhìn: Kanban, Gantt, Table, Scrum mà không làm thay đổi dữ liệu gốc. | User click chọn View mới trên Toolbar | Giao diện render lại đồ thị/bảng theo View được chọn | BR-PRJ-001.1 | Must-have |
| **FR-PRJ-001.2** | **Đồng bộ Dữ liệu thời gian thực (View Sync):** Mọi thay đổi dữ liệu trên một View (VD: Kéo thả trên Kanban) phải được cập nhật tức thì tới các client đang mở View khác (VD: Gantt). | Event WebSocket (Thực thi thành công API Update Task) | UI cập nhật (Re-render) node task tương ứng mà không cần reload trang | BR-PRJ-001.2 | Must-have |
| **FR-PRJ-001.3** | **Bảo lưu Trạng thái (View State Preservation):** Hệ thống phải giữ nguyên các bộ lọc (Filter) và sắp xếp (Sort) khi người dùng chuyển đổi View. | Hành động chuyển View | Các tham số Filter/Sort được giữ nguyên trên URL Query Params | BR-PRJ-001.3 | Should-have |
| **FR-PRJ-001.4** | **Admin Radar (Giám sát cảnh báo):** Hệ thống tự động làm nhấp nháy đỏ các thẻ Task có tính chất khẩn cấp hoặc đang bị "Blocked". | Task cập nhật trạng thái "Blocked" hoặc Deadline < 24h | UI thẻ Task chuyển viền Đỏ và có hiệu ứng nhấp nháy liên tục | BR-PRJ-001.4 | Should-have |

---

## 2. Business Rules

| BR ID | Rule Description | Applies to FR |
|---|---|---|
| **BR-PRJ-001.1** | **Single Source of Truth:** Chỉ có duy nhất 1 database lưu thông tin Task. Mọi thay đổi ở bất kỳ View nào đều cập nhật chung vào bản ghi này thông qua REST API. | FR-PRJ-001.1 |
| **BR-PRJ-001.2** | **Optimistic Update & Fallback:** Thao tác trên giao diện (Kéo thả) sẽ update UI ngay lập tức. Nếu API ném lỗi (HTTP 4xx/5xx), UI tự động rollback về vị trí cũ và báo lỗi. | FR-PRJ-001.2 |
| **BR-PRJ-001.3** | **State Location:** Filter và Sort bắt buộc lưu ở `URL Params` để share link. Visible Columns và độ rộng cột lưu ở `LocalStorage`. | FR-PRJ-001.3 |
| **BR-PRJ-001.4** | **Gantt Unscheduled Edge Case:** Khi sang Gantt, nếu Task chưa có `start_date` hoặc `end_date`, nó bị đẩy ra "Unscheduled Backlog", không được vẽ lên timeline. | FR-PRJ-001.1 |

---

## 3. Data Structure

### Entity: Task (Dùng cho Multi-View)
| Field | Data Type | Required | Constraints |
|---|---|---|---|
| `task_id` | UUID | Yes | Primary Key |
| `title` | String | Yes | Max 255 chars |
| `status_id` | UUID | Yes | Foreign Key to Status table |
| `start_date` | ISO8601 | No | Phải nhỏ hơn hoặc bằng `end_date` |
| `end_date` | ISO8601 | No | Phải lớn hơn hoặc bằng `start_date` |
| `due_date` | ISO8601 | No | Deadline cố định |
| `reporter_id` | UUID | Yes | Foreign Key to User table |
| `assignee_id` | UUID | No | Foreign Key to User table |

---

## 4. Pre/Post-Conditions & Kịch bản Kiểm thử

### FR-PRJ-001.1: Chuyển đổi View & Đồng bộ
- **Pre-condition:** Người dùng đang ở màn hình Kanban của dự án "Marketing Q4", có quyền xem dự án.
- **Post-condition:** Dữ liệu Task hiển thị đúng logic cấu trúc của Gantt Chart.

**Kịch bản Kiểm thử (Gherkin):**
```gherkin
Given tôi đang ở màn hình dự án "Marketing Q4" (Kanban View)
When tôi chọn chuyển sang "Gantt View" từ thanh điều hướng
Then hệ thống tải đồ thị Gantt từ tập Task hiện tại
And nếu tôi thay đổi ngày kết thúc của Task A trên Gantt
Then khi quay lại "Kanban View", Task A cũng hiển thị ngày kết thúc mới
```

### FR-PRJ-001.4: Real-time Admin Radar
- **Pre-condition:** Project Manager đang mở màn hình Kanban/Gantt của dự án.
- **Post-condition:** Giao diện thay đổi tự động (nhấp nháy đỏ) theo tín hiệu WebSocket mà không cần Refresh trang.

**Kịch bản Kiểm thử (Gherkin):**
```gherkin
Given tôi (Project Manager) đang mở màn hình Kanban của dự án
When một nhân viên bấm nút "Mark as Blocked" ở một task bất kỳ trên máy của họ
Then thẻ task đó trên màn hình của tôi ngay lập tức chuyển sang viền màu đỏ và nhấp nháy (qua WebSocket)
And tôi không cần phải ấn F5 (Reload) trang web
```

---

## 5. Non-Functional Requirements (NFRs)

Mục này quy định các tiêu chuẩn kỹ thuật phi chức năng bắt buộc đối với Multi-View Engine.

| NFR Category | Requirement | Metrics / Targets |
|---|---|---|
| **Performance (Hiệu năng hiển thị)** | Render mượt mà khi dự án có trên 10.000 Tasks trên Kanban hoặc Table. Không bị crash trình duyệt. | Bắt buộc sử dụng **Virtual Scrolling (Windowing)**. |
| **Performance (Tốc độ tải)** | Thời gian render lần đầu khi chuyển View (Kanban -> Gantt) cho lượng dữ liệu < 1,000 tasks. | **First Contentful Paint (FCP) $\le 1.0s$**. |
| **Network (Độ trễ thời gian thực)** | Tốc độ truyền tải tín hiệu WebSocket từ lúc User A nhả chuột (Drop) đến khi màn hình User B chớp sáng. | **End-to-End Latency < 200ms** (mạng 4G tiêu chuẩn). |
| **Usability (Khả năng tương tác)** | Hỗ trợ tương tác cảm ứng trên thiết bị di động (Mobile/Tablet). | Hỗ trợ **Touch Events (Long-press to Drag)** bên cạnh HTML5 Drag&Drop. |
| **Availability (Khả năng dự phòng)** | Xử lý khi kết nối WebSocket không ổn định (rớt mạng hoặc bị Firewall chặn cổng). | Client auto-reconnect (Exponential backoff) và **Fallback xuống HTTPS Long-Polling**. |
