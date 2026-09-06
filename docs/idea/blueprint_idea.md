## 1. TỔNG QUAN KIẾN TRÚC HỆ THỐNG (SYSTEM BLUEPRINT)

Hệ thống được thiết kế theo mô hình **Module-driven / Event-driven Architecture**, giúp các module hoạt động độc lập nhưng dễ dàng đồng bộ dữ liệu thông qua Event Bus (Message Queue).

```
                      +-----------------------------+
                      |       OmniMer Web App       |
                      |   (Next.js / React / Vue)   |
                      +--------------+--------------+
                                     |
+------------------------------------+------------------------------------+
|                                    |                                    |
v                                    v                                    v
[ OmniProject ]              [ OmniChannel ]                [ OmniKPI ]
- Kanban / Scrum / Gantt     - Gateway: Zalo, Telegram      - Scoring Engine
- Multi-domain Workflows     - Unified Inbox                - HRM Integration API
- Dynamic Custom Fields      - Channel Router               - Performance Dashboards
|                                    |                                    |
+------------------------------------+------------------------------------+
                                     |
                                     v
                       +---------------------------+
                       |          OPAgent          |
                       |    (AI Workflow Engine)   |
                       | - Natural Language to Task|
                       | - Auto Assignment & Due   |
                       | - Status & Health Monitor |
                       +---------------------------+

```

---

## 2. THIẾT KẾ CHI TIẾT TỪNG MODULE

### 2.1. OmniProject: Quản trị dự án đa ngành & linh hoạt mô hình

Không giới hạn ở dự án phần mềm, module này phục vụ đa dạng nhu cầu (Marketing Campaign, Triển khai bán hàng, Tuyển dụng, R&D).

* **Đa chế độ xem (Multi-View System):**
* *Kanban View:* Phù hợp vận hành thường nhật, kiểm soát WIP (Work in Progress), áp dụng cho Marketing, Sales pipeline, HR sourcing.
* *Scrum/Sprint View:* Phù hợp các chiến dịch ngắn hạn (Sprint 1–2 tuần) với Product Backlog, User Stories, Story Points.
* *Gantt / Timeline View:* Tuyến tính (Waterfall), thể hiện quan hệ phụ thuộc (Dependencies: Finish-to-Start), đường găng (Critical Path) cho các dự án xây dựng, sự kiện, triển khai hạ tầng.
* *Table / List View:* Dễ dàng thao tác dạng bảng tính cho các phòng ban phi công nghệ.

* **Cơ chế tùy biến linh hoạt (Dynamic Workflows):**
* *Custom Statuses:* Tự định nghĩa luồng trạng thái theo phòng ban (Ví dụ: Marketing có trạng thái `Idea` $\rightarrow$ `Draft` $\rightarrow$ `Review` $\rightarrow$ `Approved` $\rightarrow$ `Published`).
* *Custom Fields:* Hỗ trợ đa dạng trường dữ liệu: Số tiền (Budget), Tệp đính kèm, Checklist con, Đánh giá độ ưu tiên (Eisenhower Matrix: Khẩn cấp/Quan trọng).

---

### 2.2. OmniChannel: Trung tâm hội tụ giao tiếp đa nền tảng

Hợp nhất các kênh giao tiếp phổ biến (Zalo OA / Zalo Bot, Telegram Bot, Webhook) về một giao diện tập trung.

* **Kiến trúc Gateway & Router:**
* Tiếp nhận Webhook từ Zalo API, Telegram Bot API và điều phối qua Message Queue (RabbitMQ hoặc Redis Streams) để đảm bảo không thất thoát tin nhắn khi tải cao.
* *Unified Inbox (Hộp thư tập trung):* Quản lý hội thoại theo khách hàng/thành viên mà không cần chuyển đổi ứng dụng.

* **Liên kết trực tiếp với Dự án:**
* Chuyển đổi 1-click hoặc tự động từ tin nhắn/hội thoại thành Task dự án.
* Tạo các Group/Topic riêng biệt gắn với từng Dự án (Project-bound Threading).

