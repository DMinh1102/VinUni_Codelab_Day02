# 🏗️ Phase 3 — DEEP-DIVE (Nhóm)

## 3.1. Current-State Workflow
Quy trình hiện tại của bác sĩ Vinmec khi tổng hợp và hoàn thiện hồ sơ tóm tắt xuất viện:

```text
┌──────────────────┐    ┌──────────────────┐    ┌──────────────────┐
│ BƯỚC 1           │    │ BƯỚC 2           │    │ BƯỚC 3           │
│ Mở bệnh án điện  │    │ Tra cứu kết quả  │    │ Đối chiếu thuốc, │
│ tử và thông tin  │ -> │ xét nghiệm, chẩn │ -> │ thủ thuật và diễn│
│ hành chính       │    │ đoán, diễn biến  │    │ biến điều trị    │
│ Ai: Bác sĩ       │    │ Ai: Bác sĩ       │    │ Ai: Bác sĩ       │
│ ⏱ 2 phút        │     │ ⏱ 6 phút 🔴    │    │ ⏱ 5 phút 🔴     │
│ In: Hồ sơ EMR    │    │ In: EMR, LIS     │    │ In: Thuốc, y lệnh│
│ Out: Ca bệnh     │    │ Out: Mốc điều trị│    │ Out: Dữ kiện     │
└──────────────────┘    └──────────────────┘    └──────────────────┘
                                                    |
                                                    ▼
                     ┌──────────────────┐    ┌──────────────────┐
                     │ BƯỚC 5           │    │ BƯỚC 4           │
                     │ Kiểm tra và hoàn │ ←─ │ Viết bản tóm tắt │
                     │ thiện hồ sơ      │    │ xuất viện theo mẫu│
                     │ Ai: Bác sĩ       │    │ Ai: Bác sĩ       │
                     │ ⏱ 2 phút 🔄     │    │ ⏱ 5 phút 🔴     │
                     │ In: Bản nháp     │    │ In: Dữ kiện tổng │
                     │ Out: Hồ sơ duyệt │    │ Out: Bản nháp 🔄 │
                     └──────────────────┘    └──────────────────┘

🔴 Bottleneck: Bước 2-4 chiếm 16/20 phút (80%), do dữ liệu nằm ở nhiều phần của hồ sơ, phải đối chiếu các mốc điều trị và diễn đạt lại thành văn bản
🔄 Handoff: Dữ liệu từ hệ thống bệnh án/xét nghiệm/y lệnh sang bản tóm tắt; bản nháp sau đó chuyển sang bước bác sĩ kiểm tra, ký và hoàn thiện. Nếu phát hiện thiếu hoặc không khớp, bác sĩ quay lại bước 2–4 để sửa

⏱ Tổng thời gian xử lý thủ công giả định: 20 phút/hồ sơ. Đây là thời gian soạn thảo và rà soát nội dung, không bao gồm chờ thanh toán, xác nhận bảo hiểm hoặc các thủ tục hành chính xuất viện khác
```

---

## 3.2. Problem Statement (6-field) — Vin Smart Future Standard

