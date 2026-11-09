# 🔍 Deliverable Phase 1 & 2 — Problem Scan & Quick Cards

> **Đơn vị:** Vin Smart Future (Vingroup)  
> **Người thực hiện:** Phạm Quốc Huy (Member — Healthcare & Smart Living Stream)  
> **Phân hệ trọng tâm:** **Hệ thống Y tế Vinmec** & **Đô thị thông minh Vinhomes**  
> **Deliverable:** Gate I1 — Scan & Cards (15 điểm cá nhân)

---

## 🏛️ Bối cảnh & Vai trò

Tôi là kỹ sư AI Product tại **Vin Smart Future**, đơn vị công nghệ của Tập đoàn Vingroup. Nhóm chúng tôi được phân công khảo sát vận hành thực tế tại **Bệnh viện Đa khoa Quốc tế Vinmec** và Ban Quản lý Đô thị **Vinhomes** nhằm phát hiện các điểm nghẽn (bottlenecks) hành chính, từ đó thiết kế giải pháp AI (LLM / RAG) giúp giảm tải gánh nặng thủ tục giấy tờ cho đội ngũ y bác sĩ, nâng cao an toàn điều trị và trải nghiệm của người bệnh.

---

# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội (Cá nhân)

Dùng **4 Lenses** (Lặp lại, Tốn thời gian, AI-upgrade, Stakeholder Pain) quét qua vận hành của các công ty thành viên Vingroup:

| # | Subsidiary | Lens | Tên bài toán / Bottleneck | Mô tả ngắn bài toán |
|---|------------|------|---------------------------|---------------------|
| 1 | **Vinmec** | Tốn thời gian | Tóm tắt hồ sơ bệnh án xuất viện (Discharge Summary) | Bác sĩ phải tổng hợp thông tin từ bệnh án điện tử (EMR), kết quả xét nghiệm, chẩn đoán và đơn thuốc để viết hồ sơ tóm tắt xuất viện. Việc tra cứu và nhập liệu thủ công chiếm 16/20 phút/ca, gây quá tải giờ làm việc của bác sĩ. |
| 2 | **Vinmec** | Lặp lại | Đối chiếu hồ sơ bảo lãnh viện phí & bảo hiểm | Nhân viên bảo hiểm phải kiểm tra quyền lợi, đối chiếu thông tin bệnh nhân, mã dịch vụ, chỉ định và hồ sơ y tế để hoàn thiện yêu cầu bảo lãnh viện phí hoặc thanh toán bảo hiểm (mất 20 phút/hồ sơ). |
| 3 | **Vinmec** | Pain từ người khác | Phân luồng & gợi ý chuyên khoa khám ban đầu | Nhân viên tiếp nhận phải đọc và phân loại nhu cầu khám bệnh từ cuộc gọi hoặc tin nhắn của bệnh nhân để chuyển đến đúng chuyên khoa, gây chậm trễ khi lượng yêu cầu lớn và triệu chứng mơ hồ. |
| 4 | **Vinhomes** | Lặp lại | Phân loại & điều phối phản ánh cư dân trên Resident App | Ban quản lý phải tiếp nhận, đọc, phân loại và xác định mức độ ưu tiên các phản ánh của cư dân (mất nước, hỏng thang máy, rò rỉ điện, vệ sinh) trước khi chuyển đến đội kỹ thuật phụ trách. |
| 5 | **Vinhomes** | Tốn thời gian | Thẩm định hồ sơ đăng ký thi công nội thất căn hộ | Nhân viên ban quản lý phải kiểm tra thủ công hồ sơ đăng ký thi công nội thất, thông tin nhà thầu, giấy tờ và danh mục yêu cầu an toàn PCCC trước khi phê duyệt hoặc yêu cầu bổ sung (mất 3–5 ngày). |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards (Cá nhân)

