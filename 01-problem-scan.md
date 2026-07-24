# 01 — Problem Scan & Quick-Assess
# Lab 02: AI Product Scoping — Vin Smart Future

> **Tác giả:** Bùi Thế Huy — MSSV: 20A202601881
> **Ngày:** 24/07/2026
> **Vai trò:** AI Product Engineer tại Vin Smart Future

---

# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội AI (Cá nhân)

Sử dụng **4 Lenses** để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **6 bài toán/bottleneck** thực tế tiềm năng.

### 4 Lenses:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ hiện tại còn chậm hoặc phản hồi rập khuôn
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn

### 📝 Bảng quét cơ hội:

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **Vinhomes** | Lặp lại | Nhân viên CSKH phân loại thủ công ~500 phản ánh/khiếu nại của cư dân gửi qua App Vinhomes Resident mỗi ngày (mất nước, hỏng thang máy, ồn ào…) và route đến đúng đội kỹ thuật của từng tòa nhà — mất ~12 phút/ticket. |
| 2 | **Vinmec** | Tốn thời gian | Bác sĩ mất 20–30 phút/bệnh nhân để viết tay bản tóm tắt hồ sơ xuất viện (Discharge Summary) từ bệnh án điện tử, kết quả xét nghiệm và ghi chú lâm sàng — dẫn đến quá tải và trì hoãn ra viện. |
| 3 | **Xanh SM** | Tốn thời gian | Điều phối viên phải nghe lại từng đoạn ghi âm cuộc gọi hủy chuyến của khách hàng và ghi chú thủ công của tài xế để phân loại lý do hủy — mất ~8 phút/ca, ~150 ca/ngày, không thể tìm pattern lỗi hệ thống. |
| 4 | **VinFast** | AI-upgrade | Khách hàng mô tả lỗi xe bằng tiếng Việt thông thường (ví dụ: *"xe qua gờ giảm tốc kêu cụp cụp ở bánh trước"*), tổng đài tiếp nhận thủ công và phân loại nhầm mã lỗi kỹ thuật, dẫn đến triệu hồi xe về xưởng sai bộ phận. |
| 5 | **Vinpearl** | Pain từ người khác | Đội quản lý Vinpearl Hotels không theo dõi kịp các review 1–2 sao xuất hiện real-time trên Booking.com, Agoda, Google Map — phàn nàn khẩn cấp như "phòng bẩn" hay "điều hòa hỏng" đến 12–24 tiếng mới được xử lý. |
| 6 | **Xanh SM** | Tốn thời gian | Điều phối viên Xanh SM xử lý thủ công sự cố tài xế báo hết pin thực địa — tra cứu bản đồ, tìm trụ sạc trống, soạn tin hướng dẫn mất ~15 phút/lượt trong khi có ~80 sự cố/ngày tại Hà Nội. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards (Cá nhân)

Chọn **top 3 bài toán tiềm năng nhất** từ danh sách SCAN: **#6 (Xanh SM sự cố pin)**, **#1 (Vinhomes CSKH)**, **#2 (Vinmec Discharge Summary)**.

**Lý do loại bỏ #3, #4, #5:**
- **#3 (Xanh SM hủy chuyến):** Bài toán phân tích offline (back-office), không ảnh hưởng trực tiếp đến vận hành thời gian thực như sự cố pin thực địa.
- **#4 (VinFast phân loại lỗi):** Cần tích hợp sâu với cơ sở dữ liệu mã lỗi kỹ thuật độc quyền — dữ liệu training chưa sẵn sàng.
- **#5 (Vinpearl review):** Rủi ro thấp hơn, ít ảnh hưởng vận hành real-time so với 3 bài toán được chọn.

---

```
┌─────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                           │
│                                                                 │
│ Bài toán: Tự động hóa hỗ trợ điều phối viên Xanh SM xử lý      │
│           sự cố tài xế báo hết pin thực địa                     │
│ Công ty thành viên: [x] Xanh SM (GSM)                          │
│                                                                 │
│ Ai đang đau (Actor)?                                            │
│   Điều phối viên (Dispatcher) tại Trung tâm Điều vận Xanh SM — │
│   xử lý ~80 sự cố pin/ngày tại Hà Nội hoàn toàn thủ công.     │
│                                                                 │
│ Workflow thủ công hiện tại (5 bước):                            │
│   1. Tài xế gọi tổng đài báo hết pin                           │
│   → 2. Dispatcher tra cứu vị trí xe trên bản đồ nội bộ         │
│   → 3. Tìm thủ công trạm sạc VinFast còn trụ trống gần nhất    │
│   → 4. Soạn tin nhắn hướng dẫn đường đi gửi qua App tài xế     │
│   → 5. Gọi cứu hộ nếu pin dưới ngưỡng di chuyển an toàn        │
│                                                                 │
│ Bước nào tốn nhất? Bước 3–4 (⏱ 10–12 phút/lượt)                │
│   → Tra cứu thủ công + soạn tin nhắn bằng tiếng Việt rõ ràng   │
│                                                                 │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                          │
│   Bước 2–4: Auto-pull vị trí GPS → Tra trạm sạc trống phù hợp  │
│   với loại xe (VF5/VF8) → LLM draft tin hướng dẫn [DRAFT_ONLY] │
│                                                                 │
│ Đo thành công bằng gì (Metric có số)?                           │
│   1. Giảm thời gian xử lý từ 15 phút → dưới 3 phút/lượt        │
│   2. Tỉ lệ hướng dẫn đúng địa điểm + đúng loại trụ sạc ≥ 98%  │
│   3. Tiết kiệm ~20 giờ làm việc/ngày cho team điều vận          │
│                                                                 │
│ Quick Architecture: [x] LLM Feature                             │
│   (Quy trình cố định, cần HITL: dispatcher phê duyệt draft)    │
└─────────────────────────────────────────────────────────────────┘
```

