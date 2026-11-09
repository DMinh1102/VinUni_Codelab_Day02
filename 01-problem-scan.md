# 01 — Problem Scan & Quick Assessment (Cá nhân)

> **Học viên:** Đỗ Quốc Khánh — Branch: `doquockhanh`
> **Vai trò trong nhóm:** Member 2 — **Xanh SM / GSM (Fleet & Dispatch)**
> **Overlap dữ liệu:** Vehicle Telemetry VinFast (mức pin, vị trí GPS, log hành trình)

---

# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội (Cá nhân)

Dùng **4 Lenses** quét qua vận hành của các công ty thành viên Vingroup, ưu tiên mảng Fleet & Dispatch của Xanh SM.

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **Xanh SM** | Tốn thời gian | Điều phối viên tra cứu thủ công trạm sạc VinFast còn trụ trống và soạn chỉ dẫn khi tài xế báo pin thấp (10–12 phút/lượt, ~80 lượt/ngày tại Hà Nội). |
| 2 | **Xanh SM** | AI có thể tốt hơn | CSKH xử lý khiếu nại cước/lộ trình bằng cách đọc tay trip log, GPS trace và chat transcript để đối chiếu lời kể khách (20 phút/lượt, ~200 lượt/ngày toàn mạng). |
| 3 | **Xanh SM** | Pain từ người khác | Tài xế đầu ca không được briefing về mưa/sự kiện/giờ cao điểm → xe dồn sai vùng, hụt cuốc ngay lúc nhu cầu bùng nổ. |
| 4 | **VinFast** | Lặp lại | So khớp hóa đơn sạc điện từ hàng nghìn trụ sạc đối tác ngoài với dữ liệu telemetry thực tế hằng tuần. |
| 5 | **VinFast** | AI có thể tốt hơn | Phân loại mã lỗi kỹ thuật ban đầu từ mô tả tiếng Việt đời thường của khách (VD: *"xe đi qua gờ giảm tốc kêu cụp cụp bánh trước"*). |
| 6 | **Vinhomes** | Lặp lại | Phân loại & route tự động phản ánh cư dân trên App Resident đến đúng ban quản lý từng tòa nhà. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards (Cá nhân)

Chọn top 3 từ danh sách SCAN đúng phạm vi được phân công: **#1 (Dispatch Co-pilot), #2 (CS Dispute Resolution), #3 (Shift Briefing)**.

## Thẻ bài toán: Card #1 — Smart Dispatch & Driver Co-pilot

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1 — Smart Dispatch & Driver Co-pilot    │
│                                                             │
│ Bài toán: Tài xế Xanh SM tự quyết định thời điểm/nơi sạc    │
│ theo cảm tính, dẫn tới downtime sạc trùng giờ cao điểm và   │
│ xe chết pin giữa đường phải gọi cứu hộ.                     │
│ Công ty thành viên: [x] Xanh SM   [x] VinFast (telemetry)   │
│                                                             │
│ Ai đang đau? Tài xế (mất cuốc), Điều phối viên (quá tải),   │
│ Khách hàng (chờ xe lâu vào giờ cao điểm)                    │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Tài xế tự quan sát % pin trên app                      │
│   → 2. Tự đoán/nhớ trạm sạc gần nhất                        │
│   → 3. Gọi tổng đài hỏi trạm nào còn trụ trống              │
│   → 4. Điều phối tra bản đồ + soạn chỉ dẫn gửi lại          │
│                                                             │
│ Bước nào tốn nhất? Bước 3-4 (⏱ 10-12 phút/lượt,             │
│ ~80 lượt/ngày). Ngoài ra xe chết pin phải chờ cứu hộ 60-90'.│
│ AI nhảy vào ở bước nào? Bước 2-4: gộp telemetry pin         │
│ (VinFast) + trạng thái trụ sạc + demand cuốc để gợi ý       │
│ thời điểm & trạm sạc ít chờ nhất.                           │
│ (Điểm khác biệt với bài mẫu: PROACTIVE planning đầu ca,     │
│ không chỉ emergency cứu hộ khi đã hết pin.)                 │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm phút chết pin/tài xế/ngày từ 45' ──> 15'.              │
│ Giảm lượt gọi cứu hộ pin từ 80 ──> dưới 20 lượt/ngày.       │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