---

### 2.3. OmniKPI: Đo lường hiệu suất dự án & Tích hợp HRM

Hệ thống tính toán hiệu suất tự động dựa trên dữ liệu thực thi thực tế, loại bỏ việc đánh giá cảm tính.

* **Cơ chế tính điểm hiệu suất đa biến (Scoring Engine):**

$$\text{Điểm KPI Dự án} = w_1 \times \text{Tỷ lệ đúng hạn (On-time)} + w_2 \times \text{Tỷ lệ hoàn thành (Completion)} + w_3 \times \text{Độ phức tạp (Task Weight)}$$

* Tích hợp phạt trễ hạn (Overdue Penalty) có trọng số theo mức độ ưu tiên.
* Hỗ trợ chấm điểm chéo (Peer Review) và đánh giá chất lượng (Definition of Done Compliance).

* **Kiến trúc API kết nối HRM:**
* *Inbound API:* Đồng bộ danh sách nhân sự, sơ đồ phòng ban, chức vụ, ca làm việc từ hệ sinh thái HRM (như Odoo, Base, hoặc custom ERP).
* *Outbound Webhook / Sync API:* Định kỳ (cuối tháng/quý) tự động đẩy bảng tổng hợp hiệu suất (Performance Scorecard) sang module Tính lương / Khen thưởng của HRM.
* *Bảo mật & Phân quyền:* Phân quyền RBAC (Role-Based Access Control) nghiêm ngặt; chỉ HR Manager và Direct Manager mới có quyền tra cứu dữ liệu điểm nhạy cảm.

---

### 2.4. OPAgent: Trợ lý AI điều phối dự án thông minh

Đóng vai trò như một thư ký/quản lý dự án ảo (AI PM Assistant) chạy ngầm xuyên suốt hệ thống.

* **1. Tiếp nhận & Phân tích yêu cầu (Task Extraction):**
* *Đầu vào:* Tin nhắn chat từ OmniChannel (Zalo, Telegram) hoặc ghi âm/voice note trong cuộc họp.
* *Xử lý NLP/LLM:* Trích xuất Intent, tự động sinh:
* Tiêu đề chuẩn hóa (Title).
* Mô tả chi tiết (Description) định dạng Markdown.
* Tiêu chí chấp nhận bàn giao (Acceptance Criteria / Definition of Done).
* Danh sách công việc con (Sub-tasks / Action items).

* **2. Đề xuất nhân sự & Thời hạn (Smart Assignment):**
* Phân tích kỹ năng (Skill Tags) của thành viên trong team và độ tải hiện tại (Current Workload) để gợi ý người phù hợp nhất (`Assignee`).
* Dự đoán thời lượng thực hiện dựa trên lịch sử các task tương tự để đề xuất `Deadline` hợp lý.

* **3. Giám sát & Nhắc nhở chủ động (Health Check & Follow-up):**
* *Daily Standup Bot:* Định kỳ hỏi nhanh trạng thái qua Telegram/Zalo: *"Hôm nay bạn đang vướng gì ở task X?"*.
* *Cảnh báo rủi ro (Risk Alert):* Phát hiện các task sắp trễ hạn hoặc các task bị ứ đọng tại một cột quá lâu để nhắc nhở người phụ trách hoặc báo cáo cho PM.

---

## 3. THIẾT KẾ CÔNG NGHỆ ĐỀ XUẤT (TECH STACK)

