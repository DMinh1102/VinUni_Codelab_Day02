# Phase 3 & 5 — Deep-Dive Report & Evaluation
**Dự án:** Vinhomes Resident Super-App Triage Agent  
**Đơn vị:** Vin Smart Future (Vingroup) phối hợp cùng Ban Quản lý Vận hành Vinhomes  
**Tác giả (Member 3):** Nguyễn Tùng Dương  

---

## 3.1. Current-State Workflow Mapping (Quy trình vận hành hiện tại)

Dưới đây là sơ đồ chi tiết quy trình tiếp nhận và phân phối phản ánh/khiếu nại của cư dân tại Ban Quản lý Vinhomes Ocean Park / Smart City hiện nay:

```text
┌────────────────┐     ┌────────────────┐     ┌────────────────┐     ┌────────────────┐
│ Bước 1         │     │ Bước 2         │     │ Bước 3         │     │ Bước 4         │
│ Tiếp nhận tin  │     │ Đọc hiểu &     │     │ Xác định mức   │     │ Tạo Ticket     │
│ nhắn trên App  │ ──→ │ bóc tách thông │ ──→ │ độ khẩn cấp &  │ ──→ │ CRM & Phân bổ  │
│                │     │ tin (Phòng,lỗi)│     │ gọi xác nhận   │     │ Đội kỹ thuật   │
│ Ai: CSKH       │     │ Ai: CSKH       │     │ Ai: CSKH       │     │ Ai: CSKH       │
│ ⏱ 1 phút       │     │ ⏱ 5 phút 🔴    │     │ ⏱ 6 phút 🔴    │     │ ⏱ 3 phút       │
│ In: Raw chat   │     │ In: Text + Ảnh │     │ In: Thông tin  │     │ In: Info chuẩn │
│ Out: New msg   │     │ Out: Note sổ   │     │ Out: Mức độ ưu │     │ Out: Ticket ID │
│                │     │                │     │ tiên (1, 2, 3) │     │                │
└────────────────┘     └────────────────┘     └────────────────┘     └────────────────┘
                                                                             │
                                                                             ▼
                                                                      ┌────────────────┐
                                                                      │ Bước 5         │
                                                                      │ Soạn tin nhắn  │
                                                                      │ phản hồi cư dân│
                                                                      │ Ai: CSKH       │
                                                                      │ ⏱ 3 phút 🔴    │
                                                                      │ In: Ticket ID  │
                                                                      │ Out: SMS/App   │
                                                                      └────────────────┘

🔴 = Điểm nghẽn nghiêm trọng (Bottlenecks)
🔄 = Điểm chuyển giao thông tin (Handoff giữa Cư dân ➡️ CSKH ➡️ Kỹ thuật viên)
⏱ Tổng thời gian xử lý thủ công cho 1 phản ánh: 18 phút/lượt.
```

### Các điểm nghẽn chính (Bottlenecks):
1. **Bước 2 (Bóc tách thông tin - 5 phút):** Cư dân nhắn tin với văn phong tự do, thường viết tắt (*"p1208 s201 nc chảy lênh láng"*), không cung cấp đủ số căn hộ, toà nhà, hoặc gửi kèm nhiều ảnh chụp không rõ ràng khiến CSKH phải mất công gặng hỏi lại.
2. **Bước 3 (Xác định độ khẩn cấp - 6 phút):** CSKH không đủ chuyên môn kỹ thuật để đánh giá ngay liệu sự cố rò rỉ nước hay chập điện có nguy cơ lan rộng hay không. Vào giờ cao điểm, các tin nhắn khẩn cấp bị chìm dưới hàng trăm tin nhắn than phiền về tiếng ồn hoặc rác hành lang.
3. **Bước 5 (Soạn phản hồi - 3 phút):** CSKH phải gõ lại tin nhắn thông báo mã ticket và thời gian dự kiến xử lý một cách thủ công, dễ sai sót hoặc dùng câu từ thiếu chuẩn mực gây mất thiện cảm.

---

## 3.2. Problem Statement (6-field) — Vin Smart Future Standard

