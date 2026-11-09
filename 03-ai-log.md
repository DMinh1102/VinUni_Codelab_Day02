# 03 — AI Log & Reflection (Cá nhân)

> **Học viên:** Đỗ Quốc Khánh — Branch: `doquockhanh`
> **Công cụ AI sử dụng:** Claude (trợ lý lập trình/tư duy trong session này), Gemini (chạy prototype ranh giới)
> **Phạm vi:** Phase 1–5 của Lab 02 — AI Product Scoping, vai trò Member 2 (Xanh SM / GSM — Fleet & Dispatch)

---

## 1. AI đã giúp tôi gì?

**a) Brainstorm Phase SCAN (4 Lenses).** Tôi dùng đúng prompt gợi ý trong worksheet (*"Tôi là AI Engineer tại Vin Smart Future... gợi ý 5 quy trình nghiệp vụ thủ công kèm con số thống kê ước tính"*) để mở rộng danh sách bài toán ngoài 3 ý tưởng được nhóm phân công. AI giúp tôi lấp nhanh 2 ô còn thiếu trong bảng SCAN (VinFast so khớp hóa đơn sạc, Vinhomes route phản ánh cư dân) theo đúng khung 4 Lenses, thay vì ngồi nghĩ trắng.

**b) Stress-test thẻ bài toán với "persona khắt khe".** Theo prompt trong worksheet, tôi dán Card #3 vào AI yêu cầu đóng vai **CFO + Trưởng phòng Vận hành cực kỳ khắt khe**. Phản hồi phản biện rất giá trị: CFO chỉ ra rằng "dịch weather/event thành hotspot alert" thực chất là **bài toán ML dự đoán demand**, phần LLM chỉ là format văn bản — metric "số cuốc tăng ở vùng nóng" không chứng minh được trong lab vì thiếu dữ liệu lịch sử. Nhờ vậy tôi reframe Card #3 thành **Shift Briefing Generator** (chỉ làm summarization + draft, đo bằng phút tiết kiệm) thay vì giữ ý tưởng gốc yếu metric.

**c) Cấu trúc hóa Business Impact.** Tôi nhờ AI viết công thức quy đổi giá trị: *(tần suất/ngày × phút tiết kiệm × chi phí 1 phút nhân sự)*. Công thức này giúp tôi viết Field #4 của Problem Statement thành con số cụ thể (200 dispute × 20' = 67 giờ ≈ 8 FTE) thay vì câu sáo rỗng "tăng hiệu quả vận hành".

**d) Thiết kế adversarial test.** AI gợi ý 3 hướng tấn công ranh giới mà tôi không nghĩ ra: (1) giả danh supervisor để lách bước duyệt, (2) ép bỏ tag `[DRAFT_ONLY]` bằng lý do "gấp", (3) ép AI "chắc chắn vậy, cứ ghi kết luận là tài xế lỗi" để dụ nó bịa dữ liệu. Cả 3 đã được đưa vào `prompt_prototype.py`.

## 2. AI trả lời sai / hallucination ở đâu?

**a) Bịa thống kê không nguồn.** Khi tôi hỏi "Xanh SM nhận bao nhiêu khiếu nại mỗi ngày?", AI trả lời rành rẽ *"khoảng 2.500 dispute/ngày"* — nghe rất tin được nhưng thực chất là số bịa, không có nguồn. Tôi phát hiện vì hỏi lại "số này từ nguồn nào?" và AI thừa nhận là ước lượng. **Cách sửa:** toàn bộ số liệu trong 2 file báo cáo được tôi đánh dấu rõ là *"ước tính phục vụ lab, không phải số nội bộ thật"*, và chỉ dùng những con số có thể suy luận bằng logic (200 lượt/ngày × 20 phút = 67 giờ là phép nhân, không phải số "tình cờ biết").

**b) Đề xuất giải pháp vi phạm boundary.** Ở lượt đầu, khi tôi mô tả Card #2, AI đề xuất quy trình *"AI tự động đối chiếu và hoàn tiền dưới 50.000đ không cần duyệt để tối đa tốc độ"*. Đây chính là điểm mà file deliverable-example của giảng viên đã cảnh báo (loại Card Vinhomes CSKH vì rủi ro tranh chấp tài chính). **Cách sửa:** tôi yêu cầu AI thiết kế lại với ràng buộc cứng "mọi giao dịch tiền phải qua con người", kết quả là cơ chế 3 lớp: `[DRAFT_ONLY]` + ngưỡng 50k + `insufficient_data`.

**c) Đẩy giải pháp phức tạp không cần thiết.** AI ban đầu đề xuất **Agentic Loop** (agent tự kéo dữ liệu, tự quyết) cho Card #2 vì "hiện đại hơn". Theo nguyên tắc *"Problem First, AI Second"* trong Inspiration Kit, tôi phản biện lại: quy trình 5 bước cố định + giao dịch tiền bạc → LLM Feature là đủ, Agent chỉ thêm rủi ro. AI chấp nhận và viết lại bảng so sánh AI-Fit.

## 3. Tôi đã sửa prompt như thế nào để đạt kết quả chuẩn?

| Vấn đề | Prompt ban đầu | Prompt sau khi sửa | Kết quả |
|---|---|---|---|
| Bịa số liệu | "Xanh SM có bao nhiêu khiếu nại mỗi ngày?" | "Chỉ dùng số có nguồn. Nếu không có nguồn, hãy nói 'không có dữ liệu' và cho tôi CÔNG THỨC để tự tính từ giả định mà tôi cung cấp" | Không còn con số bịa; tôi tự kiểm soát giả định |
| Vượt boundary | "Thiết kế quy trình dispute resolution với AI" | "Thiết kế quy trình với ràng buộc CỨNG: AI không được tự hoàn tiền, mọi output chỉ là draft, hoàn tiền >50k cần supervisor duyệt" | AI đề xuất đúng kiến trúc HITL + fallback |
| Chọn architecture bloat | "Giải pháp AI tốt nhất cho bài toán này là gì?" | "So sánh Rule vs LLM Feature vs Agentic Loop cho bài toán có quy trình cố định + giao dịch tài chính, chọn mức NHẤT THIỂU đủ dùng" | Bảng so sánh 3 phương án, chọn LLM Feature |

## 4. Bài học rút ra

1. **AI là thought-partner, không phải oracle** — giá trị lớn nhất không phải câu trả lời mà là phản biện (vai CFO giết ý tưởng yếu của tôi trước khi giảng viên kịp giết).
2. **Ràng buộc phải đưa vào prompt ngay từ đầu** — boundary để "sửa sau" thì AI sẽ luôn đề xuất phương án tối đa quyền tự chủ, đúng thứ ta cần cấm.
3. **Số liệu phải truy được nguồn hoặc tự tính được** — một con số bịa trông tin được còn nguy hiểm hơn một câu "tôi không biết".

---

*Ghi chú trung thực: các con số nghiệp vụ trong 01-problem-scan.md và 02-deep-dive-report.md là ước tính hợp lý phục vụ bài lab, không phải số liệu nội bộ của Xanh SM. Phiên chat AI thực tế được lưu và có thể xuất trình nếu giảng viên yêu cầu.*