---

```
┌─────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                           │
│                                                                 │
│ Bài toán: Phân loại và điều hướng tự động phản ánh cư dân       │
│           gửi qua App Vinhomes Resident đến đúng đội kỹ thuật   │
│ Công ty thành viên: [x] Vinhomes                                │
│                                                                 │
│ Ai đang đau (Actor)?                                            │
│   Nhân viên CSKH Vinhomes (BQL tòa nhà) — xử lý thủ công       │
│   ~500 ticket/ngày trên tất cả các dự án Vinhomes Hà Nội.      │
│                                                                 │
│ Workflow thủ công hiện tại (5 bước):                            │
│   1. Cư dân gửi phản ánh qua App Vinhomes Resident             │
│   → 2. CSKH đọc nội dung text và ảnh đính kèm                  │
│   → 3. Tra cứu danh mục phân loại (mất nước / thang máy /      │
│         ồn ào / điện / an ninh / vệ sinh / khác)               │
│   → 4. Gõ thủ công vào hệ thống quản lý ticket (Salesforce)    │
│   → 5. Forward đến nhóm kỹ thuật phụ trách tòa tương ứng       │
│                                                                 │
│ Bước nào tốn nhất? Bước 3–4 (⏱ 8 phút/ticket)                  │
│   → Đọc hiểu ngôn ngữ tự nhiên đa dạng của cư dân              │
│     và tra cứu + map vào đúng danh mục                         │
│                                                                 │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                          │
│   Bước 2–4: LLM đọc nội dung → Phân loại danh mục              │
│   → Extract thông tin căn hộ/tòa → Tự động tạo draft ticket    │
│                                                                 │
│ Đo thành công bằng gì (Metric có số)?                           │
│   1. Giảm thời gian xử lý từ 12 phút → dưới 2 phút/ticket      │
│   2. Độ chính xác phân loại đúng danh mục đạt ≥ 95%            │
│   3. Tiết kiệm ~83 giờ làm việc/ngày cho team CSKH             │
│                                                                 │
│ Quick Architecture: [x] LLM Feature                             │
│   (Phân loại có cấu trúc cố định, không cần Agent tự trị)      │
└─────────────────────────────────────────────────────────────────┘
```

---

```
┌─────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                           │
│                                                                 │
│ Bài toán: Tự động soạn thảo bản tóm tắt hồ sơ xuất viện        │
│           (Discharge Summary) từ bệnh án điện tử tại Vinmec     │
│ Công ty thành viên: [x] Vinmec                                  │
│                                                                 │
│ Ai đang đau (Actor)?                                            │
│   Bác sĩ điều trị và intern tại các khoa của Vinmec —           │
│   mỗi bác sĩ viết 8–15 Discharge Summary/ngày trong giờ cao    │
│   điểm, chiếm ~30% tổng thời gian làm việc lâm sàng.           │
│                                                                 │
│ Workflow thủ công hiện tại (5 bước):                            │
│   1. Bác sĩ mở bệnh án điện tử (HIS) tra cứu lịch sử nhập viện │
│   → 2. Đọc kết quả xét nghiệm, chẩn đoán hình ảnh, ghi chú     │
│         lâm sàng từ nhiều nguồn khác nhau                       │
│   → 3. Viết tay/gõ bản tóm tắt theo template Word cứng         │
│   → 4. Trưởng khoa review và ký duyệt                          │
│   → 5. In và đóng hồ sơ giấy giao cho bệnh nhân khi ra viện    │
│                                                                 │
│ Bước nào tốn nhất? Bước 2–3 (⏱ 22 phút/bệnh nhân)              │
│   → Tổng hợp thủ công từ nhiều tài liệu rời rạc và viết lại    │
│     thành ngôn ngữ dễ hiểu cho bệnh nhân                       │
│                                                                 │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                          │
│   Bước 2–3: LLM đọc dữ liệu HIS → Trích xuất thông tin chính   │
│   → Soạn thảo draft Discharge Summary bằng tiếng Việt           │
│     thân thiện theo đúng template Vinmec                        │
│                                                                 │
│ Đo thành công bằng gì (Metric có số)?                           │
│   1. Giảm thời gian soạn thảo từ 25 phút → dưới 5 phút/ca      │
│   2. Tỉ lệ draft đạt chuẩn không cần sửa lớn: ≥ 85%            │
│   3. Giải phóng ~3 giờ/ngày cho mỗi bác sĩ tập trung lâm sàng  │
│                                                                 │
│ Quick Architecture: [x] LLM Feature                             │
│   (Cần Human-in-the-loop bắt buộc: bác sĩ PHẢI ký duyệt trước  │
│    khi giao cho bệnh nhân — không được tự động hóa hoàn toàn)  │
└─────────────────────────────────────────────────────────────────┘
```

---

> **Ghi chú cá nhân:** Trong 3 cards trên, tôi đánh giá **Card #1 (Xanh SM sự cố pin)** có tác động trực tiếp nhất đến vận hành real-time và an toàn của tài xế. Card này cũng có ranh giới kỹ thuật rõ nhất để implement (HITL + PIN_THRESHOLD < 5% → Mobile Charger dispatch). Đây là bài toán nhóm lựa chọn để thực hiện Deep-Dive.
