# Feature: Dynamic Custom Fields (FR-PRJ-004)

**Mô tả:** Hệ thống quản lý trường dữ liệu tùy biến cho từng Project.

## 1. Đặc tả Kỹ thuật (FRD)

### 1.1 Field Definition Schema

```jsonc
{
  "field_id": "uuid",
  "project_id": "uuid",
  "name": "Budget",
  "type": "CURRENCY",
  "validation_rules": {
    "min": 0,
    "required": true
  }
}
```

### 1.2 Business Logic & Rules

* **BL-PRJ-004.1 (Type Safety Enforcement):** Backend validate chặt chẽ `value` truyền lên dựa vào `type`. Nếu `type=CURRENCY`, `value` phải là Number; nếu sai ném lỗi HTTP 422 Unprocessable Entity.

*(Lưu ý: Tính năng này chưa có Acceptance Criteria chi tiết trong tài liệu hiện tại).*