## Thẻ bài toán: Card #2 — Automated CS Dispute Resolution (Triage + Draft, HITL)

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2 — CS Dispute Resolution Co-pilot      │
│                                                             │
│ Bài toán: Khiếu nại cước/lộ trình của khách phải được CSKH  │
│ đọc tay trip log + GPS trace + chat transcript để đối chiếu │
│ và soạn phương án giải quyết — chậm, dễ sai lệch.           │
│ Công ty thành viên: [x] Xanh SM (dữ liệu GPS/log từ VinFast)│
│                                                             │
│ Ai đang đau? Nhân viên CSKH (quá tải, lặp lại), Supervisor  │
│ (duyệt mệt), Khách hàng (chờ SLA 24h, khó chịu)             │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Khách gửi khiếu nại qua App/Hotline                    │
│   → 2. CSKH mở 3 hệ thống đọc trip log + GPS + chat         │
│   → 3. Đối chiếu thủ công lời kể khách vs dữ liệu           │
│   → 4. Trình supervisor duyệt phương án hoàn tiền           │
│   → 5. Soạn tin nhắn phản hồi và gửi khách                  │
│                                                             │
│ Bước nào tốn nhất? Bước 3-4 (⏱ tổng 20 phút/lượt,           │
│ ~200 lượt/ngày toàn mạng ≈ 67 giờ nhân sự/ngày)             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-3-5:           │
│ AI đọc & tóm tắt log, đối chiếu, DRAFT phương án + tin      │
│ nhắn. Con người vẫn duyệt (HITL), AI không tự hoàn tiền.    │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian xử lý từ 20 phút ──> 5 phút/lượt.            │
│ 95% draft được duyệt không phải sửa. SLA 24h ──> 4h.        │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

## Thẻ bài toán: Card #3 — Shift & Demand Summarizer (Shift Briefing Generator)

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3 — Shift Briefing Generator            │
│                                                             │
│ Bài toán: Điều phối viên đầu ca phải tự đọc 4-5 nguồn       │
│ (thời tiết, lịch sự kiện, giao thông, backlog cuốc) rồi     │
│ viết tay briefing phân vùng xe cho tài xế.                  │
│ Công ty thành viên: [x] Xanh SM                             │
│                                                             │
│ Ai đang đau? Điều phối viên (30'/ca viết briefing),         │
│ Tài xế (thiếu thông tin vùng nóng), Công ty (mất cuốc)      │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Đọc dự báo thời tiết + lịch sự kiện concert/cờ         │
│   → 2. Xem bản đồ giao thông + vùng tắc đường               │
│   → 3. Xem backlog cuốc chưa nhận của ca trước              │
│   → 4. Viết tay briefing + gửi app tài xế (30 phút/ca)      │
│                                                             │
│ Bước nào tốn nhất? Bước 4 — tổng hợp & diễn đạt (⏱ 30'/ca)  │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 1-4: AI gom      │
│ dữ liệu có sẵn + DRAFT briefing đầu ca, điều phối duyệt.    │
│ (Lưu ý: KHÔNG làm bài toán dự đoán demand bằng ML — ngoài   │
│ phạm vi lab, chỉ summarization + format.)                   │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian soạn briefing từ 30' ──> 5'/ca.              │
│ 3 ca/ngày × 5 trung tâm điều vận ≈ tiết kiệm ~6 giờ/ngày.   │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

---

## 🗳️ Đề xuất lựa chọn cho nhóm

Đề xuất nhóm chọn **Card #2 — CS Dispute Resolution Co-pilot** để Deep-Dive, vì:

1. **LLM-fit mạnh nhất:** đầu vào là chat transcript tiếng Việt đời thường — rule-based không đọc hiểu được; GPS/log đối chiếu bằng số thì rule làm được nhưng "diễn giải lời kể vs dữ liệu" là việc của LLM.
2. **Không trùng worked example:** bài mẫu giảng viên đã làm kịch bản cứu hộ pin — nếu deep-dive Card #1 sẽ bị đánh giá là copy.
3. **Boundary HITL rõ và có chiều sâu:** tiền bạc của khách → bắt buộc có ngưỡng duyệt hoàn tiền, adversarial test rất "có máu".
4. Card #3 yếu nhất về metric (giá trị nằm ở "bắt demand" nhưng phần đó cần ML dữ liệu lịch sử — không làm được trong lab).

> *(Điểm trừ của Card #2 đã được xử lý: loại bỏ hoàn toàn ý "AI giải quyết tự động" — mọi hoàn tiền phải qua con người duyệt.)*
