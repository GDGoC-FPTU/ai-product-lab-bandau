 Tên nhóm: bandau
 Thành viên: Hoàng Tuấn Trung - 2A202601807
 
 Phase 1 — SCAN
 List bài toán của tôi:
| # | Subsidiary | Lens                              | Mô tả ngắn bài toán                                                                                  
| 1 | Xanh SM    | Repetitive + AI-upgrade           | Hệ thống phải liên tục phân bổ và điều phối tài xế/xe đến các khu vực có nhu cầu cao, nhưng việc dự đoán nhu cầu và điều phối chưa tối ưu, dẫn đến xe rỗng hoặc khách phải chờ lâu. |
| 2 | Xanh SM    | Stakeholder Pain + Time-consuming | Tài xế gặp tình trạng gợi ý điểm đón không chính xác, phải liên tục liên hệ với khách để xác định vị trí, gây mất thời gian và giảm trải nghiệm.                                    |
| 3 | VinFast    | Repetitive + Time-consuming       | Nhân viên phải theo dõi tình trạng pin, lỗi xe và dữ liệu cảm biến để xác định xe nào cần bảo trì, dễ bỏ sót các dấu hiệu bất thường.                                               |
| 4 | Vinhomes   | Time-consuming + AI-upgrade       | Nhân viên CSKH phải thủ công phân loại và trả lời số lượng lớn phản ánh của cư dân như thang máy, vệ sinh, an ninh và cơ sở vật chất.                                               |
| 5 | Vinmec     | Time-consuming + AI-upgrade       | Bác sĩ và nhân viên y tế mất nhiều thời gian tổng hợp thông tin từ hồ sơ bệnh án để tìm lại lịch sử điều trị và các thông tin quan trọng của bệnh nhân.                             |

🃏 Phase 2 — QUICK-ASSESS
QUICK PROBLEM CARD #1
Bài toán (1 câu):

Xanh SM cần tối ưu việc điều phối xe và tài xế theo nhu cầu dự kiến của từng khu vực để giảm thời gian chờ của khách hàng và giảm số lượng xe chạy rỗng.

Công ty thành viên:
 VinFast
 X Xanh SM
 Vinhomes
 Vinmec
 Khác
Ai đang đau (Actor)?
Điều phối viên vận hành.
Tài xế Xanh SM.
Khách hàng phải chờ lâu.
Workflow thủ công hiện tại:
1. Theo dõi số lượng yêu cầu đặt xe
        ↓
2. Kiểm tra số lượng xe/tài xế đang hoạt động
        ↓
3. Quan sát khu vực đang có nhu cầu cao
        ↓
4. Điều phối hoặc khuyến khích tài xế di chuyển đến khu vực đó
        ↓
5. Theo dõi lại tình trạng cung - cầu
Bước nào tốn thời gian/lỗi nhất?

Bước 2–4: phân tích cung cầu và quyết định điều phối.

Ước tính:

⏱ 5–10 phút/lần kiểm tra thủ công.

AI có thể nhảy vào hỗ trợ ở bước nào?

AI có thể dự đoán nhu cầu theo:

Khu vực.
Thời gian trong ngày.
Ngày trong tuần.
Lịch sử đặt xe.
Thời tiết.
Sự kiện đặc biệt.

Sau đó, AI đề xuất các khu vực cần bổ sung xe/tài xế.

Đo thành công bằng gì?

Giảm thời gian chờ trung bình của khách hàng từ 8 phút xuống dưới 5 phút và giảm tỷ lệ xe chạy rỗng 10–15%.

Quick Architecture:
 No AI
 Rule
 X LLM
 X Agent

Ghi chú: Phần dự đoán nhu cầu nên sử dụng mô hình Machine Learning/Forecasting. LLM hoặc Agent có thể dùng ở lớp giải thích và hỗ trợ điều phối, không nhất thiết là thành phần dự đoán chính.

🃏 QUICK PROBLEM CARD #2
Bài toán (1 câu):

Tài xế Xanh SM thường gặp khó khăn khi tìm đúng điểm đón khách do vị trí GPS hoặc mô tả địa điểm không chính xác, dẫn đến thời gian chờ và số cuộc gọi giữa tài xế với khách tăng lên.

Công ty thành viên:
 VinFast
 X Xanh SM
 Vinhomes
 Vinmec
 Khác
Ai đang đau (Actor)?
Tài xế.
Khách hàng.
Bộ phận chăm sóc khách hàng.
Workflow thủ công hiện tại:
1. Khách đặt xe và nhập vị trí đón
        ↓
