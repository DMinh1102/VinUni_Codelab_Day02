# 01 - Problem Scan and Quick Cards

## Bối cảnh và phạm vi

Nhóm đóng vai trò AI Product Engineer tại Vin Smart Future. Bản scan tổng hợp các hướng bài toán trong brief của năm thành viên: VinFast, Xanh SM/GSM, Vinhomes, Vinmec và Vinpearl/VinWonders. Đây là cơ hội cần kiểm chứng, không phải mô tả đã xác nhận về quy trình nội bộ.

**Lưu ý về bằng chứng:** Các bước workflow, thời lượng và bottleneck trong Quick Cards là giả thuyết để lập kế hoạch khảo sát. Không có dữ liệu vận hành hay phỏng vấn nhân viên trong brief. Cần đo baseline thực tế trước khi dùng các con số làm cam kết hiệu quả.

## Phase 1 - SCAN: Tìm kiếm cơ hội

| # | Công ty | Lens | Bài toán / bottleneck tiềm năng |
|---|---|---|---|
| 1 | **VinFast** | AI upgrade / stakeholder pain | Trợ lý giọng nói trong xe khó hiểu lệnh nhiều ý khi cabin ồn hoặc người dùng nói giọng địa phương. |
| 2 | **VinFast** | Tốn thời gian | Nhân viên dịch vụ phải chuyển mô tả mơ hồ như “xe kêu lạ khi phanh” thành ticket có cấu trúc cho kỹ thuật viên. |
| 3 | **VinFast** | Lặp lại | Nhân viên hỗ trợ phải giải thích lặp đi lặp lại log BMS và cảnh báo sức khỏe pin cho chủ xe. |
| 4 | **Xanh SM / GSM** | Tốn thời gian / pain từ người khác | Điều phối viên cần tổng hợp pin, nhu cầu chuyến, tình trạng trạm và thời gian chờ để tư vấn tài xế về điểm sạc phù hợp. |
| 5 | **Xanh SM / GSM** | Lặp lại | Nhân viên CSKH đối chiếu log chuyến, GPS và hội thoại để xử lý khiếu nại về cước hoặc lộ trình. |
| 6 | **Xanh SM / GSM** | Tốn thời gian | Thông tin thời tiết và sự kiện cần được chuyển thành cảnh báo khu vực có nhu cầu cho tài xế theo ca. |
| 7 | **Vinhomes** | Lặp lại / pain từ người khác | Tin nhắn cư dân về rò rỉ nước, tiếng ồn hoặc giấy phép thi công cần được trích xuất vị trí, mức độ khẩn cấp và đội xử lý. |
| 8 | **Vinhomes** | AI upgrade | Cư dân tra cứu phí, tiện ích và nội quy từ nhiều tài liệu; câu trả lời không có căn cứ có thể gây hiểu nhầm chính sách. |
| 9 | **Vinmec** | Pain từ người khác | Bệnh nhân cần được hỏi triệu chứng có cấu trúc và hướng đến chuyên khoa phù hợp mà không để bot tự chẩn đoán. |
| 10 | **Vinmec** | Tốn thời gian | Bác sĩ cần tổng hợp dictation và kết quả xét nghiệm thành bản tóm tắt bệnh án/xuất viện để bác sĩ kiểm tra. |
| 11 | **Vinpearl / VinWonders** | AI upgrade / pain từ người khác | Gia đình cần lịch tham quan theo sở thích và tình trạng hàng chờ hiện tại, có phương án thay thế khi trò chơi quá đông hoặc tạm dừng. |
| 12 | **Vinpearl / VinWonders** | Lặp lại | Quản lý phải đọc review đa ngôn ngữ và chuyển phản hồi lặp lại thành việc cần xử lý cho bộ phận buồng phòng/F&B. |

## Phase 2 - QUICK-ASSESS: Ba Quick Problem Cards

Các thẻ được chọn vì có actor cụ thể, quy trình có thể quan sát và AI có thể bị giới hạn ở bước hỗ trợ. Thời lượng ghi trong workflow là **ước tính giả định để kiểm chứng**, không phải số liệu vận hành đã đo.

