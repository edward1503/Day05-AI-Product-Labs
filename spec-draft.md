# SPEC draft — Nhom02-403

## Track: VinSchool

## Problem statement
Học sinh, sinh viên thường bị mất tập trung và đứt gãy luồng tư duy khi phải chuyển đổi giữa giao diện bài giảng (LMS, Video player, Slide) và các công cụ tìm kiếm/AI bên ngoài để giải đáp thắc mắc.

Mục tiêu: Xây dựng một AI Tutor "lớp phủ" (overlay) có khả năng hiểu ngữ cảnh hiện tại của bài giảng để trả lời câu hỏi ngay lập tức mà không cần thay đổi giao diện người dùng.

## Canvas draft

| | Value | Trust | Feasibility |
|---|-------|-------|-------------|
| 1 | Sinh viên gặp khái niệm khó trong slide/video. Pain: Tốn 2-3 phút search + chuyển tab gây xao nhãng. AI: Giải thích dựa trên chính nội dung đang hiển thị (OCR slide hoặc Metadata video). | Nếu AI giải thích sai kiến thức chuyên môn hoặc ảo giác (hallucination) → Sinh viên hổng kiến thức. Cần có nút "Nguồn tham khảo" dẫn tới đoạn video/trang slide tương ứng. | Sử dụng Gemini/GPT-4o API để xử lý hình ảnh (Vision) hoặc text từ slide. Latency cần < 2s để giữ mạch học. Thách thức: Video dài cần xử lý transcript theo timestamp. |
| 2 | “Just-in-time learning” AI không chỉ trả lời, mà trả lời đúng thời điểm user cần nhất - Khi user hover / pause → AI proactively gợi ý: “Bạn có muốn hiểu khái niệm này không?” | Giảm friction xuống gần 0 (không cần gõ câu hỏi) “AI xuất hiện đúng lúc bạn bắt đầu không hiểu”. | Nếu không có context → AI nói: “Không tìm thấy thông tin trong slide/video hiện tại”, tránh hallucination hoàn toàn | 5|

**Auto hay aug?** Augmentation — AI hỗ trợ giải thích và gợi ý mở rộng, sinh viên vẫn là người chủ động tiếp thu và đặt câu hỏi.

**Learning signal:** 
- Tỷ lệ sinh viên nhấn "Đã hiểu" sau câu trả lời
- Thời gian sinh viên ở lại giao diện bài giảng sau khi hỏi (so với việc thoát ra ngoài).
- Câu hỏi follow-up: Nếu sinh viên hỏi lại cùng một ý → Câu trả lời trước chưa đạt.

## Hướng đi chính
- Prototype: chatbot hỏi đáp trực tiếp theo tiến trình học của người dùng
- Eval: Độ chính xác nội dung (so với transcript bài giảng) ≥ 85%.
- Main failure mode: Video không có transcript khiến AI thiếu ngữ cảnh sâu của toàn bộ bài giảng.

## Phân công
- Quân: failure modes
- Đức: User stories 4 paths
- Phúc: Eval metrics + ROI
- Hoàng: Prototype research + prompt test