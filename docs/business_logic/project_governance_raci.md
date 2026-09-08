# Project Governance, RACI & Escalation Model

> **Mục đích:** Xác định ai chịu trách nhiệm, ai phê duyệt, quyết định được đưa ra ở cấp nào và khi nào phải escalation.  
> **Áp dụng cùng:** `project_management_operating_model.md`  
> **Trạng thái:** Baseline Draft  
> **Phiên bản:** 1.0.0  
> **Ngày:** 2026-09-08

---

## 1. Nguyên tắc governance

1. Mỗi quyết định chỉ có **một Accountable owner** tại một thời điểm.
2. `Accountable` không đồng nghĩa người trực tiếp thực hiện.
3. Vai trò quản trị, chức danh nhân sự và quyền hệ thống là ba lớp riêng.
4. Một người kiêm nhiều vai trò phải được khai báo; không làm mất separation of duties.
5. Người tạo yêu cầu không tự phê duyệt thay đổi ảnh hưởng quyền lợi hoặc KPI của chính mình.
6. Phê duyệt phải dựa trên artifact/evidence, không chỉ dựa vào trạng thái UI.
7. Ủy quyền phải có phạm vi, thời hạn và audit trail.
8. AI/OPAgent không giữ vai trò `A` hoặc `R`; AI chỉ tạo đề xuất và evidence.

---

## 2. Danh mục vai trò

| Mã | Vai trò | Trách nhiệm chính | Không mặc định chịu trách nhiệm |
| :--- | :--- | :--- | :--- |
| **PB** | Portfolio Board / Steering Committee | Ưu tiên đầu tư, cấp vốn, dừng hoặc đổi hướng sáng kiến lớn | Điều phối task hằng ngày |
| **SP** | Project Sponsor | Business case, bảo trợ, quyết định vượt tolerance và chấp nhận closure | Quản lý sprint/backlog |
| **BO** | Business Owner / Product Owner | Giá trị, scope priority, acceptance và benefit realization | Phê duyệt ngân sách ngoài thẩm quyền |
| **PMO** | PMO / Governance Office | Chuẩn, assurance, portfolio reporting, coaching và audit | Thay PM điều hành project |
| **PGM** | Program Manager | Benefit và dependency giữa các project | Quản lý chi tiết mọi task |
| **PM** | Project Manager | Lập kế hoạch, baseline, RAID, change, forecast và delivery coordination | Sở hữu business benefit |
| **SM** | Scrum Master / Flow Facilitator | Hiệu quả quy trình, loại bỏ trở ngại, coaching Scrum/Kanban | Đánh giá nhân sự, sở hữu scope hoặc ngân sách |
| **TL** | Team/Technical Lead | Giải pháp thực thi, estimate, quality kỹ thuật và năng lực đội | Phê duyệt business scope |
| **TM** | Team Member / Contributor | Thực hiện, cập nhật trạng thái, evidence, cảnh báo blocker | Tự xác nhận acceptance cuối |
| **QA** | QA/Test Lead | Test strategy, quality evidence và release recommendation | Chấp nhận business outcome |
| **FIN** | Finance/Commercial | Funding control, cost validation, invoice/contract checks | Xếp priority sản phẩm |
| **HR** | HR/People Operations | Policy đánh giá, calibration, privacy và HRM export | Sửa task telemetry nguồn |
| **WA** | Workspace/System Admin | Cấu hình quyền, integration và technical operations | Phê duyệt nghiệp vụ hoặc KPI |

### 2.1 Quy tắc kiêm nhiệm

- Startup có thể để một người giữ `SP + BO` hoặc `PM + TL`; phải ghi trong Governance Profile.
- `PM + SM` chỉ nên kiêm nhiệm khi đội hiểu rõ xung đột giữa delivery accountability và process coaching.
- `HR`, `Direct Manager` và `Employee` không được cùng một người ở bước approve score của chính họ.
- `WA` có quyền kỹ thuật không được tự động có quyền đọc salary/KPI chi tiết.

---

## 3. RACI lifecycle

**Ký hiệu:** `R` — thực hiện; `A` — chịu trách nhiệm cuối; `C` — được tham vấn; `I` — được thông báo; `—` — không bắt buộc.

| Hoạt động | PB | SP | BO | PMO | PGM | PM | TL/TM | QA | FIN |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Tiếp nhận và sàng lọc proposal | A | C | R | R | C | I | — | — | C |
| Phê duyệt business case/funding | A | R | C | C | C | I | — | — | C |
| Chỉ định Sponsor và PM | I | A | C | R | C | I | — | — | — |
| Lập Project Charter | I | A | C | C | C | R | C | — | C |
| Chọn methodology/governance profile | I | A | C | C | C | R | C | C | — |
| Lập scope/WBS và acceptance plan | I | C | A | C | C | R | R | C | C |
| Lập schedule/resource/cost baseline | I | A | C | C | C | R | R | C | C |
| Phê duyệt Gate G3 | I | A | C | C | C | R | I | C | C |
| Điều hành và forecast project | I | C | C | C | C | A/R | R | C | C |
| Quản lý dependency liên project | I | C | C | C | A/R | R | C | — | — |
| Quality verification | I | I | C | C | I | C | R | A/R | — |
| Business acceptance | I | C | A/R | I | I | C | I | C | — |
| Closure project | I | A | C | C | C | R | I | C | C |
| Benefit review | C | C | A/R | C | R | I | — | — | C |