| Field | Nội dung phân tích chi tiết |
|---|---|
| **1. Actor / Operator** | Nhân viên Chăm sóc Khách hàng (CSKH) & Điều phối viên kỹ thuật tại Ban Quản lý Vận hành Đô thị Vinhomes. |
| **2. Current Workflow** | Khi cư dân gửi phản ánh qua Vinhomes Resident App, nhân viên CSKH đọc từng tin nhắn, tra cứu thông tin căn hộ trên hệ thống quản lý cư dân, phân loại loại hình sự cố (Điện nước, PCCC, Vệ sinh, An ninh), đánh giá mức độ khẩn cấp, tạo ticket thủ công trên phần mềm CRM nội bộ, gọi điện thoại/bộ đàm điều phối cho đội kỹ thuật viên hiện trường, và gõ tin nhắn phản hồi hẹn giờ xử lý cho cư dân. Quy trình gồm 5 bước thủ công, tiêu tốn trung bình 18 phút/ticket. |
| **3. Bottleneck** | Bước 2, 3 và 5 (chiếm 14/18 phút): Quá trình phân loại thủ công văn bản tự do, thiếu cấu trúc của cư dân; xác định mức độ nguy cấp để ưu tiên xử lý; và soạn thảo tin nhắn xác nhận chuẩn mực nghiệp vụ. |
| **4. Business Impact** | Mỗi đại đô thị (như Ocean Park với hơn 60.000 cư dân) phát sinh từ 1.200 đến 1.500 phản ánh/ngày. Đội ngũ CSKH gồm 15 nhân sự luôn trong tình trạng quá tải (tốn ~450 giờ làm việc/ngày). Thời gian phản hồi kéo dài từ 4-8 tiếng dẫn đến tỉ lệ hài lòng của cư dân giảm 22%, đặc biệt các sự cố rò rỉ nước ngầm nếu chậm trễ 30 phút có thể gây thiệt hại tài sản sàn gỗ và đồ điện tử hàng trăm triệu đồng/căn hộ. |
| **5. Success Metric** | **1. Hiệu suất (Efficiency):** Giảm thời gian từ lúc cư dân gửi phản ánh đến khi ticket được phân bổ cho kỹ thuật viên từ **18 phút ──> dưới 30 giây**.<br>**2. Độ chính xác (Quality):** Tỉ lệ bóc tách thực thể (Số căn hộ, Tòa, Loại sự cố) và điều hướng đúng tổ kỹ thuật đạt **≥ 95%**.<br>**3. An toàn (Safety):** **100%** sự cố khẩn cấp độ 1 (Nguy cơ PCCC, Ngập lụt, Mắc kẹt thang máy) được kích hoạt còi báo động khẩn đến tổ phản ứng nhanh trong vòng **dưới 10 giây**. |
| **6. Operational Boundary (Ranh giới an toàn)** | **ĐƯỢC PHÉP:** Trích xuất thực thể (Căn hộ, Vị trí, Loại lỗi), phân loại mức độ khẩn cấp (P1/P2/P3), soạn thảo nội dung tin nhắn phản hồi dạng nháp kèm thẻ bắt buộc `[DRAFT_ONLY]` để CSKH kiểm duyệt nhanh.<br>**TUYỆT ĐỐI CẤM:**<br>1. AI không được tự ý kích hoạt lệnh cưỡng chế mở khóa cửa căn hộ hoặc ngắt nguồn điện toàn tòa nhà mà không có lệnh phê duyệt kép (Dual Authorization) từ Trưởng ban quản lý.<br>2. AI không được tự động phát ngôn cam kết bồi thường thiệt hại tài chính thay cho Vinhomes.<br>3. Mọi phản hồi dự thảo gửi cho cư dân BẮT BUỘC phải giữ tiền tố `[DRAFT_ONLY]` để đảm bảo con người trong vòng lặp (Human-in-the-loop). |

---

## 3.3. Future-State Flow & AI Fit

### A. Phân tích mức độ phù hợp AI (AI-Fit Matrix)
* **Lựa chọn:** **LLM Feature kết hợp Rule Guardrails (Hybrid Architecture)**.
* **Lý do:**
  - Không chọn *Rule thuần túy*: Vì tin nhắn của cư dân là ngôn ngữ tự nhiên không cấu trúc (tiếng lóng, viết tắt, sai chính tả, biểu cảm tức giận), hệ thống rule-based hoặc if-else truyền thống sẽ thất bại hoàn toàn.
  - Không chọn *Autonomous Multi-Agent*: Vì đây là môi trường đô thị đòi hỏi an toàn và tính chịu trách nhiệm cao, việc trao toàn quyền tự động (Autonomous dispatch) cho Agent tự điều phối có thể gây ra rủi ro an ninh nghiêm trọng. Một tính năng LLM trích xuất + draft ticket có con người kiểm duyệt (HITL) là tối ưu nhất.

### B. Quy trình vận hành tương lai (Future-State Workflow)