| Field | Nội dung |
|---|---|
| **1. Actor / Operator** | Bác sĩ điều trị tại Vinmec trực tiếp tổng hợp, viết và phê duyệt hồ sơ xuất viện; điều dưỡng hỗ trợ kiểm tra thông tin |
| **2. Current Workflow** | Bác sĩ mở bệnh án điện tử (EMR), tra cứu xét nghiệm, chẩn đoán, thuốc và diễn biến điều trị, sau đó viết tóm tắt xuất viện. Quy trình gồm 5 bước, ước tính 20 phút/hồ sơ |
| **3. Bottleneck** | Bước 2–4 (16 phút): Tra cứu dữ liệu từ nhiều nguồn, đối chiếu thông tin điều trị và viết tóm tắt thủ công, dễ mất thời gian hoặc bỏ sót thông tin |
| **4. Business Impact** | Mỗi hồ sơ mất khoảng 20 phút xử lý, trong đó 16 phút dành cho tổng hợp và soạn thảo. Làm tăng khối lượng công việc của bác sĩ và có thể kéo dài thời gian hoàn thiện hồ sơ |
| **5. Success Metric** | Efficiency: Giảm tổng thời gian từ 20 phút xuống dưới 5 phút/hồ sơ (giảm trên 75%). Quality: Mục tiêu ≥95% bản nháp đạt yêu cầu sau khi bác sĩ kiểm tra; 100% hồ sơ được phê duyệt trước khi lưu chính thức |
| **6. Operational Boundary** | AI được phép truy xuất dữ liệu theo phân quyền, tổng hợp thông tin và tạo bản nháp hồ sơ xuất viện. CẤM: Tự chẩn đoán, thay đổi đơn thuốc, tạo thông tin không có trong bệnh án hoặc tự phê duyệt hồ sơ. Bắt buộc bác sĩ kiểm tra và xác nhận (HITL) |

---

## 3.3. Future-State Flow & AI Fit
Chọn LLM Feature + RAG. LLM tổng hợp dữ liệu y tế và tạo bản nháp tóm tắt xuất viện; RAG hỗ trợ truy xuất thông tin từ bệnh án điện tử. Không cần Agentic Loop vì quy trình cố định và yêu cầu bác sĩ kiểm soát kết quả cuối cùng
* **Quy trình tương lai (Future-State):**

```text
┌─────────────────────────┐
│ Bước 1                  │
│ 🟢 Bác sĩ chọn hồ sơ    │
│ bệnh nhân xuất viện     │
│ ⏱ 0,5 phút              │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│ Bước 2                  │
│ 🔵 RAG truy xuất bệnh   │
│ án, xét nghiệm, thuốc   │
│ và diễn biến điều trị   │
│ ⏱ 0,5 phút              │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│ Bước 3                  │
│ 🔵 LLM tổng hợp và tạo  │
│ bản nháp xuất viện      │
│ theo mẫu                │
│ ⏱ 0,5 phút              │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│ Bước 4                  │
│ 🟢 Bác sĩ kiểm tra,     │
│ chỉnh sửa bản nháp      │
│ ⏱ 2,5 phút              │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│ Bước 5                  │
│ 🟢 Bác sĩ phê duyệt,    │
│ lưu hồ sơ vào EMR       │
│ ⏱ 0,5 phút              │
└─────────────────────────┘
             │
             ▼

↩️ FALLBACK:
Nếu AI lỗi, thiếu dữ liệu hoặc thông tin không chính xác:
→ Cảnh báo bác sĩ và yêu cầu kiểm tra nguồn.
→ Bác sĩ chỉnh sửa hoặc lập hồ sơ thủ công.
→ Không lưu hồ sơ khi chưa được phê duyệt.

⏱ Tổng thời gian mục tiêu: 4,5 phút/hồ sơ. Giảm 77,5% so với quy trình thủ công.
```

---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:
1. [ ] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?
2. [ ] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)?
3. [ ] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[ ] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**
> *Quyết định GO cho prototype vì bài toán có quy trình rõ ràng, phù hợp với LLM kết hợp RAG và có thể kiểm soát rủi ro thông qua HITL. Theo giả định tại Phase 3, giải pháp hướng tới giảm thời gian xử lý từ 20 phút xuống 4,5 phút/hồ sơ (giảm 77,5%). Về chi phí, prototype tận dụng LLM API và dữ liệu giả lập, chưa cần tích hợp trực tiếp vào EMR nên hạn chế chi phí phát triển ban đầu. AI chỉ hỗ trợ tổng hợp và soạn thảo, không thay thế quyết định chuyên môn của bác sĩ. Nhóm cần kiểm thử độ chính xác, đo thời gian thực tế và lấy ý kiến bác sĩ trước khi xem xét triển khai chính thức*

---