### QUICK PROBLEM CARD #1 - Xanh SM: Smart Dispatch & Charging Co-pilot

**Bài toán (1 câu):** Điều phối viên mất thời gian tổng hợp trạng thái pin, nhu cầu chuyến và dữ liệu trạm để đưa ra hướng dẫn sạc phù hợp cho tài xế.

**Công ty thành viên:** [ ] VinFast  [x] Xanh SM / GSM  [ ] Vinhomes  [ ] Vinmec  [ ] Khác

**Ai đang đau (Actor)?** Tài xế phải chờ hướng dẫn; điều phối viên phải tra cứu nhiều nguồn; hành khách có thể bị ảnh hưởng nếu xe ngừng hoạt động.

**Workflow thủ công hiện tại (giả thuyết, 5 bước):**
1. Tài xế báo pin thấp và cung cấp tình trạng/vị trí (2 phút).
2. Điều phối viên kiểm tra pin, vị trí và nhu cầu chuyến hiện tại (2 phút).
3. Tra cứu trạm tương thích, trạng thái còn chỗ và thời gian chờ (5 phút).
4. So sánh phương án, soạn hướng dẫn và xác nhận với tài xế (4 phút).
5. Ghi nhận kết quả hoặc chuyển đội hỗ trợ sạc (2 phút).

**Bước tốn thời gian/lỗi nhất:** Bước 3-4, ước tính 9 phút/lượt; cần đo bằng quan sát thực tế.

**AI hỗ trợ ở đâu?** Trích xuất thông tin từ báo cáo tự do và soạn bản nháp dựa trên snapshot đã được hệ thống tin cậy cung cấp. Rule xác định ngưỡng an toàn; điều phối viên duyệt trước mọi hành động. Prototype hiện tại không kết nối API trạm và không thực hiện điều phối.

**Metric thành công (mục tiêu pilot đề xuất):** Giảm thời gian từ khi nhận đủ thông tin đến khi có hướng dẫn được duyệt xuống tối đa 3 phút; đạt ít nhất 95% chính xác khi trích xuất pin/vị trí/độ khẩn cấp trên tập test gán nhãn; không có đề xuất trạm trong test khi pin dưới 5%.

**Quick Architecture:** [ ] No AI  [ ] Rule  [x] LLM Feature + Rule kiểm tra an toàn  [ ] Agent

### QUICK PROBLEM CARD #2 - VinFast: Service Desk Triage

**Bài toán (1 câu):** Mô tả triệu chứng xe bằng tiếng Việt tự nhiên cần được chuẩn hóa thành ticket đủ thông tin để cố vấn dịch vụ chuyển cho kỹ thuật viên.

**Công ty thành viên:** [x] VinFast  [ ] Xanh SM / GSM  [ ] Vinhomes  [ ] Vinmec  [ ] Khác

**Ai đang đau (Actor)?** Chủ xe phải mô tả lại triệu chứng; cố vấn dịch vụ mất thời gian hỏi và ghi nhận; kỹ thuật viên nhận ticket thiếu chi tiết.

**Workflow thủ công hiện tại (giả thuyết, 4 bước):**
1. Chủ xe mô tả tiếng động/sự cố qua điện thoại hoặc quầy dịch vụ (2 phút).
2. Cố vấn hỏi thêm thời điểm, điều kiện xảy ra và vị trí triệu chứng (4 phút).
3. Cố vấn viết tóm tắt, thông tin xe và biểu hiện vào ticket (3 phút).
4. Kỹ thuật viên tiếp nhận và tự kiểm tra xe; không dựa vào AI để kết luận lỗi.

**Bước tốn thời gian/lỗi nhất:** Bước 2-3, ước tính 7 phút intake/lượt; cần kiểm tra qua mẫu ticket và phỏng vấn cố vấn.

**AI hỗ trợ ở đâu?** Tạo tóm tắt trung lập, điền trường thông tin và đề xuất câu hỏi còn thiếu. Không chẩn đoán, không chỉ dẫn sửa chữa, không tự đóng ticket; cố vấn dịch vụ duyệt bản nháp.