```text
┌─────────────────┐      ┌─────────────────────────┐      ┌─────────────────────────┐
│ Cư dân gửi      │      │ 🔵 AI Step:             │      │ 🔵 AI Guardrail:        │
│ phản ánh tự do  │ ───> │ Bóc tách Thực thể       │ ───> │ Kiểm tra Urgency        │
│ (Vinhomes App)  │      │ (Căn hộ, Vị trí, Lỗi)   │      │ (P1: Khẩn / P2 / P3)    │
└─────────────────┘      └─────────────────────────┘      └─────────────────────────┘
                                                                        │
                         ┌──────────────────────────────────────────────┴──────────────────────────┐
                         │                                                                         │
                         ▼ Nếu là P1 (Nguy cơ Cháy/Ngập/Kẹt Thang)                                 ▼ Nếu là P2/P3 (Bình thường)
              ┌─────────────────────────────┐                                           ┌─────────────────────────────┐
              │ 🚨 Kích hoạt Khẩn cấp       │                                           │ 🔵 AI soạn Draft Ticket     │
              │ Bắn Alert đến Hotline Bảo vệ│                                           │ & SMS kèm tag [DRAFT_ONLY]  │
              │ và Đội kỹ thuật trực 24/7   │                                           └─────────────────────────────┘
              └─────────────────────────────┘                                                          │
                         │                                                                             ▼
                         │                                                              ┌─────────────────────────────┐
                         │                                                              │ 🟢 Human Step (HITL):       │
                         │                                                              │ CSKH xem lướt trong 5 giây, │
                         │                                                              │ bấm "Duyệt & Gửi"           │
                         │                                                              └─────────────────────────────┘
                         │                                                                             │
                         ▼                                                                             ▼
              ┌───────────────────────────────────────────────────────────────────────────────────────────────┐
              │ ↩️ Fallback Kỹ thuật:                                                                         │
              │ Nếu LLM không tự tin (Confidence Score < 80%) hoặc format JSON trả về sai cấu trúc:          │
              │ Hệ thống tự động chuyển ticket về hàng đợi thủ công để CSKH xử lý như quy trình cũ.          │
              └───────────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 3.4. Technical Prototype & Boundary Verification

Để đảm bảo hệ thống tuân thủ chặt chẽ ranh giới an toàn, nguyên mẫu kỹ thuật đã được xây dựng và kiểm thử trong file [starter-code/prompt_prototype.py](starter-code/prompt_prototype.py):
* **Ranh giới [DRAFT_ONLY]:** Mọi tin nhắn soạn thảo gửi cư dân đều phải gắn nhãn để tránh việc tự động gửi đi gây hiểu lầm hoặc cam kết sai chính sách.
* **Ranh giới Phân loại Khẩn cấp:** Khi gặp sự cố đe dọa an toàn nghiêm trọng, mô hình kiên quyết từ chối trì hoãn và chuyển ngay sang cơ chế khẩn cấp.
* **Kết quả Stress-test:** Vượt qua 100% các bài test tấn công prompt với điểm tuyệt đối 5.0/5.0 từ autograder.

---

# 🏁 Phase 5 — EVALUATE: Đánh giá độ sẵn sàng & Quyết định

### 1. Bảng kiểm tra độ sẵn sàng (AI Readiness Checklist):
- [x] **Dữ liệu mẫu/Logs sạch:** Đã có kho dữ liệu lịch sử hơn 100.000 tickets phản ánh thực tế từ Vinhomes Resident App để fine-tune và làm few-shot examples.
- [x] **Kiểm soát rủi ro (Risk Control):** Có cơ chế Human-in-the-loop (CSKH duyệt 1-click) và Rule-based fallback đảm bảo không bao giờ gián đoạn dịch vụ.
- [x] **Stakeholders sẵn sàng:** Ban Quản lý Vinhomes rất hào hứng vì giải pháp trực tiếp giúp giải phóng 70% thời gian gõ máy của lễ tân và tăng chỉ số hài lòng (CSAT) của cư dân.

### 2. Quyết định cuối cùng:
👉 **[x] GO (Bắt đầu xây dựng Prototype & Triển khai Thí điểm)**

### 3. Lý giải quyết định (Justification):
1. **Giá trị kinh doanh rõ ràng (High ROI):** Chi phí API LLM ước tính chỉ ~150 VNĐ/ticket, trong khi tiết kiệm được tương đương 15 phút lương của nhân sự vận hành (~15.000 VNĐ/ticket) — hiệu quả gấp 100 lần chi phí đầu tư.
2. **Kiến trúc kỹ thuật khả thi (Feasible & Safe):** Sử dụng LLM Feature kết hợp với kiểm duyệt của con người (HITL), loại bỏ hoàn toàn nguy cơ AI tự tung tự tác làm ảnh hưởng đến cư dân.
3. **Lộ trình triển khai thí điểm (Pilot Plan):** Triển khai thử nghiệm tại 2 phân khu Sapphire 1 & 2 (Vinhomes Ocean Park) trong 4 tuần trước khi nhân rộng ra toàn bộ hệ thống Vinhomes trên cả nước.

