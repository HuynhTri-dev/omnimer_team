# Feature: Unified Inbox Gateway (FR-CHN-001)

**Mô tả:** Cổng tiếp nhận Webhook từ Telegram và Zalo OA, lưu vào hàng đợi và chuyển tới UI.

## 1. Đặc tả Kỹ thuật (FRD)

### 1.1 Data Contract (Inbound Webhook Payload normalization)
Hệ thống phải map JSON khác nhau từ Telegram/Zalo về một cấu trúc chuẩn chung:
```json
{
  "message_id": "string",
  "channel_type": "TELEGRAM | ZALO",
  "external_sender_id": "string",
  "sender_name": "string",
  "content": "string",
  "attachments": ["url1", "url2"],
  "received_at": "ISO8601"
}
```

### 1.2 Business Logic & Rules
*   **BL-CHN-001.1 (Message Queue):** Webhook endpoint chỉ làm nhiệm vụ parse và push vào RabbitMQ/Redis Streams, trả về `HTTP 200 OK` cho nền tảng thứ 3 trong vòng $< 100\text{ms}$ để tránh timeout.
*   **BL-CHN-001.2 (Idempotency):** Xử lý trùng lặp. Nếu Zalo gửi lại Webhook do nghẽn mạng (Retry), backend phải dựa vào `message_id` để bỏ qua, không hiển thị 2 lần trên Inbox.
