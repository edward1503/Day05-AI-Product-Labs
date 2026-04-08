# SPEC draft — Nhom02-403

## Track: VinSchool

## Problem statement
Học sinh, sinh viên thường bị mất tập trung và đứt gãy luồng tư duy khi phải chuyển đổi giữa giao diện bài giảng (LMS, Video player, Slide) và các công cụ tìm kiếm/AI bên ngoài để giải đáp thắc mắc.

Mục tiêu: Xây dựng một AI Tutor "lớp phủ" (overlay) có khả năng hiểu ngữ cảnh hiện tại của bài giảng để trả lời câu hỏi ngay lập tức mà không cần thay đổi giao diện người dùng.

## Canvas draft

| | Value | Trust | Feasibility |
|---|-------|-------|-------------|
| Trả lời | Sinh viên gặp khái niệm khó trong slide/video. Pain: Tốn 2-3 phút search + chuyển tab gây xao nhãng. AI: Giải thích dựa trên chính nội dung đang hiển thị (OCR slide hoặc Metadata video). | Nếu AI giải thích sai kiến thức chuyên môn hoặc ảo giác (hallucination) → Sinh viên hổng kiến thức. Cần có nút "Nguồn tham khảo" dẫn tới đoạn video/trang slide tương ứng. | Sử dụng Gemini/GPT-4o API để xử lý hình ảnh (Vision) hoặc text từ slide. Latency cần < 2s để giữ mạch học. Thách thức: Video dài cần xử lý transcript theo timestamp. |

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
- A: Canvas
- B: failure modes
- C: User stories 4 paths
- D: Eval metrics + ROI
- E: Prototype research + prompt test