# Bài tập UX: phân tích sản phẩm AI thật

**Thời gian:** 40 phút | **Cá nhân** | **Output:** sketch giấy, nộp cuối bài

---

## Chọn 1 sản phẩm

**Sản phẩm đã chọn: V-App — Trợ lý ảo V-AI**

| Sản phẩm | AI feature | Truy cập |
|-----------|------------|----------|
| **V-App — Trợ lý ảo V-AI** ✅ | Trợ lý text, gợi ý theo context | App V-App |

---

## Phần 1 — Khám phá (15 phút)

**Sản phẩm hứa gì (marketing):**
- Trợ lý text thông minh, gợi ý nội dung và dịch vụ theo sở thích người dùng
- Gợi ý cá nhân hóa theo hành vi và nhu cầu
- Tích hợp nhiều dịch vụ trong 1 app (siêu app)

**Quan sát thực tế khi dùng:**
- AI trả lời dạng text, có cấu trúc rõ (tiêu đề, bullet, bold)
- Hiển thị "Đã xem xét X nguồn" → transparent về quá trình xử lý
- Cite nguồn bên ngoài (motogo, hanoimoi...) → tăng credibility
- Có gợi ý autocomplete khi gõ (search suggestions), nhưng không có quick-reply buttons sau khi AI trả lời xong
- Không có nút CTA trực tiếp để thực hiện hành động ngay

---

## Phần 2 — Phân tích 4 paths (10 phút)

| Path | Quan sát thực tế |
|------|---------|
| 1. Khi AI **đúng** | User thấy câu trả lời có cấu trúc, bold key info, cite nguồn. Hệ thống hiện "Đã xem xét X nguồn". Không có animation hay CTA trực tiếp. |
| 2. Khi AI **không chắc** | AI tự assume context (assume location = Hà Nội) thay vì hỏi lại. Trả lời generic, dài, không personalized. Không có quick-reply để user filter. |
| 3. Khi AI **sai** | Test: gõ "nạp tiền cho máy lạnh" (typo: "nạp tiền cho máy lạnh"). AI hiểu nhầm thành "nạp gas máy lạnh" → trả lời hướng dẫn kỹ thuật nạp gas. Sai hoàn toàn về intent. Không có cơ chế confirm lại ý user trước khi trả lời. Không có thumbs down / feedback button. User phải tự nhận ra sai, xóa và gõ lại từ đầu — ít nhất 3 bước. |
| 4. Khi user **mất tin** | Không có nút "Gặp nhân viên" hay hotline nào trong giao diện chat. Thoát khỏi chat dễ (vuốt sang là về menu chính). Khi hỏi "gặp nhân viên" → AI hiểu nhầm thành bài HR. Khi hỏi "cho tôi nói chuyện với người thật" → AI thừa nhận không thể kết nối người thật, nhưng follow-up suggestions vẫn là HR topics (phát triển nhân viên, đào tạo nội bộ) — không có hotline, không có link CSKH, không có lối thoát thực sự. |

**Tự phân tích:**
- Path xử lý tốt nhất: **Path 1** — khi câu hỏi rõ ràng, AI trả lời có cấu trúc, có nguồn, đáng tin
- Path yếu nhất: **Path 2** — AI đoán context thay vì hỏi, không có cơ chế clarification
- Gap marketing vs thực tế: Marketing nói "gợi ý theo context" nhưng thực tế AI không thu thập context từ user, chỉ assume. Không có personalization thực sự.

---

## Phần 3 — Sketch "làm tốt hơn" (10 phút)

**Path yếu nhất được chọn: Path 2 — Khi AI không chắc**

**As-is (hiện tại — chỗ gãy):**
```
User: "Hôm nay làm gì hay?"
        ↓
V-AI tự assume location = Hà Nội (không hỏi)
        ↓
Trả lời dài, generic, không actionable
        ↓
❌ User không biết lọc / không biết tiếp theo làm gì
        ↓
User bỏ qua hoặc gõ lại câu hỏi khác
```

**To-be (đề xuất):**
```
User: "Hôm nay làm gì hay?"
        ↓
V-AI hỏi lại nhanh bằng quick-reply:
[🍜 Ăn uống] [🏛️ Tham quan] [🎮 Giải trí] [📍 Gần tôi]
        ↓
User chọn 1 option
        ↓
V-AI trả lời ngắn, focused, có nút CTA ("Xem trên bản đồ" / "Đặt bàn")
```

- **Thêm gì:** quick-reply buttons sau câu hỏi mơ hồ, CTA button trong kết quả
- **Bớt gì:** bỏ đoạn văn dài generic không actionable
- **Đổi gì:** từ "assume rồi trả lời" → "hỏi lại rồi mới trả lời"

---

## Phần 4 — Share + vote (5 phút)

*(Trình bày 30 giây với nhóm)*

> Mình chọn **V-App — Trợ lý ảo V-AI**. Marketing nói AI "gợi ý theo context", nhưng thực tế khi hỏi câu mơ hồ như *"Hôm nay làm gì hay?"*, AI không hỏi lại — nó tự assume location là Hà Nội rồi trả lời dài, generic, không actionable. Đây là **Path 2** — path yếu nhất. Đề xuất của mình: thêm **quick-reply buttons** ngay sau câu hỏi mơ hồ để user chọn context, rồi AI mới trả lời — ngắn hơn, focused hơn, có CTA luôn.

---

## Nộp bài

- [x] Ghi chú phân tích 4 paths
- [x] Sketch giấy as-is + to-be
- [x] Screenshot app + annotate chỗ gãy (nice to have)

---

## Tiêu chí chấm (10 điểm + bonus)

| Tiêu chí | Điểm |
|----------|------|
| Phân tích 4 paths đủ + nhận xét path yếu nhất | 4 |
| Sketch as-is + to-be rõ ràng | 4 |
| Nhận xét gap marketing vs thực tế | 2 |
| **Bonus:** nhóm vote sketch hay nhất | +bonus |

---

*Bài tập UX — Ngày 5 — VinUni A20 — AI Thực Chiến · 2026*