**Metric thành công (mục tiêu pilot đề xuất):** Giảm thời gian soạn ticket từ baseline đo được xuống tối đa 2 phút; ít nhất 90% ticket có đủ trường bắt buộc sau chỉnh sửa; không có chẩn đoán hoặc hướng dẫn sửa chữa do AI tự khẳng định.

**Quick Architecture:** [ ] No AI  [ ] Rule  [x] LLM Feature + kiểm tra trường bắt buộc  [ ] Agent

### QUICK PROBLEM CARD #3 - Vinhomes: Resident Super-App Triage

**Bài toán (1 câu):** Phản ánh cư dân dạng tự do cần được phân loại theo sự cố, địa điểm, mức độ ưu tiên và đội kỹ thuật phụ trách.

**Công ty thành viên:** [ ] VinFast  [ ] Xanh SM / GSM  [x] Vinhomes  [ ] Vinmec  [ ] Khác

**Ai đang đau (Actor)?** Cư dân chờ xử lý; CSKH phải đọc và chuyển yêu cầu; kỹ thuật viên có thể nhận ticket thiếu vị trí hoặc sai nhóm.

**Workflow thủ công hiện tại (giả thuyết, 4 bước):**
1. Cư dân gửi tin nhắn qua ứng dụng (1 phút).
2. Nhân viên đọc, xác định tòa/căn hộ và loại vấn đề (3 phút).
3. Nhân viên hỏi thêm chi tiết nếu thiếu và chọn mức ưu tiên (3 phút).
4. Chuyển ticket cho ban quản lý/đội kỹ thuật và theo dõi tiếp nhận (2 phút).

**Bước tốn thời gian/lỗi nhất:** Bước 2-3, ước tính 6 phút/lượt; việc phân loại sai hoặc thiếu địa điểm có thể gây chuyển nhầm.

**AI hỗ trợ ở đâu?** Tạo ticket nháp có loại yêu cầu, vị trí, mức độ khẩn cấp, nội dung tóm tắt và câu hỏi còn thiếu. Rule xử lý các dấu hiệu nguy hiểm đã được thống nhất; nhân viên xác nhận trước khi chuyển. Không tự đóng ticket hoặc thay thế quy trình ứng cứu.

**Metric thành công (mục tiêu pilot đề xuất):** Đạt ít nhất 90% chính xác về loại yêu cầu và địa điểm trên tập test được nhân viên gán nhãn; giảm thời gian intake trung vị ít nhất 30% so với baseline; 100% cảnh báo khẩn cấp được người phụ trách xem xét.

**Quick Architecture:** [ ] No AI  [x] LLM Feature + Rule định tuyến  [ ] Agent

## Quyết định lựa chọn của nhóm

Nhóm chọn **Card #1 - Xanh SM Smart Dispatch & Charging Co-pilot** để làm Deep-Dive. Lý do: bài toán gắn trực tiếp với brief Member 2, có thể giới hạn prototype ở trích xuất và soạn nháp, đồng thời có các điều kiện an toàn kiểm thử được. Việc chọn này phục vụ phạm vi lab, **không khẳng định đây là cơ hội có giá trị kinh doanh cao nhất**.

- **Chưa chọn Card #2 (VinFast):** Có tiềm năng giảm công việc nhập ticket, nhưng cần bộ ticket đã được kỹ thuật viên gán nhãn để đánh giá chất lượng; phạm vi ưu tiên của prototype hiện tại là dispatch/sạc.
- **Chưa chọn Card #3 (Vinhomes):** Có thể triển khai phân loại ticket, nhưng cần quy tắc ưu tiên và taxonomy riêng cho từng dự án/tòa nhà; cần xác nhận với ban quản lý trước khi đánh giá routing.

**Ranh giới cho bài được chọn:** Prototype chỉ dùng dữ liệu được đưa vào prompt, không giả định có dữ liệu thời gian thực. Nếu pin dưới 5%, yêu cầu chuyển sang phương án xe sạc di động và không đề xuất trạm; nếu dữ liệu trạm thiếu/cũ/mâu thuẫn thì yêu cầu điều phối viên xem xét. AI không gửi tin, điều xe hoặc thay đổi chuyến; mọi hành động cần người phụ trách duyệt.
