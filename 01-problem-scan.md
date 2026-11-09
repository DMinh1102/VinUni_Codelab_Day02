# Phase 1 & 2 — Problem Scan & Quick Problem Cards
**Đơn vị:** Vin Smart Future (Vingroup)  
**Phân hệ phụ trách:** Vinhomes (Smart Cities & Living) & Vinpearl (Property & Facility Management)  
**Người thực hiện (Member 3):** Nguyễn Tùng Dương  

---

## 🏛️ Bối cảnh & Nhiệm vụ
Tôi là kỹ sư AI Product tại **Vin Smart Future**, được phân công phối hợp cùng Ban Quản lý Vận hành Đô thị **Vinhomes** (đại diện tại các đại đô thị Vinhomes Ocean Park, Smart City, Grand Park) và Khối Quản lý Tiện ích **Vinpearl** nhằm phát hiện các điểm nghẽn (bottlenecks) vận hành thực địa, từ đó áp dụng các giải pháp Trí tuệ Nhân tạo (LLM / Agentic Workflow) để nâng cao chất lượng sống của cư dân và năng suất làm việc của ban quản trị.

---

# 🔍 Phase 1 — SCAN: Bảng quét cơ hội (4 Lenses)

Sử dụng 4 thấu kính (4 Lenses) để rà soát quy trình vận hành hằng ngày tại các công ty thành viên Vinhomes & Vinpearl:

| # | Subsidiary | Lens | Tên bài toán / Bottleneck | Mô tả ngắn bài toán |
|---|------------|------|---------------------------|---------------------|
| 1 | **Vinhomes** | Lặp lại | Phân loại & điều phối yêu cầu cư dân trên Resident App | Cư dân gửi hàng ngàn tin nhắn phản ánh mỗi ngày (mất nước, hỏng đèn, tiếng ồn, đăng ký thi công). Nhân viên CSKH phải đọc thủ công từng tin nhắn và gõ lại ticket chuyển đến từng tổ kỹ thuật (mất 15-20 phút/ticket). |
| 2 | **Vinhomes** | Tốn thời gian | Tra cứu & giải đáp nội quy, chính sách tòa nhà (SOP RAG) | Cư dân liên tục gọi điện/chat hỏi về quy định nuôi thú cưng, giờ giấc chuyển đồ, biểu phí dịch vụ, đăng ký làm thẻ cư dân. CSKH phải tra cứu trong hàng chục file PDF quy chế dài dòng, dẫn đến phản hồi chậm (trung bình 2-4 tiếng). |
| 3 | **Vinhomes** | Pain từ người khác | Tiếp nhận & thẩm định hồ sơ đăng ký thi công nội thất căn hộ | Cư dân và nhà thầu nộp bản vẽ và hồ sơ thi công qua app. Kỹ sư ban quản lý mất 3-5 ngày để đọc soát lỗi vi phạm quy chuẩn an toàn (kết cấu chịu lực, PCCC) gây chậm tiến độ dọn vào ở và cư dân bức xúc. |
| 4 | **Vinpearl** | Tốn thời gian | Tự động hóa xử lý email booking đoàn (Group Booking) | Nhân viên Sales/Lễ tân mất 30-45 phút để đọc các email yêu cầu đặt phòng đoàn phức tạp (nhiều loại phòng, ngày check-in/out lệch nhau, yêu cầu ăn uống) để đối chiếu quỹ phòng trống và soạn báo giá. |
| 5 | **Vinpearl** | Pain từ người khác | Tổng hợp & cảnh báo khẩn cấp từ Review khách hàng | Review từ Google Maps, TripAdvisor, OTA đổ về liên tục. Quản lý không kịp phát hiện các phản hồi tiêu cực nghiêm trọng (vệ sinh kém, thái độ nhân viên) trong vòng 2 giờ đầu để xử lý khủng hoảng kịp thời. |
| 6 | **Vinhomes** | AI-upgrade | Dự đoán tải năng lượng & tối ưu điều hòa/chiếu sáng khu vực công cộng | Hệ thống HVAC và chiếu sáng hành lang các tòa nhà vận hành theo lịch cố định, không thích ứng với mật độ cư dân và nhiệt độ thực tế bên ngoài, gây lãng phí 15-20% điện năng công cộng. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

