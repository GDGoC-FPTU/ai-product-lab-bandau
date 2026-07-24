# Phase 3 — DEEP-DIVE REPORT

> Tên nhóm: bandau
> Thành viên: Nguyen Van Dat - 2A202601969

## 1. Quyết định lựa chọn bài toán

Nhóm chọn bài toán: **Xanh SM — Xử lý sự cố sạc pin thực địa**.

### Lý do chọn

- Bài toán có tính thực tế và lặp lại hàng ngày.
- Dễ quan sát bottleneck rõ ràng.
- Có thể xây dựng prompt prototype và kiểm tra ranh giới an toàn.
- Tính khả thi cao nếu dùng **LLM Feature** kết hợp **Human-in-the-loop**.

---

## 2. Problem Statement (6-field)

| Field                             | Nội dung chi tiết                                                                                                                                                                                                                                                                                                                     |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1. Actor / Operator**     | Điều phối viên (Dispatcher) thuộc Trung tâm Điều vận Xanh SM.                                                                                                                                                                                                                                                                  |
| **2. Current Workflow**     | Khi tài xế báo hết pin, điều phối viên tra cứu vị trí định vị trên bản đồ nội bộ, mở Dashboard trạm sạc VinFast để tìm trụ sạc trống gần nhất, viết tin nhắn chỉ dẫn/định vị gửi qua App tài xế, và gọi cứu hộ nếu pin dưới 5%. 5 bước, hoàn toàn thủ công, mất 15 phút/lượt. |
| **3. Bottleneck**           | Bước 3 & 4 (mất 10 phút): tra cứu thủ công trụ sạc trống phù hợp với dòng xe và soạn thảo tin nhắn hướng dẫn đường đi chi tiết bằng Tiếng Việt thân thiện.                                                                                                                                               |
| **4. Business Impact**      | Mỗi ngày có khoảng 80 sự cố pin thực địa tại Hà Nội. Gây lãng phí ~20 giờ làm việc/ngày của team điều vận, tăng thời gian chờ đợi của tài xế và làm giảm doanh thu do xe không thể đón khách kịp.                                                                                               |
| **5. Success Metric**       | 1. Giảm tổng thời gian xử lý sự cố từ**15 phút xuống dưới 3 phút**.2. Tỷ lệ hướng dẫn đúng địa điểm và đúng loại trụ sạc phù hợp đạt **98%**.                                                                                                                                             |
| **6. Operational Boundary** | AI được phép truy xuất API định vị xe, API trạm sạc VinFast trống, và tự động soạn thảo tin nhắn hướng dẫn dạng nháp.**Cấm:** AI không được tự động gửi tin mà không có điều phối viên phê duyệt; không được đề xuất trạm sạc không phù hợp với loại cổng sạc của xe.   |

---

## 3. Current-State Workflow Mapping

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Nhận cuộc    │     │ Tra cứu định │     │ Tra cứu trạm │     │ Soạn văn bản │
│ gọi sự cố    │ ──→ │ vị GPS xe   │ ──→ │ sạc VinFast  │ ──→ │ hướng dẫn    │
│              │     │              │     │ còn trụ trống│     │ gửi tài xế   │
│ Ai: Dispatcher│     │ Ai: Dispatcher│     │ Ai: Dispatcher│    │ Ai: Dispatcher│
│ ⏱ 2 phút     │     │ ⏱ 2 phút     │     │ ⏱ 5 phút 🔴  │     │ ⏱ 5 phút 🔴  │
│ In: Điện thoại│     │ In: Biển số  │     │ In: Vị trí GPS│     │ In: Raw data │
│ Out: Log sự cố│     │ Out: Toạ độ  │     │ Out: Địa chỉ │     │ Out: SMS     │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                      │
                                                                      ▼
                                                               ┌──────────────┐
                                                               │ Bước 5       │
                                                               │ Gọi xe cứu   │
                                                               │ hộ (nếu cần) │
                                                               │ Ai: Dispatcher│
                                                               │ ⏱ 1 phút     │
                                                               └──────────────┘
🔴 = Bottlenecks
⏱ Tổng thời gian xử lý thủ công: 15 phút/lượt.
```

---

## 4. Future-State Flow & AI Fit

### AI Fit

Chọn **LLM Feature**.

### Vì sao không chọn Agentic Loop?

- Quy trình có cấu trúc cố định và dễ xác định điểm kiểm soát.
- Rủi ro sai sót nếu AI tự ra quyết định trực tiếp có thể dẫn đến xe bị mất pin giữa đường.
- Với mức độ phức tạp hiện tại, một LLM feature kết hợp HITL là hợp lý và ít rủi ro hơn.

### Future-State Flow

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Nhận cuộc    │     │ 🔵 Auto-pull │     │ 🔵 AI draft  │     │ 🟢 Dispatcher│
│ gọi sự cố    │ ──→ │ vị trí &     │ ──→ │ SMS chỉ dẫn  │ ──→ │ duyệt & gửi │
│              │     │ trạm sạc trống│    │ & chỉ đường  │     │ qua App      │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                      │
                                                                      ▼
                                                               ↩️ Fallback:
                                                               Nếu AI draft lỗi,
                                                               Dispatcher tự viết
                                                               tay lại như cũ.
```

---

## 5. AI Readiness Checklist

1. [X] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test.
2. [X] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback).
3. [X] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ.

---

## 6. Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future

**GO** — Bắt đầu xây dựng Prototype với scope hẹp.

### Lý giải quyết định

- Bài toán có tính lặp lại và mức độ rõ ràng cao.
- Dữ liệu đầu vào có thể được truy xuất từ hệ thống hiện hữu.
- Ranh giới an toàn dễ định nghĩa bằng prompt và human review.
- Chi phí triển khai thấp hơn nhiều so với xây dựng một agent tự trị phức tạp.
- Metric thành công rõ ràng: giảm thời gian xử lý đáng kể, nâng chất lượng và giảm rủi ro an toàn.

---

## 7. Kết luận ngắn

Dự án này phù hợp để bắt đầu bằng **LLM Feature** trong quy trình điều phối Xanh SM. Với cơ chế **HITL** và **Fallback**, nhóm có thể tạo ra một prototype an toàn, có thể đo lường và dễ mở rộng sau này.
