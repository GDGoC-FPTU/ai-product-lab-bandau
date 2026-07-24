# Phase 1 — SCAN & QUICK-ASSESS

> Tên nhóm: bandau
> Thành viên: Nguyen Van Dat - 2A202601969

## 1. Bảng quét cơ hội (SCAN)

Dùng 4 lenses để quét các bài toán hoạt động trong các công ty thành viên Vingroup.

| # | Subsidiary         | Lens                   | Mô tả ngắn bài toán                                                                                                       |
| - | ------------------ | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| 1 | **Xanh SM**  | Lặp lại              | So khớp và phân bổ lại cuốc xe khi khách hàng yêu cầu thay đổi điểm đến giữa chừng.                          |
| 2 | **Xanh SM**  | Tốn thời gian        | Điều phối viên xử lý thủ công các phản hồi khẩn cấp từ tài xế về sự cố sạc pin hoặc va chạm thực địa. |
| 3 | **VinFast**  | Lặp lại              | So khớp hóa đơn sạc điện và đối chiếu số liệu trạm sạc đối tác hằng tuần.                                  |
| 4 | **Vinhomes** | AI-upgrade             | Hệ thống phân loại và route tự động các phản hồi/khiếu nại của cư dân trên App Vinhomes Resident.             |
| 5 | **Vinmec**   | Pain từ người khác | Bác sĩ mất quá nhiều thời gian viết tóm tắt hồ sơ xuất viện.                                                      |
| 6 | **Xanh SM**  | Tốn thời gian        | Tóm tắt lý do khách hàng hủy chuyến từ cuộc gọi ghi âm và ghi chú của tài xế để tìm pattern lỗi.           |

## 2. 3 Quick Problem Cards

### Quick Problem Card #1 — Xanh SM xử lý sự cố sạc pin thực địa

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Tài xế Xanh SM báo cáo sự cố sạc pin / hết pin   │
│ giữa đường cần điều phối cứu hộ hoặc trạm sạc gần nhất.     │
│ Công ty thành viên: [x] Xanh SM (GSM)                       │
│                                                             │
│ Ai đang đau? Tài xế (chờ đợi), Điều phối viên (quá tải)     │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Tài xế gọi tổng đài điều vận báo hết pin               │
│   → 2. Điều phối viên tra cứu thủ công vị trí xe trên bản đồ│
│   → 3. Tra cứu thủ công các trạm sạc VinFast còn trụ trống   │
│   → 4. Viết tin nhắn chỉ dẫn/đường đi gửi qua App tài xế    │
│   → 5. Liên hệ đội xe cứu hộ nếu xe đã cạn kiệt pin         │
│                                                             │
│ Bước nào tốn nhất? Bước 3-4 (⏱ 12 phút/lượt)                │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3-4              │
│ (Tự động hóa lấy vị trí -> Tra cứu trạm trống -> Draft tin) │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ Giảm thời gian xử lý sự cố từ 15 phút xuống dưới 3 phút.   │
│                                                             │
│ Quick Architecture: [x] LLM Feature                          │
└─────────────────────────────────────────────────────────────┘
```

### Quick Problem Card #2 — Vinhomes xử lý phản hồi cư dân

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Hệ thống phản hồi/khiếu nại của cư dân bị xử lý    │
│ thủ công, trễ thời gian và thiếu tính nhất quán.            │
│ Công ty thành viên: [x] Vinhomes                            │
│                                                             │
│ Ai đang đau? Nhân viên CSKH Vinhomes / Quản lý cư dân        │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Cư dân gửi khiếu nại qua App                           │
│   → 2. Nhân viên đọc và phân loại thủ công                  │
│   → 3. Soạn phản hồi định dạng và gửi lại cho cư dân        │
│   → 4. Cập nhật hồ sơ và theo dõi SLA                       │
│                                                             │
│ Bước nào tốn nhất? Bước 2-3 (⏱ 10 phút/lượt)                │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-3              │
│ (Phân loại, tóm tắt, draft phản hồi)                        │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ Giảm thời gian phản hồi từ 12 tiếng xuống dưới 2 tiếng.    │
│                                                             │
│ Quick Architecture: [x] LLM Feature                          │
└─────────────────────────────────────────────────────────────┘
```

### Quick Problem Card #3 — Xanh SM xử lý hủy chuyến

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Tóm tắt lý do khách hàng hủy chuyến và tìm pattern │
│ lỗi từ cuộc gọi/ghi chú của tài xế.                         │
│ Công ty thành viên: [x] Xanh SM (GSM)                       │
│                                                             │
│ Ai đang đau? Điều phối viên / Team phân tích vận hành        │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Các cuộc gọi và ghi chú được lưu lại                   │
│   → 2. Điều phối viên đọc và tóm tắt thủ công               │
│   → 3. Gắn nhãn nguyên nhân hủy chuyến                       │
│   → 4. Đưa lên báo cáo hàng ngày                             │
│                                                             │
│ Bước nào tốn nhất? Bước 2-3 (⏱ 8 phút/lượt)                 │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-3              │
│ (Tóm tắt, phân loại nguyên nhân)                            │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ Giảm thời gian tóm tắt từ 8 phút xuống dưới 2 phút.        │
│                                                             │
│ Quick Architecture: [x] LLM Feature                          │
└─────────────────────────────────────────────────────────────┘
```

## 3. Quyết định lựa chọn bài toán để Deep-Dive

Nhóm quyết định chọn bài toán **"Xanh SM xử lý sự cố sạc pin thực địa"** để thực hiện Deep-Dive.

### Lý do lựa chọn

- Có tác động trực tiếp đến hiệu suất điều vận thời gian thực.
- Dễ đo lường bằng thời gian xử lý và tỷ lệ thành công.
- Có thể xây dựng prototype prompt rõ ràng với ranh giới an toàn.
- Rủi ro sai sót có thể được kiểm soát bằng human-in-the-loop.

### Lý do loại bỏ các thẻ khác

- **Vinhomes CSKH:** Rủi ro liên quan đến thông tin cư dân và tranh chấp hợp đồng, cần thêm dữ liệu và quy trình rule-based trước.
- **Xanh SM hủy chuyến:** Tập trung ở back-office; không ảnh hưởng trực tiếp đến thao tác vận hành real-time như sự cố hết pin trên đường.
