# AI Product Canvas — VinMec AI Health Assistant

**Use case:** AI agent trợ lý sức khỏe thông minh hỗ trợ nhắc lịch tái khám cho bệnh nhân MyVinMec

---

## Canvas

|   | Value | Trust | Feasibility |
|---|-------|-------|-------------|
| **Câu hỏi guide** | User nào? Pain gì? AI giải quyết gì mà cách hiện tại không giải được? | Khi AI sai thì user bị ảnh hưởng thế nào? User biết AI sai bằng cách nào? User sửa bằng cách nào? | Cost bao nhiêu/request? Latency bao lâu? Risk chính là gì? |
| **Trả lời** | **User:** Bệnh nhân VinMec (đặc biệt người cao tuổi 60+) sử dụng app MyVinMec<br><br>**Pain:** <br>• Khó khăn trong việc đặt lịch tái khám (UI phức tạp, nhiều bước)<br>• Tỉ lệ bỏ lỡ lịch tái khám cao do thiếu nhắc nhở thông minh<br>• Nhắc nhở hiện tại không cá nhân hóa, không chủ động<br>• Phải tự nhớ và tự đặt lại lịch khi bỏ lỡ<br><br>**AI giải quyết:**<br>• Tự động phân tích lịch sử khám và đề xuất thời điểm tái khám phù hợp<br>• Chủ động kiểm tra slot khả dụng và đặt lịch tự động (với xác nhận)<br>• Nhắc nhở đa kênh (app notification, SMS, call) dựa trên preference và hành vi user<br>• Điều chỉnh lịch thông minh khi user bỏ lỡ hoặc cần reschedule | **Khi AI sai:**<br>• Đặt sai thời gian → user đến sai giờ hoặc bỏ lỡ<br>• Đặt sai bác sĩ/chuyên khoa → user phải đặt lại<br>• Nhắc nhở sai thời điểm → spam hoặc miss appointment<br>• Đặt trùng lịch → conflict với lịch cá nhân<br><br>**User biết AI sai:**<br>• Hiển thị rõ thông tin đặt lịch: bác sĩ, thời gian, địa điểm<br>• Yêu cầu xác nhận trước khi đặt lịch chính thức<br>• Gửi reminder 48h, 24h, 2h trước để user double-check<br>• Hiển thị confidence score cho đề xuất<br><br>**User sửa:**<br>• Từ chối đề xuất và tự chọn slot khác<br>• Reschedule trực tiếp trong notification<br>• Cập nhật preference (thời gian ưa thích, kênh nhắc nhở)<br>• Feedback "không phù hợp" để AI học | **Cost/request:**<br>• LLM call cho context analysis: ~$0.001-0.003/request<br>• Slot checking API: negligible<br>• SMS notification: ~$0.01-0.02/SMS<br>• Voice call reminder: ~$0.05-0.10/call<br>• Ước tính: $0.02-0.05/user/month<br><br>**Latency:**<br>• Slot checking: <2s<br>• AI recommendation: <3s<br>• Booking confirmation: <5s<br>• Acceptable cho non-realtime use case<br><br>**Risk chính:**<br>• Privacy: dữ liệu sức khỏe nhạy cảm (HIPAA-like compliance)<br>• Reliability: miss appointment → ảnh hưởng sức khỏe<br>• Integration: phụ thuộc HIS/booking system của VinMec<br>• Adoption: người cao tuổi cần onboarding tốt |

---

## Automation hay augmentation?

☐ Automation — AI làm thay, user không can thiệp
☑ Augmentation — AI gợi ý, user quyết định cuối cùng

**Justify:** 

Chọn **Augmentation** vì:
1. **High stakes:** Lịch khám bệnh ảnh hưởng trực tiếp đến sức khỏe → cần user xác nhận
2. **Context phức tạp:** AI không biết lịch cá nhân, công việc, ưu tiên của user
3. **Trust building:** User (đặc biệt người cao tuổi) cần cảm giác kiểm soát
4. **Legal/compliance:** Đặt lịch y tế nên có explicit consent

**Flow đề xuất:**
- AI phân tích → đề xuất 2-3 slot phù hợp nhất
- User chọn 1 slot hoặc xem thêm options
- AI đặt lịch sau khi user confirm
- AI nhắc nhở chủ động nhưng user có thể snooze/reschedule

---

## Learning signal

