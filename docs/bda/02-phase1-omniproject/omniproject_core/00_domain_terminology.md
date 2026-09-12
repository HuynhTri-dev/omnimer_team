# Domain Terminology & System Hierarchy

**Mô tả:** Tài liệu này chuẩn hóa các thuật ngữ nghiệp vụ (Domain Terminology) và mô tả hệ thống phân cấp (System Hierarchy) trong OmniProject. Tài liệu đóng vai trò như một "từ điển chung" giúp mọi thành viên (Dev, PM, QA, Client) hiểu đồng nhất về các khái niệm được sử dụng trong toàn bộ hệ thống.

---

## 1. Hệ thống Phân cấp (System Hierarchy Levels)

Hệ thống OmniProject được tổ chức theo cấu trúc phân cấp từ cao xuống thấp như sau:

### 1.1 Tổ chức & Không gian làm việc (Macro Level)
* **Organization (Tổ chức/Doanh nghiệp):** Cấp độ cao nhất, đại diện cho một công ty hoặc doanh nghiệp trả phí. Một Organization quản lý tập trung khâu thanh toán (Billing), bản quyền (License), và cấu hình SSO bảo mật cho toàn bộ nhân viên.
* **Workspace (Không gian làm việc):** Phân vùng làm việc vật lý/logic bên trong Organization. Một công ty có thể có nhiều Workspace (Ví dụ: Workspace cho Team IT, Workspace cho Team Marketing).
  * *Ranh giới:* Người dùng ở Workspace A không nhìn thấy dữ liệu của Workspace B. Thành viên phải được mời vào Workspace thì mới thấy danh sách dự án bên trong nó.

### 1.2 Nhóm dự án & Dự án (Project Level)
* **Portfolio (Danh mục dự án):** Là một tập hợp các dự án (Projects) được nhóm lại để quản lý ở cấp độ chiến lược. Giúp PMO hoặc C-level theo dõi tổng thể sức khỏe của nhiều dự án cùng lúc (FR-PRJ-010).
* **Project (Dự án):** Nơi chứa toàn bộ luồng công việc, danh sách Task, tài liệu, và thành viên tham gia cho một mục tiêu cụ thể. Mỗi Project có cấu hình quy trình riêng (Workflow, WIP limit, Custom Fields).
* **Personal Space (Không gian cá nhân):** Một "Dự án ảo" đặc biệt tự động tạo ra cho từng user. Chỉ user đó mới thấy. Nơi chứa các công việc cá nhân, ghi chú, to-do list (FR-PRJ-015).

### 1.3 Phân chia công việc (Task Level)
* **Sprint / Iteration (Vòng lặp):** Chỉ áp dụng nếu Project bật chế độ Scrum. Là khoảng thời gian cố định (thường 2 tuần) để hoàn thành một khối lượng công việc cụ thể.
* **Milestone (Cột mốc):** Điểm đánh dấu quan trọng trên dòng thời gian của dự án (Ví dụ: Ngày ra mắt MVP, Ngày chốt thiết kế). Thường hiển thị dưới dạng hình thoi trên Gantt Chart.
* **Task (Công việc):** Đơn vị công việc cơ bản nhất của hệ thống. Chứa thông tin mô tả, người phụ trách, hạn chót, file đính kèm và bình luận.
* **Subtask (Công việc con):** Các tác vụ nhỏ hơn nằm bên trong một Task cha. OmniProject giới hạn cấu trúc này ở 1 cấp độ (Không có sub-subtask) để tránh hệ thống quá phức tạp.

---

## 2. Các Góc nhìn Dữ liệu (Multi-View Engine)

OmniProject sử dụng mô hình "Single Source of Truth" (Dữ liệu gốc duy nhất). Cùng một tập hợp Task có thể được trực quan hóa qua nhiều "Góc nhìn" (View) khác nhau tùy mục đích sử dụng (FR-PRJ-001):