Chọn top 3 từ danh sách SCAN: **#1 (Vinmec – AI Tóm tắt hồ sơ xuất viện), #2 (Vinmec – AI Đối chiếu hồ sơ bảo hiểm), #5 (Vinhomes – AI Phân loại và xử lý phản ánh cư dân).**

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Bác sĩ phải tổng hợp thủ công thông tin từ bệnh   │
│ án điện tử, kết quả xét nghiệm, chẩn đoán và đơn thuốc để   │
│ viết hồ sơ tóm tắt xuất viện cho bệnh nhân.                 │
│                                                             │
│ Công ty thành viên: [x] Vinmec                              │
│                                                             │
│ Ai đang đau? Bác sĩ điều trị (mất thời gian tổng hợp),      │
│ điều dưỡng (hỗ trợ hoàn thiện hồ sơ), bệnh nhân (chờ        │
│ hoàn tất thủ tục xuất viện).                                │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Bác sĩ mở và kiểm tra hồ sơ bệnh án điện tử            │
│   → 2. Tra cứu kết quả xét nghiệm, chẩn đoán và diễn biến   │
│       điều trị                                              │
│   → 3. Tổng hợp thông tin thuốc và phương pháp điều trị     │
│   → 4. Tự viết nội dung tóm tắt xuất viện                   │
│   → 5. Kiểm tra, chỉnh sửa và hoàn thiện hồ sơ              │
│                                                             │
│ Bước nào tốn nhất? Bước 2-4 (⏱ 16/20 phút/hồ sơ)            │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-4              │
│ (Truy xuất thông tin bệnh án -> Tóm tắt diễn biến điều trị  │
│ -> Tạo bản nháp hồ sơ xuất viện theo mẫu chuẩn).            │
│ Bác sĩ kiểm tra và phê duyệt trước khi lưu chính thức.      │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian soạn hồ sơ từ 20 phút -> dưới 5 phút/hồ sơ.  │
│ Mục tiêu giảm ít nhất 75% thời gian soạn thảo.              │
│                                                             │
│ Quick Architecture: [ ] No AI [ ] Rule [x] LLM [ ] Agent    │
│ (LLM kết hợp RAG truy xuất bệnh án, sinh bản nháp có cấu    │
│ trúc; bác sĩ chịu trách nhiệm kiểm tra nội dung cuối cùng). │
└─────────────────────────────────────────────────────────────┘
```

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Nhân viên bảo hiểm Vinmec phải kiểm tra và đối    │
│ chiếu thủ công thông tin bệnh nhân, quyền lợi bảo hiểm,     │
│ mã dịch vụ và chứng từ y tế trước khi gửi yêu cầu           │
│ bảo lãnh viện phí hoặc thanh toán bảo hiểm.                 │
│                                                             │
│ Công ty thành viên: [x] Vinmec                              │
│                                                             │
│ Ai đang đau? Nhân viên bảo hiểm (xử lý hồ sơ lặp lại),      │
│ kế toán viện phí (chờ xác nhận), bệnh nhân (chờ bảo lãnh).  │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Tiếp nhận hồ sơ và thông tin bảo hiểm bệnh nhân        │
│   → 2. Kiểm tra quyền lợi và điều kiện bảo lãnh             │
│   → 3. Đối chiếu mã dịch vụ, chỉ định và chứng từ y tế      │
│   → 4. Kiểm tra giấy tờ thiếu hoặc thông tin không khớp     │
│   → 5. Gửi yêu cầu bảo lãnh hoặc liên hệ bổ sung hồ sơ      │
│                                                             │
│ Bước nào tốn nhất? Bước 2-4 (⏱ 20 phút/hồ sơ)              │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 1-4              │
│ (OCR trích xuất dữ liệu -> LLM phân loại chứng từ và phát   │
│ hiện thông tin thiếu -> Rule engine đối chiếu điều kiện     │
│ bảo hiểm -> Tạo bản nháp yêu cầu bảo lãnh).                 │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian kiểm tra hồ sơ từ 20 phút -> dưới 8 phút.    │
│ Mục tiêu giảm ít nhất 60% thời gian xử lý hồ sơ.            │
│                                                             │
│ Quick Architecture: [ ] No AI [x] Rule [x] LLM [ ] Agent    │
│ (OCR + LLM trích xuất, phân loại chứng từ; Rule engine      │
│ kiểm tra điều kiện và đối chiếu quyền lợi bảo hiểm).        │
└─────────────────────────────────────────────────────────────┘
```

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #5                                       │
│                                                             │
│ Bài toán: Ban quản lý Vinhomes phải đọc, phân loại, xác     │
│ định mức độ ưu tiên và chuyển phản ánh của cư dân đến       │
│ đúng bộ phận phụ trách để xử lý sự cố.                      │
│                                                             │
│ Công ty thành viên: [x] Vinhomes                            │
│                                                             │
│ Ai đang đau? Nhân viên CSKH (quá tải phản ánh),             │
│ nhân viên kỹ thuật (nhận yêu cầu phân loại sai),            │
│ cư dân (chờ phản hồi và xử lý sự cố).                       │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Cư dân gửi phản ánh qua ứng dụng Resident hoặc tổng đài│
│   → 2. Nhân viên đọc và kiểm tra nội dung phản ánh          │
│   → 3. Phân loại sự cố (điện, nước, thang máy, vệ sinh...)  │
│   → 4. Xác định mức độ ưu tiên và chuyển bộ phận phụ trách  │
│   → 5. Theo dõi tiến độ và cập nhật kết quả cho cư dân      │
│                                                             │
│ Bước nào tốn nhất? Bước 2-4 (⏱ 5 phút/phản ánh)            │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-4              │
│ (NLP phân loại nội dung -> Phát hiện phản ánh trùng lặp     │
│ -> Đề xuất mức độ ưu tiên -> Tự động gợi ý bộ phận xử lý).  │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian phân loại và chuyển phản ánh từ 5 phút       │
│ -> dưới 1 phút/yêu cầu. Mục tiêu giảm ít nhất 80%.          │
│                                                             │
│ Quick Architecture: [ ] No AI [x] Rule [x] LLM [ ] Agent    │
│ (LLM/NLP hiểu nội dung phản ánh; Rule engine xử lý mức độ   │
│ khẩn cấp, SLA và quy tắc phân công theo khu vực, bộ phận).  │
└─────────────────────────────────────────────────────────────┘
```

---

# 🗳️ Quyết định lựa chọn bài toán Deep-Dive (Nhóm)

Nhóm thống nhất lựa chọn **Quick Problem Card #1: Vinmec – AI Hỗ trợ Soạn thảo & Tóm tắt Hồ sơ Bệnh án Xuất viện (Discharge Summary Co-Pilot)** để tiến hành phân tích sâu.

### 📌 Lý do lựa chọn và loại trừ:
1. **Vì sao chọn Card #1 (Vinmec Discharge Summary):**
   * **Giá trị kinh tế & vận hành cực lớn:** Bác sĩ là tài nguyên nhân lực quý giá và đắt đỏ nhất của Vinmec. Giảm từ 20 phút xuống dưới 5 phút/hồ sơ giúp giải phóng hơn **116 giờ công của bác sĩ mỗi ngày** trên toàn hệ thống 7 bệnh viện Vinmec, cho phép bác sĩ dành nhiều thời gian hơn cho việc thăm khám và điều trị bệnh nhân.
   * **Độ chín muồi công nghệ (AI-Fit hoàn hảo):** Bài toán RAG + LLM Feature tổng hợp văn bản y tế từ bệnh án điện tử (EMR) có cấu trúc cố định, không đòi hỏi huấn luyện lại mô hình nền mà chỉ cần trích xuất chính xác theo mẫu chuẩn của Bộ Y Tế và Vinmec.
   * **Kiểm soát rủi ro y tế chặt chẽ (HITL 100%):** Ranh giới an toàn được thiết lập nghiêm ngặt: AI tuyệt đối không tự chẩn đoán, không tự sửa đơn thuốc, và chỉ tạo bản nháp (draft); bác sĩ điều trị bắt buộc phải kiểm tra và ký số duyệt mới được lưu vào EMR.
2. **Vì sao tạm gác Card #2 và Card #5:**
   * *Card #2 (Đối chiếu bảo hiểm Vinmec):* Quy trình phụ thuộc vào cổng API và danh mục mã thanh toán của hàng chục công ty bảo hiểm tư nhân bên ngoài (Bảo Việt, Prudential, PVI...), mức độ phụ thuộc bên thứ ba rất cao, khó kiểm soát trong khuôn khổ triển khai ban đầu.
   * *Card #5 (Phân loại phản ánh Vinhomes):* Mức độ cấp bách và tổn thất chi phí thấp hơn nhiều so với việc giảm tải thời gian cho bác sĩ tại bệnh viện.

---

## 📌 Các bước tiếp theo (Next Deliverables):
* 🏗️ **Phase 3 (Deep-Dive), Phase 4 (Prompt Prototype) & Phase 5 (Evaluate):** Toàn bộ phân tích sâu chi tiết và báo cáo kỹ thuật được trình bày tại file **[02-deep-dive-report.md](02-deep-dive-report.md)**.
* 📊 **Sơ đồ Quy trình Vận hành (Workflow Mapping Diagram):** Xem sơ đồ trực quan tại file **[04-workflow-diagram.png](04-workflow-diagram.png)**.
* 📝 **Phase 6 — AI Log & Reflection:** Toàn bộ nhật ký cá nhân về quá trình sử dụng AI làm Thought-Partner được ghi lại chi tiết tại file **[03-ai-log.md](03-ai-log.md)**.