Chọn lọc Top 3 bài toán tiềm năng nhất từ danh sách SCAN: **#1 (Vinhomes Triage phản ánh), #2 (Vinhomes SOP RAG), #4 (Vinpearl Group Booking)**.

---

### 📇 QUICK PROBLEM CARD #1: Resident Super-App Triage Agent

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                                       │
│                                                                             │
│ Bài toán (1 câu): Phân loại tự động, trích xuất độ khẩn cấp (Urgency) và   │
│ điều phối phản ánh cư dân trên Vinhomes Resident App đến đúng đội kỹ thuật. │
│ Công ty thành viên: [x] Vinhomes   [ ] Vinpearl   [ ] VinFast               │
│                                                                             │
│ Ai đang đau (Actor)?                                                        │
│ - Nhân viên CSKH / Lễ tân: Quá tải vì phải đọc và gán thủ công 1.200+        │
│   tin nhắn/ngày bằng ngôn từ tự do, thiếu cấu trúc của cư dân.              │
│ - Cư dân: Chờ đợi phản hồi lâu (4-8 tiếng), sự cố khẩn cấp (rò rỉ nước,     │
│   chập điện) không được phát hiện kịp thời gây thiệt hại tài sản.           │
│                                                                             │
│ Workflow thủ công hiện tại (5 bước):                                        │
│   1. Cư dân gửi phản ánh tự do qua App (kèm ảnh/video)                      │
│   → 2. CSKH đọc tin nhắn, liên hệ lại cư dân nếu thiếu thông tin (phòng, tầng)│
│   → 3. Xác định mức độ khẩn cấp (Khẩn / Cao / Bình thường)                  │
│   → 4. Tạo ticket nội bộ trên hệ thống CRM và gán bộ phận kỹ thuật phù hợp  │
│   → 5. Soạn tin nhắn phản hồi báo cư dân đã tiếp nhận yêu cầu               │
│                                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ 15 phút/ticket)             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2, 3 & 5                         │
│ (Trích xuất Intent, Location, Urgency -> Tự động draft ticket & phản hồi)   │
│                                                                             │
│ Đo thành công bằng gì (Metric có số)?                                       │
│ - Giảm thời gian phân loại & tạo ticket từ 15 phút ──> dưới 30 giây.        │
│ - Tỉ lệ gán đúng tổ kỹ thuật đạt trên 95%.                                  │
│ - 100% sự cố khẩn cấp (nguy cơ an toàn, PCCC) được route tức thì (< 1 phút). │
│                                                                             │
│ Quick Architecture: [x] LLM Feature (Trích xuất & Draft) + Rule Guardrails │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

### 📇 QUICK PROBLEM CARD #2: SOP & Regulation RAG Assistant

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                                       │
│                                                                             │
│ Bài toán (1 câu): Trợ lý ảo RAG tra cứu nội quy, quy chế tòa nhà và giải đáp│
│ thắc mắc biểu phí cho cư dân Vinhomes dựa trên kho tài liệu pháp quy chuẩn.  │
│ Công ty thành viên: [x] Vinhomes   [ ] Vinpearl                             │
│                                                                             │
│ Ai đang đau (Actor)?                                                        │
│ - Cư dân mới dọn về: Bối rối về các quy định đăng ký tạm trú, giờ giấc thi │
│   công, phí dịch vụ xe điện, khu vực nướng BBQ.                             │
│ - Nhân viên lễ tân: Trả lời lặp đi lặp lại hàng trăm câu hỏi giống nhau      │
│   mỗi ngày, tốn 40% thời gian trực quầy.                                    │
│                                                                             │
│ Workflow thủ công hiện tại (4 bước):                                        │
│   1. Cư dân gọi điện hoặc nhắn tin hỏi quy định                             │
│   → 2. Lễ tân tra cứu sổ tay nội quy PDF dài 200+ trang                    │
│   → 3. Soạn câu trả lời kèm trích dẫn điều khoản                            │
│   → 4. Gửi giải đáp cho cư dân                                              │
│                                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (⏱ 10 phút/câu hỏi)             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 3                            │
│ (RAG tra cứu chính xác tài liệu nội bộ và trích nguồn minh bạch)            │
│                                                                             │
│ Đo thành công bằng gì (Metric có số)?                                       │
│ - Tự động hóa giải đáp 80% câu hỏi thường gặp về nội quy.                   │
│ - Thời gian phản hồi giảm từ 10 phút ──> dưới 5 giây.                       │
│ - Tỉ lệ câu trả lời chuẩn xác 100% không bịa đặt chính sách (Zero Hallucination).│
│                                                                             │
│ Quick Architecture: [x] LLM Feature (RAG Tra cứu & Trích dẫn)              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