* **Kanban View:** Hiển thị công việc dưới dạng bảng các cột trạng thái (To Do, In Progress, Done). Tối ưu cho việc kéo thả và theo dõi dòng chảy công việc (Workflow/WIP limits).
* **Gantt View (Gantt Chart):** Đồ thị hình thanh ngang thể hiện thời gian bắt đầu và kết thúc của công việc theo trục thời gian dài hạn. Tối ưu để lập kế hoạch tổng thể, xem sự phụ thuộc (Dependencies) và Đường găng (Critical Path).
* **Table View (Dạng bảng):** Hiển thị công việc dưới dạng lưới (giống Excel). Tối ưu cho việc chỉnh sửa hàng loạt, sắp xếp, và xem các thông tin chi tiết qua nhiều Custom Fields.
* **Scrum Board (Active Sprint View):** Giao diện Kanban đặc biệt chỉ hiển thị các Task của một Sprint đang "ACTIVE". Ẩn toàn bộ Task trong Backlog.
* **Calendar View:** Lịch (tháng/tuần/ngày). Tối ưu để xem nhanh các thời hạn chót (Deadline) và khối lượng sự kiện rơi vào từng ngày.
* **Portfolio Board:** Màn hình dashboard cho PMO, không hiển thị Task mà hiển thị các "Thẻ Dự Án" để theo dõi "sức khỏe" của toàn tổ chức.

---

## 3. Thuật ngữ Vai trò & Quyền hạn (RBAC)

* **Workspace Admin:** Người sở hữu/quản lý cao nhất của Workspace. Cấu hình bảo mật, thanh toán và có quyền xem/xóa toàn bộ Project.
* **Project Manager (PM) / Owner:** Người quản lý một Project cụ thể. Có toàn quyền cấu hình workflow, thêm custom fields, duyệt ngày nghỉ, và quyết định ai làm gì.
* **Team Member (Assignee):** Thành viên thực thi công việc. Có quyền tạo, chỉnh sửa Task, nhưng bị hạn chế ở các thao tác thay đổi cấu trúc Project.
* **Guest (Khách / Client):** Người ngoài tổ chức (Ví dụ: Khách hàng, Đối tác thuê ngoài). Chỉ có quyền "Read-only" (Chỉ xem) hoặc chỉ tương tác với các Task được tag tên, bị chặn không cho thấy nội bộ team chat.

---

## 4. Các Thuật ngữ Kỹ thuật & Nghiệp vụ Đặc thù

* **Real-time Radar / View Sync:** Khái niệm chỉ việc màn hình của tất cả những người đang mở chung 1 dự án sẽ đồng bộ lập tức (bằng WebSocket) khi có 1 người nào đó thay đổi dữ liệu (kéo thả Task) mà không cần nhấn F5 (Tải lại trang).
* **DoD (Definition of Done) / Output Contract:** "Định nghĩa Hoàn thành". Trong OmniProject (FR-PRJ-008), DoD là điều kiện kỹ thuật ép buộc user phải tải lên file thiết kế hoặc link kết quả thì hệ thống mới cho phép kéo Task sang cột "Done".
* **WIP Limit (Work-In-Progress Limit):** Cảnh báo hoặc chặn việc nhét quá nhiều việc vào cùng một lúc. Ví dụ cột "Dev" có WIP Limit = 3, thì chỉ có tối đa 3 Task được phép nằm ở cột đó.
* **Optimistic Update (Cập nhật lạc quan):** Trải nghiệm UX mượt mà khi người dùng kéo thả Task, giao diện sẽ phản hồi thành công ngay lập tức thay vì phải hiển thị icon "Loading..." chờ server trả lời.
* **Action Score:** Thuật toán tự động tính toán "điểm ưu tiên" của một Task kết hợp giữa trọng số quan trọng (Importance) và thời gian còn lại đến hạn chót (Days to deadline), giúp hệ thống tự động đẩy việc gấp lên đầu danh sách (FR-PRJ-007).
* **Dependency & Critical Path (Đường găng):** Sự phụ thuộc giữa 2 việc (Ví dụ: Phải Xây móng xong mới được Xây tường). "Đường găng" là chuỗi dài nhất các công việc bị phụ thuộc nhau, nếu bất kỳ việc nào trên đường găng này bị trễ, toàn bộ dự án sẽ bị trễ.
* **Asset Governance:** Kho lưu trữ tài nguyên/tri thức tập trung. Nơi lưu trữ an toàn mọi file đính kèm, kết quả bàn giao của các Task sau khi đã hoàn thành.
