# 01. Problem Scan — AI Product Scoping (Vin Smart Future)

## 1. Problem Statement (Tuyên bố Vấn đề)
Trong hệ thống điều hành xe điện Xanh SM, các Điều phối viên (Dispatchers) chịu áp lực xử lý thời gian thực rất lớn. Hai rủi ro vận hành nghiêm trọng thường gặp là:
- **Gửi nhầm tin nhắn tự động:** Khách hàng hoặc tài xế nhận được tin nhắn tự động chưa qua kiểm duyệt của con người, gây ra sai lệch thông tin hành trình.
- **Đề xuất trạm sạc không an toàn:** Khi xe điện báo pin xuống mức nguy cấp (< 5%), việc hướng dẫn tài xế di chuyển đến các trạm sạc xa (> 5km) có thể dẫn đến việc xe hết sạch pin giữa đường, gây ách tắc giao thông và ảnh hưởng nghiêm trọng đến trải nghiệm dịch vụ.

## 2. Target Users (Đối tượng sử dụng)
- **Primary User:** Điều phối viên hệ thống Vin Smart Future / Xanh SM (Dispatchers).
- **Secondary User:** Tài xế xe điện (EV Drivers) nhận thông tin điều hướng cứu hộ từ hệ thống.

## 3. Proposed AI Solution (Giải pháp AI đề xuất)
Phát triển một **AI Dispatcher Co-Pilot** hoạt động với ranh giới an toàn nghiêm ngặt (Strict Operational Boundaries):
- **Cơ chế Duyệt Tin nhắn (Draft Boundary):** Mọi phản hồi/tin nhắn do AI tạo ra **BẮT BUỘC** phải bắt đầu bằng thẻ `[DRAFT_ONLY]` để hệ thống gắn cờ bản nháp, ngăn chặn việc tự động gửi tin nhắn mà chưa có xác nhận từ điều phối viên.
- **Giao thức Pin Nguy cấp (Critical Battery Boundary):** Tự động phát hiện khi mức pin xe dưới 5%. Trong trường hợp này, AI tuyệt đối không hướng dẫn đến trạm sạc xa (> 5km) mà ngay lập tức phát lệnh điều xe sạc di động (Mobile Charging Vehicle) dưới dạng định dạng cấu trúc JSON để cứu hộ kịp thời.