2. Hệ thống gửi vị trí GPS cho tài xế
        ↓
3. Tài xế di chuyển đến vị trí được chỉ định
        ↓
4. Không tìm thấy khách hoặc vị trí không chính xác
        ↓
5. Tài xế gọi/nhắn tin cho khách để xác nhận vị trí
Bước nào tốn thời gian/lỗi nhất?

Bước 3–5: tìm kiếm và xác nhận lại vị trí đón.

Ước tính:

⏱ 3–8 phút cho mỗi trường hợp gặp lỗi.

AI có thể nhảy vào hỗ trợ ở bước nào?

AI có thể:

Phân tích lịch sử các điểm đón thường xảy ra lỗi.
Kết hợp dữ liệu GPS và mô tả văn bản của khách hàng.
Gợi ý điểm đón tối ưu và dễ tiếp cận hơn.
Phát hiện các địa điểm có khả năng gây nhầm lẫn.
Đề xuất điểm đón thay thế gần đó.

Ví dụ:

"Vị trí hiện tại nằm phía sau tòa nhà. Đề xuất điểm đón tại cổng chính, cách vị trí hiện tại 120 m."

Đo thành công bằng gì?

Giảm thời gian tìm điểm đón trung bình từ 5 phút xuống dưới 2 phút và giảm 30% số trường hợp tài xế phải gọi lại cho khách để xác nhận vị trí.

Quick Architecture:
 No AI
 X Rule
 X LLM
 Agent

Nhận xét: Đây có thể là bài toán kết hợp Rule-based + AI. Các quy tắc địa lý đơn giản có thể xử lý bằng code, còn AI phù hợp để hiểu mô tả địa điểm tự nhiên của người dùng.

🃏 QUICK PROBLEM CARD #3
Bài toán (1 câu):

Vinhomes cần tự động phân loại và hỗ trợ xử lý hàng nghìn phản ánh của cư dân để giảm thời gian phản hồi và phân công yêu cầu đến đúng bộ phận.

Công ty thành viên:
 VinFast
 Xanh SM
 X Vinhomes
 Vinmec
 Khác
Ai đang đau (Actor)?
Cư dân.
Nhân viên chăm sóc khách hàng.
Bộ phận vận hành tòa nhà.
Bộ phận kỹ thuật và bảo trì.
Workflow thủ công hiện tại:
1. Cư dân gửi phản ánh
        ↓
2. Nhân viên đọc và hiểu nội dung
        ↓
3. Phân loại vấn đề
        ↓
4. Chuyển yêu cầu đến bộ phận phụ trách
        ↓
5. Soạn phản hồi và theo dõi trạng thái xử lý
Bước nào tốn thời gian/lỗi nhất?

Bước 2–4: đọc, phân loại và chuyển tiếp phản ánh.

Ước tính:

⏱ 5–10 phút cho mỗi phản ánh.

AI có thể nhảy vào hỗ trợ ở bước nào?

AI có thể:

Đọc và hiểu nội dung phản ánh tự nhiên.
Tự động phân loại:
Thang máy.
Vệ sinh.
An ninh.
Bãi đỗ xe.
Điện nước.
Cơ sở vật chất.
Xác định mức độ ưu tiên.
Đề xuất bộ phận xử lý.
Tạo bản nháp phản hồi cho nhân viên.

Ví dụ:

{
  "category": "elevator",
  "priority": "high",
  "department": "maintenance",
  "draft_response": "..."
}
Đo thành công bằng gì?

Giảm thời gian phân loại và chuyển tiếp một phản ánh từ 8 phút xuống dưới 1 phút, đồng thời đạt tỷ lệ phân loại đúng trên 90%.

Quick Architecture:
 No AI
 X Rule
 X LLM
 Agent

Kiến trúc đề xuất:

Resident Message
        ↓
LLM Classification
        ↓
Rule-based Safety & Priority Check
        ↓
Human Approval
        ↓
Department Routing
🎯 Top 3 bài toán được chọn
Rank	Bài toán	                                Lý do chọn
🥇 1	Phân loại và xử lý phản ánh cư dân Vinhomes	Dễ xây dựng prototype bằng      LLM,                                                 dữ liệu đầu vào rõ ràng, metric dễ đo
🥈 2	Tối ưu điểm đón khách Xanh SM	            Có pain point rõ từ tài xế và khách hàng, kết hợp AI + dữ liệu địa lý
🥉 3	Điều phối xe Xanh SM theo nhu cầu	        Tác động kinh doanh lớn nhưng cần nhiều dữ liệu và hệ thống phức tạp hơn