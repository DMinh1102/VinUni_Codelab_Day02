# Deliverable — Vin Smart Future (Vinpearl & VinWonders / Xanh SM Use Case)

---

## 🏛️ Bối cảnh: Tôi là ai?

Tôi là **DangDucMinh**, AI Engineer tại **Vin Smart Future**. Nhóm chúng tôi được giao nhiệm vụ phối hợp với Khối Vận Hành của **Vinpearl & VinWonders** và đội vận tải du lịch **Xanh SM** để tìm kiếm các cơ hội tối ưu hóa bằng trí tuệ nhân tạo.

Thông qua khảo sát thực tế tại các khu nghỉ dưỡng Vinpearl Nha Trang và công viên VinWonders Đà Nẵng, tôi nhận thấy hai điểm nghẽn lớn: (1) Khách tham quan mất nhiều thời gian chờ đợi tại các trò chơi hot mà không có hệ thống điều phối thông minh, và (2) quản lý vận hành không xử lý kịp hàng nghìn review đa ngôn ngữ mỗi ngày để hành động kịp thời. Song song đó, đội tài xế Xanh SM phục vụ tuyến du lịch đang xử lý thủ công từng yêu cầu lộ trình đa điểm dừng — một quy trình tốn thời gian và dễ gây mất khách.

---

# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội (Cá nhân)

Dùng **4 Lenses** quét qua vận hành của các công ty thành viên Vingroup.

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **Vinpearl / VinWonders** | AI có thể tốt hơn (AI-upgrade) | **Dynamic Itinerary & Crowd-Shifting Concierge:** Hệ thống chatbot cá nhân hóa lịch trình tham quan theo thời gian thực, tự động gợi ý gia đình chuyển sang trò chơi/khu vực ít đông hơn khi hàng đợi một điểm vượt ngưỡng (ví dụ >30 phút), thay vì nhân viên phát tờ rơi tĩnh như hiện tại. |
| 2 | **Vinpearl / VinWonders** | Pain từ người khác (Stakeholder Pain) | **Multilingual Review & Feedback Analyzer:** Hằng ngày có hàng nghìn review tiếng Anh, Hàn, Trung, Nga trên Booking.com/Google Map/Agoda về khách sạn và công viên — quản lý phòng và F&B phàn nàn vì không đọc được và mất 2–3 ngày mới xử lý phàn nàn khẩn cấp (ví dụ: "phòng bẩn", "nhân viên thái độ tệ"). |
| 3 | **Xanh SM** | Tốn thời gian (Time-consuming) | **Tourist Multi-Stop Route Drafting:** Khách du lịch đặt xe Xanh SM yêu cầu dừng nhiều điểm tham quan (ví dụ: Bà Nà Hills → Mỹ Khê → Hội An), tài xế mất 10–15 phút mỗi chuyến để trao đổi qua lại, thương lượng giá và sắp xếp lộ trình thủ công trên Zalo/điện thoại thay vì có hệ thống tự động gợi ý lộ trình tối ưu và báo giá tức thì. |
| 4 | **Vinpearl / VinWonders** | Lặp lại (Repetitive) | **Group Booking & Room-Assignment Drafting:** Các công ty lữ hành gửi email đặt phòng đoàn phức tạp (50–200 phòng, nhiều loại phòng, nhiều check-in date). Nhân viên Vinpearl phải đọc và nhập tay vào hệ thống PMS 2–3 giờ/đơn, lặp lại hằng ngày, dễ nhầm lẫn số phòng và loại phòng. |
| 5 | **Xanh SM** | Lặp lại (Repetitive) | **Peak-Hour Tourist Shuttle Re-Dispatching:** Vào giờ cao điểm (tan ca tham quan tại Bà Nà Hills / Vinpearl Nha Trang), điều phối viên Xanh SM phải thủ công tái phân bổ hàng chục xe shuttle cho nhiều điểm đón khác nhau dựa trên số lượng khách thực tế thoát ra — quy trình lặp lại mỗi 30 phút, dễ thiếu xe hoặc dư xe gây lãng phí và khách chờ quá lâu. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards (Cá nhân)