### 3.1 RACI KPI nhân sự

| Hoạt động | Direct Manager | Employee | HR | Data Owner | PM/Delivery Lead | System Admin |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| Định nghĩa metric contract | C | C | A | R | C | I |
| Xác nhận nguồn dữ liệu | C | I | C | A/R | C | C |
| Tính điểm tự động | I | I | A | C | I | R |
| Giải thích anomaly/data quality | C | C | A | R | C | C |
| Review điểm kỳ đánh giá | A/R | C | C | C | C | I |
| Gửi khiếu nại | C | A/R | I | C | I | — |
| Giải quyết khiếu nại | C | C | A | C | C | I |
| Calibration | R | I | A | C | C | — |
| Approve score cuối | R | I | A | C | I | — |
| Export sang HRM | I | I | A | C | — | R |

Điểm được tính tự động không đồng nghĩa tự động được duyệt. HRM chỉ nhận score ở trạng thái `Approved`.

---

## 4. Quyền quyết định

| Quyết định | Trong tolerance | Vượt tolerance | Evidence bắt buộc |
| :--- | :--- | :--- | :--- |
| Điều chỉnh task plan không đổi baseline milestone | PM/TL theo phân quyền | Sponsor nếu ảnh hưởng milestone | Task/dependency impact |
| Thay đổi scope đã baseline | PM nếu nằm trong delegated tolerance | Sponsor/Change Control Board; PB nếu vượt funding envelope | Change Request và impact analysis |
| Dùng management reserve | PM theo hạn mức | Sponsor/Finance/PB theo ngưỡng | Cost forecast và approval |
| Chấp nhận residual risk | PM với Low/Medium | Sponsor với High; PB/Security authority với Critical | Risk assessment và response |
| Waive defect | BO + QA theo release policy | Sponsor hoặc risk authority với mức nghiêm trọng cao | Defect record, impact và expiry |
| Tạm dừng project | Sponsor trong funding envelope | PB nếu ảnh hưởng portfolio/contract lớn | Issue/risk, options và transition plan |
| Hủy project | Sponsor đề xuất | PB quyết định | Updated business case và closure impact |
| Override KPI | Direct Manager đề xuất có lý do | HR/Calibration authority phê duyệt | Evidence, delta và audit trail |
| Export KPI sang HRM | HR sau approval | Không cho export Draft/Disputed | Approved cycle và export manifest |

---

## 5. Tolerance

Tolerance là ngưỡng được cấp trên ủy quyền cho cấp dưới. Mỗi project phải cấu hình theo sáu chiều:

- **Time:** Sai lệch milestone/end date.
- **Cost:** Sai lệch budget hoặc forecast at completion.
- **Scope:** Mức thay đổi deliverable/requirement.
- **Quality:** Defect, acceptance hoặc service threshold.
- **Risk:** Residual exposure và risk appetite.
- **Benefit:** Sai lệch outcome/ROI dự kiến.

### 5.1 Mẫu cấu hình

| Dimension | Baseline | Lower/Upper tolerance | Measurement | Escalation owner |
| :--- | :--- | :--- | :--- | :--- |
| Time | Approved finish date | Theo Governance Profile | Forecast finish variance | Sponsor |
| Cost | Budget at Completion | Theo funding policy | EAC so với BAC | Sponsor/Finance |
| Scope | Approved scope baseline | Change category/impact | Approved vs requested scope | BO/Sponsor |
| Quality | Acceptance/DoD targets | Theo severity/SLA | Open defects và test evidence | BO/QA |
| Risk | Risk appetite | Exposure threshold | Probability × impact hoặc model được duyệt | Sponsor/Risk authority |
| Benefit | Business case target | Benefit range | Actual/forecast outcome | BO/PB |

Không dùng một ngưỡng mặc định cho mọi ngành hoặc project. Template có thể đề xuất giá trị khởi đầu, nhưng Sponsor phải xác nhận trước G3.

---

## 6. Escalation model

### 6.1 Cấp độ

