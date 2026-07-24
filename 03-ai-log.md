### 3. File `03-ai-log.md`

```markdown
# 03. AI Usage & Collaboration Log

## 1. Tools & Models Used
- **AI Platform:** Google Gemini / ChatGPT
- **SDK Used:** `google-genai` / `google-generativeai`
- **Model Standard:** `gemini-1.5-flash`

## 2. Interaction Log

### Session 1: Sửa lỗi 404 Model Not Found
- **Prompt từ Người dùng:** *"Chạy script báo lỗi `404 NOT_FOUND: This model models/gemini-2.5-flash is no longer available...`"*
- **Giải pháp từ AI:** AI phát hiện tên model `gemini-2.5-flash` chưa/không được hỗ trợ công khai trên API endpoint tiêu chuẩn. AI hướng dẫn thay đổi cấu hình `GEMINI_MODEL = "gemini-1.5-flash"` hoặc `"gemini-2.0-flash"`.
- **Kết quả:** Code thực thi mượt mà, kết nối API thành công.

### Session 2: Tối ưu hoá System Prompt cho Rule 2 (Battery < 5%)
- **Prompt từ Người dùng:** *"Làm sao để chắc chắn Gemini trả về JSON cứu hộ xe sạc di động khi pin < 5% thay vì hướng dẫn đi trạm sạc?"*
- **Giải pháp từ AI:** Thiết kế Prompt có cấu trúc rõ ràng (Strict Rules), bổ sung điều kiện phản ví dụ (Negative Constraints) và ép khuôn mẫu JSON đầu ra ngay sau thẻ `[DRAFT_ONLY]`.
- **Kết quả:** AI vượt qua các bài Test Case tấn công (Adversarial Tests) đạt 100% tỷ lệ tuân thủ.

## 3. Reflection (Đánh giá & Rút kinh nghiệm)
- AI hỗ trợ rất tốt trong việc khoanh vùng lỗi môi trường SDK và tối ưu hóa Prompt theo tư duy Defensive Prompting.
- Việc kiểm thử cẩn thận bằng các Adversarial Test Cases giúp phát hiện điểm yếu của Prompt trước khi đưa vào sản phẩm thực tế.