Chọn top 3 từ danh sách SCAN: **#4 (B2B Rooming-List Parser), #2 (Multilingual Feedback Triage), #1 (Dynamic Park Concierge).**

## Card #1 — B2B Rooming-List Parser (Vinpearl)

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Các công ty lữ hành gửi email đặt phòng đoàn     │
│ phức tạp (50–200 phòng, nhiều loại, nhiều check-in date).   │
│ Nhân viên Vinpearl phải đọc và nhập tay vào PMS 2–3 giờ/   │
│ đơn, lặp lại hằng ngày, dễ nhầm lẫn số phòng & loại phòng. │
│ Công ty thành viên: [x] Vinpearl / VinWonders               │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│   Nhân viên Reservations & Groups Desk Vinpearl             │
│   (nhập tay sai sót → overbooking → khách phàn nàn).       │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Nhận email đặt phòng đoàn từ công ty lữ hành          │
│   ──> 2. Đọc và trích xuất thông tin thủ công              │
│   ──> 3. Nhập từng dòng vào hệ thống PMS                  │
│   ──> 4. Kiểm tra lại tồn kho phòng                       │
│   ──> 5. Reply xác nhận + đính kèm rooming list            │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                           │
│   Bước 2–3: đọc và nhập tay (⏱ 2–3 giờ/đơn, lỗi ~15%)    │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                      │
│   Bước 2–3: LLM đọc email thô → trích xuất JSON chuẩn      │
│   gồm tên khách, loại phòng, ngày, số lượng → cảnh báo     │
│   nếu thiếu thông tin; nhân viên chỉ cần review & submit.  │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   Giảm thời gian xử lý/đơn từ 2–3 giờ ──> dưới 15 phút.   │
│   Tỉ lệ trích xuất đúng ≥ 98%; lỗi overbooking = 0%.       │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

## Card #2 — Multilingual Review & Feedback Triage (Vinpearl / VinWonders)

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Hàng nghìn review tiếng Anh, Hàn, Trung, Nga     │
│ đổ về mỗi ngày từ Booking.com/Agoda/Google Map. Quản lý    │
│ phòng & F&B không đọc được và mất 2–3 ngày mới phát hiện   │
│ vấn đề khẩn cấp như "phòng bẩn", "nhân viên thái độ tệ".   │
│ Công ty thành viên: [x] Vinpearl / VinWonders               │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│   Housekeeping Manager, F&B Manager, Guest Relations        │
│   (phàn nàn vì phản ứng chậm, điểm review tụt dần).        │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Nhân viên vào từng platform đọc review thủ công        │
│   ──> 2. Copy sang Excel, phân loại chủ đề bằng tay        │
│   ──> 3. Dịch review ngoại ngữ qua Google Translate        │
│   ──> 4. Gửi email tóm tắt tuần lên quản lý                │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                           │
│   Bước 2–3: phân loại + dịch thủ công (⏱ ~3 giờ/ngày)     │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                      │
│   Bước 1–3: Tự động crawl → dịch → phân tích sentiment →   │
│   gắn tag chủ đề (phòng/F&B/nhân viên) → tạo ticket        │
│   khẩn gửi đúng bộ phận trong vòng <1 giờ.                 │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   Từ review xuất hiện đến ticket hành động:                 │
│   2–3 ngày ──> dưới 1 giờ; độ chính xác phân loại ≥ 90%.  │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