| # | Câu hỏi | Trả lời |
|---|---------|---------|
| 1 | User correction đi vào đâu? | • User từ chối đề xuất → log rejected slots + lý do (nếu có)<br>• User chọn slot khác → preference learning (thời gian, bác sĩ)<br>• User reschedule → pattern về timing conflicts<br>• User feedback "không phù hợp" → explicit negative signal<br>• Tất cả vào user profile + aggregate analytics |
| 2 | Product thu signal gì để biết tốt lên hay tệ đi? | **Positive signals:**<br>• Acceptance rate của đề xuất (target >70%)<br>• Show-up rate sau khi đặt lịch (target giảm miss rate 30%+)<br>• Time-to-book giảm (so với manual booking)<br>• User engagement với reminders (open rate, click rate)<br><br>**Negative signals:**<br>• Rejection rate cao<br>• Reschedule rate tăng<br>• User turn off notifications<br>• Complaints về spam/timing<br><br>**Leading indicators:**<br>• Slot recommendation accuracy<br>• Reminder timing effectiveness<br>• User satisfaction score (NPS) |
| 3 | Data thuộc loại nào? ☑ User-specific · ☑ Domain-specific · ☐ Real-time · ☑ Human-judgment · ☐ Khác: ___ | **User-specific:** Lịch sử khám, preference thời gian, response pattern<br>**Domain-specific:** Medical protocols (tái khám sau X tuần), VinMec slot availability patterns<br>**Human-judgment:** User feedback về đề xuất, preference adjustments |

**Có marginal value không?**

**CÓ - High marginal value:**

1. **User-specific behavior:** 
   - Mỗi user có pattern riêng (sáng/chiều, thứ mấy, bác sĩ nào)
   - Model chung không biết được → cần học từ interaction

2. **VinMec-specific domain:**
   - Slot availability patterns của từng phòng khám/bác sĩ
   - Peak hours, seasonal patterns (flu season → nhiều lịch hơn)
   - Competitor không có access vào data này

3. **Closed-loop learning:**
   - Show-up data chỉ VinMec có (không public)
   - Reschedule patterns → improve recommendation
   - Reminder effectiveness → optimize timing/channel

**Data moat:** VinMec có thể build competitive advantage nếu:
- Thu thập và học từ correction signals
- Optimize cho VinMec-specific workflows
- Personalize dựa trên user behavior over time

---

## Data Flywheel Design

### Vòng lặp cơ bản:

```
User interaction → AI learns preference → Better recommendations → 
Higher acceptance rate → More bookings → More show-up data → 
Refined models → Better predictions → [Repeat]
```

### Chi tiết từng bước:

**1. Ingest (Thu thập data):**
- User booking history
- Slot acceptance/rejection
- Show-up/no-show records
- Reschedule patterns
- Reminder response rates
- Explicit feedback

**2. Digest (Xử lý & học):**
- User preference modeling (time, doctor, frequency)
- Slot availability prediction
- Optimal reminder timing
- Channel effectiveness (app vs SMS vs call)
- Churn risk prediction

**3. Output (Cải thiện product):**
- More accurate slot recommendations
- Smarter reminder timing
- Personalized communication channel
- Proactive reschedule suggestions
- Better UX for elderly users

**4. Repeat (Đo lường & tối ưu):**
- Track acceptance rate, show-up rate
- A/B test reminder strategies
- Measure time-to-book improvement
- Monitor user satisfaction

### Network effects:
- Nhiều user → better slot availability prediction
- Nhiều bookings → better doctor/clinic load balancing
- Nhiều feedback → better recommendation for new users (cold start)

---

## Implementation Roadmap

### Phase 1: MVP (2-3 tháng)
- Smart reminder với 3 channels (app, SMS, call)
- Basic slot recommendation (rule-based + simple ML)
- User confirmation flow
- Basic analytics dashboard

### Phase 2: Personalization (3-6 tháng)
- User preference learning
- Adaptive reminder timing
- Multi-slot recommendation với ranking
- Feedback loop integration

### Phase 3: Proactive Intelligence (6-12 tháng)
- Predictive rebooking (trước khi user quên)
- Conflict detection (với lịch cá nhân nếu có integration)
- Health journey tracking (chuỗi khám dài hạn)
- Voice assistant integration

---

## Success Metrics

### North Star Metric:
**Appointment show-up rate** (target: tăng từ baseline lên +30%)

### Supporting Metrics:
- Recommendation acceptance rate: >70%
- Time-to-book: giảm 50% vs manual
- User satisfaction (NPS): >50
- Elderly user adoption: >60%
- Cost per prevented no-show: <$5

---

## Risk Mitigation

| Risk | Impact | Mitigation |
|------|--------|------------|
| Privacy breach | Critical | End-to-end encryption, HIPAA-like compliance, audit logs |
| AI hallucination (sai lịch) | High | Always require user confirmation, show confidence scores |
| Low adoption (elderly) | High | Simple onboarding, voice support, family member delegation |
| Integration failure | Medium | Fallback to manual booking, graceful degradation |
| Spam perception | Medium | Adaptive frequency, easy opt-out, channel preference |

---