| Cấp | Điều kiện | Ví dụ | Hành động |
| :--- | :--- | :--- | :--- |
| **E1 — Team** | Trong tolerance, xử lý được trong team | Blocker task, thiếu thông tin ngắn hạn | TL/SM điều phối và ghi action |
| **E2 — Project** | Nguy cơ ảnh hưởng milestone hoặc cần PM quyết định | Dependency có khả năng trễ, WIP tắc nghẽn | PM lập corrective action và forecast |
| **E3 — Sponsor/Program** | Vượt hoặc dự báo vượt tolerance | Scope/cost/time breach, risk High | Exception Report và quyết định Sponsor/PGM |
| **E4 — Portfolio/Crisis** | Ảnh hưởng chiến lược, pháp lý, an toàn, dữ liệu hoặc khả năng tồn tại project | Security incident Critical, funding failure, regulatory breach | Kích hoạt crisis process và PB/risk authority |

### 6.2 Target phản hồi mặc định

Các mốc dưới đây là **đề xuất cấu hình**, không phải SLA bắt buộc cho mọi tổ chức:

| Cấp | Acknowledge target | Decision/update target | Kênh |
| :--- | :--- | :--- | :--- |
| E1 | Trong ngày làm việc | Trước daily coordination tiếp theo | Board/chat nội bộ |
| E2 | 4 giờ làm việc | 1 ngày làm việc | Project alert + action record |
| E3 | 1 giờ làm việc | 4 giờ làm việc hoặc thời gian được Sponsor xác nhận | Exception notification |
| E4 | Ngay lập tức | Theo crisis/incident policy | Paging + crisis channel |

Security, safety, legal và privacy incident phải tuân theo incident policy chuyên biệt nếu policy đó nghiêm ngặt hơn.

### 6.3 Nội dung escalation

Escalation hợp lệ phải có:

1. Vấn đề và thời điểm phát hiện.
2. Baseline/tolerance bị ảnh hưởng.
3. Tác động hiện tại và forecast.
4. Biện pháp containment đã thực hiện.
5. Các lựa chọn cùng trade-off.
6. Khuyến nghị của owner.
7. Người cần quyết định và deadline quyết định.

Thiếu giải pháp không phải lý do trì hoãn báo cáo E3/E4.

---

## 7. Change Control Board

CCB không bắt buộc là một hội đồng thường trực. Thành phần được chọn theo loại thay đổi:

- Sponsor: chủ trì quyết định.
- Business Owner/Product Owner: value và priority.
- PM: impact tổng thể và recommendation.
- TL/Architect: feasibility và technical impact.
- QA/Security/Legal: khi thay đổi ảnh hưởng domain tương ứng.
- Finance/Commercial: khi ảnh hưởng budget, pricing hoặc contract.
- PMO: assurance và policy.

CCB phải ghi `Approve`, `Reject`, `Defer` hoặc `Request More Information`; không để Change Request ở trạng thái mơ hồ.

---

## 8. Separation of duties và xung đột lợi ích

Các hành động sau cần ít nhất hai actor độc lập:

- Tạo và phê duyệt API credential/integration nhạy cảm.
- Đề xuất và phê duyệt KPI override.
- Phê duyệt score và export sang payroll.
- Tạo payment/invoice data và xác nhận financial closure.
- Đề xuất và phê duyệt waiver cho Critical defect/risk.

Nếu quy mô tổ chức không đủ người, ngoại lệ phải được Sponsor/HR ghi nhận, có expiry và post-review.

---

## 9. Ánh xạ vai trò sang quyền hệ thống

| Capability | Vai trò nghiệp vụ mặc định | Điều kiện |
| :--- | :--- | :--- |
| Tạo project | PM/PMO | Trong workspace và portfolio được cấp |
| Approve project/gate | Sponsor/PB | Có approval assignment |
| Sửa baseline | PM | Tạo version mới; không overwrite |
| Approve scope/change | BO/SP/CCB | Theo decision threshold |
| Xem task | Project participant/guest | Theo project membership |
| Xem KPI cá nhân | Chính nhân viên, Direct Manager, HR phù hợp | Least privilege |
| Sửa metric definition | Data Owner/HR governance | Versioned change và effective date |
| Override KPI | Direct Manager đề xuất, HR approve | Reason/evidence bắt buộc |
| Export HRM | HR integration operator | Score cycle đã Approved |
| Quản trị integration secret | WA được ủy quyền | Không mặc định xem dữ liệu nghiệp vụ |

Quyền phải được kiểm tra server-side; ẩn nút trên UI không phải access control.

---

## 10. Governance audit

PMO hoặc governance owner kiểm tra định kỳ:

- Mỗi project có Sponsor, PM và Business Owner rõ ràng.
- Không có gate decision thiếu evidence/approver.
- Không có baseline bị overwrite.
- E3/E4 được đóng với decision và action.
- Delegation chưa hết hạn và đúng phạm vi.
- KPI override/HRM export tuân separation of duties.
- Guest và tài khoản rời tổ chức đã bị thu hồi quyền.
- Governance Profile còn phù hợp khi scope/risk thay đổi.

---