| Tầng | Công nghệ đề xuất | Lý do lựa chọn |
| --- | --- | --- |
| **Frontend** | **Next.js (React) + TailwindCSS** | Hỗ trợ SSR/SSG tốt, tối ưu SEO, hệ sinh thái UI phong phú (Shadcn/UI). |
| **Backend Core** | **Node.js (NestJS) hoặc Go** | Kiến trúc module hóa rõ ràng, xử lý I/O bất đồng bộ mạnh mẽ, hỗ trợ WebSockets realtime. |
| **AI / OPAgent Service** | **Python (FastAPI) + LangChain / LangGraph** | Tối ưu cho việc xây dựng State Machine cho Agent, tích hợp các mô hình LLM và Speech-to-Text. |
| **Database** | **PostgreSQL** | Lưu trữ quan hệ chặt chẽ (Users, Projects, Permissions, Audit logs), hỗ trợ JSONB cho Custom Fields. |
| **Cache & Realtime** | **Redis + Redis Pub/Sub** | Caching dữ liệu, quản lý session và broadcast trạng thái thời gian thực. |
| **Message Broker** | **RabbitMQ / Celery** | Đảm bảo xử lý hàng đợi tin nhắn OmniChannel và các tác vụ tính KPI chạy ngầm không bị nghẽn. |

---

## 4. QUY TRÌNH HOẠT ĐỘNG LIÊN KẾT GIỮA CÁC MODULE (END-TO-END FLOW)

1. **Khởi tạo:** Khách hàng hoặc PM gửi một tin nhắn âm thanh/văn bản vào nhóm Telegram: *"Cần làm chiến dịch chạy Ads trên Facebook cho sản phẩm A, ngân sách 15tr, chạy từ 10/9 đến 20/9, giao cho bạn Lan Marketing"*.
2. **OmniChannel:** Tiếp nhận Webhook từ Telegram $\rightarrow$ Đẩy nội dung vào hàng đợi $\rightarrow$ Chuyển tiếp tới OPAgent.
3. **OPAgent:**

* Bóc tách thông tin: Chiến dịch = Marketing, Kênh = Facebook Ads, Budget = 15.000.000đ, Thời hạn = 10/9 – 20/9.
* Tạo Task trên **OmniProject** thuộc Board Marketing, gán nhãn `Priority: High`, gán cho nhân sự `Lan`, sinh sẵn các checklist: *Viết content*, *Thiết kế banner*, *Cài đặt chiến dịch*.
* Gửi phản hồi ngược lại Telegram để xác nhận với người giao việc.

1. **Thực thi & Giám sát:**

* Lan cập nhật tiến độ trên bảng Kanban.
* OPAgent theo dõi tiến độ; nếu ngày 18/9 vẫn chưa xong banner, OPAgent tự động gửi tin nhắn riêng cho Lan qua Zalo để hỏi thăm khó khăn.

1. **Đánh giá:**

* Sau khi task hoàn thành (`Done`), **OmniKPI** tự động tính điểm dựa trên việc hoàn thành đúng ngày 20/9 và ghi nhận vào bảng KPI tháng.
* Dữ liệu điểm được tổng hợp và đồng bộ tự động sang hệ thống HRM qua API.

---

## 5. LỘ TRÌNH TRIỂN KHAI THEO GIAI ĐOẠN (ROADMAP)

* **Giai đoạn 1: Nền tảng lõi & Quản lý Dự án (MVP)**
* Xây dựng Core Data Schema (User, Workspace, Project, Task, Custom Field).
* Hoàn thiện 2 chế độ xem cơ bản: Kanban Board và List/Table View.

* **Giai đoạn 2: Tích hợp AI (OPAgent v1)**
* Tích hợp OPAgent tạo task từ Prompt văn bản (Title, Description, Checklist).
* Xây dựng luồng xác nhận và phân rã task tự động.

* **Giai đoạn 3: Hội tụ Đa kênh (OmniChannel) & Bot tương tác**
* Kết nối Webhook Telegram Bot và Zalo OA.
* Cho phép OPAgent nhận diện lệnh qua tin nhắn chat từ các nền tảng này.

* **Giai đoạn 4: Đánh giá Hiệu suất (OmniKPI) & HRM Integration**
* Xây dựng động cơ tính điểm (Scoring Engine) và Dashboard báo cáo cá nhân/phòng ban.
* Cung cấp bộ REST API / Webhooks để kết nối với hệ thống HRM bên ngoài.