### 📇 QUICK PROBLEM CARD #3: Vinpearl Group Booking & Facility Coordinator

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                                       │
│                                                                             │
│ Bài toán (1 câu): Đọc hiểu email đặt tour đoàn phức tạp, đối chiếu quỹ phòng│
│ và soạn thảo báo giá sơ bộ kèm gợi ý dịch vụ ẩm thực tại Vinpearl.          │
│ Công ty thành viên: [ ] Vinhomes   [x] Vinpearl                             │
│                                                                             │
│ Ai đang đau (Actor)? Nhân viên kinh doanh MICE (Meetings & Events) Vinpearl.│
│                                                                             │
│ Workflow thủ công hiện tại (4 bước):                                        │
│   1. Nhận email đặt đoàn (chứa file Excel danh sách khách, yêu cầu sự kiện) │
│   → 2. Mở phần mềm Opera/PMS đối chiếu số lượng phòng trống theo từng ngày  │
│   → 3. Tính toán biểu giá chiết khấu theo chính sách mùa vụ                 │
│   → 4. Viết email báo giá và đề xuất thực đơn tiệc                          │
│                                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 4 (⏱ 35 phút/email)              │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 1, 2 & 4                         │
│ (Trích xuất entity từ email -> Draft báo giá vào PMS)                       │
│                                                                             │
│ Đo thành công bằng gì (Metric có số)?                                       │
│ - Giảm thời gian phản hồi yêu cầu đặt đoàn từ 4 tiếng ──> dưới 30 phút.     │
│ - Giảm 90% lỗi nhầm lẫn ngày check-in/out của khách đoàn.                   │
│                                                                             │
│ Quick Architecture: [x] LLM + System Integration                            │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

# 🗳️ Quyết định lựa chọn bài toán Deep-Dive

Nhóm quyết định chọn **Quick Problem Card #1: Resident Super-App Triage Agent (Phân loại & điều phối phản ánh cư dân Vinhomes)** để tiến hành phân tích sâu (Deep-Dive).

### Lý do lựa chọn và loại trừ:
1. **Vì sao chọn Card #1:** 
   - Đây là điểm nghẽn nghiêm trọng nhất ảnh hưởng trực tiếp đến chất lượng sống của hơn 300.000 cư dân Vinhomes.
   - Các sự cố an toàn (cháy nổ, vỡ đường ống nước, kẹt thang máy) đòi hỏi tính thời gian thực (real-time) và phân loại độ khẩn cấp tức thì.
   - Giá trị kinh doanh vượt trội: Tiết kiệm hàng ngàn giờ công của đội ngũ CSKH và ngăn ngừa tổn thất tài sản hàng tỷ đồng nếu sự cố hạ tầng được can thiệp sớm.
2. **Vì sao tạm gác Card #2 và #3:**
   - *Card #2 (SOP RAG):* Mặc dù hữu ích nhưng rủi ro tranh chấp pháp lý/biểu phí với cư dân rất nhạy cảm; cần chuẩn hóa kho cơ sở dữ liệu pháp lý và thiết lập hệ thống vector index chặt chẽ hơn trước khi triển khai.
   - *Card #3 (Vinpearl Booking):* Đây là bài toán mang tính thời vụ, quy trình phụ thuộc lớn vào việc đàm phán giá linh hoạt của nhân viên kinh doanh, mức độ chuẩn hóa chưa cao bằng quy trình xử lý ticket của Vinhomes.