## Card #3 — Dynamic Park Concierge (VinWonders)

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Khách tham quan VinWonders xếp hàng >30 phút     │
│ tại các trò chơi hot trong khi khu vực khác vắng. Không    │
│ có hệ thống nào chủ động điều hướng khách theo thời gian   │
│ thực dựa trên dữ liệu hàng đợi thực tế.                    │
│ Công ty thành viên: [x] Vinpearl / VinWonders               │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│   Khách tham quan (trải nghiệm kém vì hàng đợi dài),       │
│   Nhân viên vận hành park (nhận khiếu nại trực tiếp).      │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Nhân viên quan sát hàng đợi trực tiếp tại điểm        │
│   ──> 2. Báo cáo supervisor qua bộ đàm                     │
│   ──> 3. Phát thông báo loa gợi ý khu khác (đại trà)      │
│   ──> 4. Khách tự quyết định, không có follow-up           │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                           │
│   Bước 2–3: phản ứng chậm, không cá nhân hóa               │
│   (⏱ 15–20 phút/lần, không hiệu quả với gia đình có trẻ)  │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                      │
│   Thay bước 1–3: chatbot đọc mock queue data realtime →    │
│   tạo gợi ý lịch trình cá nhân hóa theo nhóm khách →      │
│   push notification qua App hoặc QR tại cổng vào.          │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   Giảm thời gian chờ TB tại điểm nóng: >30 phút ──>        │
│   dưới 15 phút; tăng lượt ghé khu vực ít đông thêm 25%.   │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [ ] LLM  [x] Agent │
└─────────────────────────────────────────────────────────────┘
```

---

# 🗳️ Quyết định lựa chọn bài toán Deep-Dive:

Tôi quyết định lựa chọn bài toán **"Card #2 — Multilingual Review & Feedback Triage (Vinpearl / VinWonders)"** để tiến hành phân tích sâu (Deep-Dive trong file `02-deep-dive-report.md`).

## Lý do lựa chọn và loại trừ các thẻ khác:
* **Vì sao chọn Card #2 (Multilingual Review Triage):**
  - Đây là "điểm đau" nhức nhối nhất trong vận hành hằng ngày của khối Hospitality Vinpearl khi lượng khách quốc tế (Hàn Quốc, Trung Quốc, Nga, Anh) chiếm tỷ trọng rất lớn.
  - Các sự cố nghiêm trọng (P1: phòng bẩn, vệ sinh an toàn thực phẩm, thái độ nhân viên) đòi hỏi xử lý thời gian thực (Real-time Triage) ngay khi khách còn ở resort, thay vì bị trôi 2–3 ngày như cách làm thủ công.
  - Ranh giới an toàn (Operational Boundary) và cơ chế Human-in-the-Loop rất rõ ràng: AI dịch thuật, phân tích cảm xúc và draft phương án; Quản lý giữ quyền kiểm soát và phê duyệt cuối cùng.
* **Vì sao tạm gác Card #1 và Card #3:**
  - *Card #1 (B2B Rooming-List Parser):* Tuy tiết kiệm thời gian nhập liệu nhưng đơn đặt đoàn MICE mang tính thời vụ, quy trình phụ thuộc lớn vào đàm phán hợp đồng của phòng Sales, mức độ ảnh hưởng thương hiệu không cấp bách bằng việc giải quyết đánh giá xấu công khai trên OTA.
  - *Card #3 (Dynamic Park Concierge):* Đòi hỏi hạ tầng cảm biến IoT đo tải hàng đợi thời gian thực tại các công viên giải trí VinWonders, độ phức tạp triển khai lớn hơn nhiều so với việc phân tích dữ liệu review dạng văn bản.

---

## 📌 Các bước tiếp theo (Next Deliverables):
* 🏗️ **Phase 3 (Deep-Dive), Phase 4 (Prompt Prototype) & Phase 5 (Evaluate):** Toàn bộ phân tích sâu chi tiết và báo cáo kỹ thuật được trình bày tại file **[02-deep-dive-report.md](02-deep-dive-report.md)**.
* 📊 **Sơ đồ Quy trình Vận hành (Workflow Mapping Diagram):** Xem sơ đồ trực quan và kiến trúc tương lai tại file **[04-workflow-diagram.md](04-workflow-diagram.md)** và **[04-workflow-diagram.png](04-workflow-diagram.png)**.
* 📝 **Phase 6 — AI Log & Reflection:** Toàn bộ nhật ký cá nhân về quá trình sử dụng AI làm Thought-Partner và bài học kinh nghiệm được ghi lại chi tiết tại file **[03-ai-log.md](03-ai-log.md)**.
