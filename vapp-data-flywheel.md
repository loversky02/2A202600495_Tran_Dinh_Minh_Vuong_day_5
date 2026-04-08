# V-App V-AI — Data Flywheel Diagrams

**Dựa trên:** Bài tập UX (01-ux-exercise.md)
**Case study:** V-App — Trợ lý ảo V-AI
**Path yếu nhất:** Path 2 — Khi AI không chắc

---

## 1. Vấn đề hiện tại: Vòng lặp ĐỨNG (As-is)

```mermaid
graph TD
    A[User hỏi mơ hồ:<br/>Hôm nay làm gì hay?] --> B[V-AI tự assume<br/>location = Hà Nội]
    B --> C[Trả lời dài, generic<br/>không actionable]
    C --> D{User có<br/>tương tác?}
    D -->|Không có nút feedback| E[❌ User bỏ qua]
    D -->|Không có quick-reply| E
    D -->|Không có thumbs up/down| E
    E --> F[❌ KHÔNG thu được signal]
    F --> G[❌ AI KHÔNG học được gì]
    G --> H[❌ VÒNG LẶP ĐỨNG]
    H -.Lần sau vẫn sai.-> A
    
    style A fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#fff
    style B fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#fff
    style C fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#fff
    style D fill:#ef4444,stroke:#dc2626,stroke-width:2px,color:#fff
    style E fill:#ef4444,stroke:#dc2626,stroke-width:3px,color:#fff
    style F fill:#ef4444,stroke:#dc2626,stroke-width:3px,color:#fff
    style G fill:#ef4444,stroke:#dc2626,stroke-width:3px,color:#fff
    style H fill:#7f1d1d,stroke:#991b1b,stroke-width:4px,color:#fff
```

**Vấn đề:**
- Không có nút feedback (thumbs up/down)
- Không có quick-reply buttons
- Không có CTA actionable
- → Không thu được signal → AI không học được

---

## 2. Giải pháp: Vòng lặp HOẠT ĐỘNG (To-be)

```mermaid
graph TD
    A[User hỏi mơ hồ:<br/>Hôm nay làm gì hay?] --> B[V-AI hỏi lại bằng<br/>quick-reply buttons]
    B --> C[🍜 Ăn uống · 🏛️ Tham quan<br/>🎮 Giải trí · 📍 Gần tôi]
    C --> D[User chọn: 🍜 Ăn uống]
    D --> E[✅ Thu EXPLICIT signal:<br/>intent = ăn uống<br/>time = 12:00 trưa<br/>location = Hà Nội]
    E --> F[V-AI trả lời ngắn, focused:<br/>3 quán phở gần đây]
    F --> G[Quán #1: Phở Thìn<br/>Quán #2: Phở Bát Đàn ⭐<br/>Quán #3: Phở Lý Quốc Sư]
    G --> H[User click Xem bản đồ<br/>cho quán #2]
    H --> I[✅ Thu IMPLICIT signal:<br/>preference = quán #2<br/>skip = quán #1, #3]
    I --> J[Dữ liệu về database]
    J --> K[AI phân tích & học:<br/>12h + làm gì hay = ăn uống 75%<br/>User này thích Phở Bát Đàn]
    K --> L[Model cải thiện]
    L --> M[Lần sau:<br/>Tự động gợi ý Ăn uống lên đầu<br/>Ưu tiên Phở Bát Đàn]
    M -.Vòng lặp tiếp tục.-> A
    
    style A fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#fff
    style B fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#fff
    style C fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#fff
    style D fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#fff
    style E fill:#10b981,stroke:#059669,stroke-width:3px,color:#fff
    style F fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#fff
    style G fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#fff
    style H fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#fff
    style I fill:#10b981,stroke:#059669,stroke-width:3px,color:#fff
    style J fill:#0891b2,stroke:#0e7490,stroke-width:2px,color:#fff
    style K fill:#0891b2,stroke:#0e7490,stroke-width:2px,color:#fff
    style L fill:#0891b2,stroke:#0e7490,stroke-width:2px,color:#fff
    style M fill:#10b981,stroke:#059669,stroke-width:3px,color:#fff
```

**Cải thiện:**
- Thêm quick-reply buttons → thu intent (explicit)
- Thêm CTA "Xem bản đồ" → thu preference (implicit)
- Track user behavior → biết user thích gì
- → Thu được signal → AI học và cải thiện

---

## 3. So sánh As-is vs To-be

```mermaid
graph LR
    subgraph AsIs[" ❌ AS-IS: Vòng lặp ĐỨNG "]
        A1[User hỏi mơ hồ]
        A2[AI assume context]
        A3[Trả lời generic]
        A4[User bỏ qua]
        A5[KHÔNG thu signal]
        A6[AI không học]
        A1 --> A2 --> A3 --> A4 --> A5 --> A6
    end
    
    subgraph ToBe[" ✅ TO-BE: Vòng lặp HOẠT ĐỘNG "]
        B1[User hỏi mơ hồ]
        B2[AI hỏi lại quick-reply]
        B3[User chọn option]
        B4[Thu EXPLICIT signal]
        B5[AI trả lời focused]
        B6[User click CTA]
        B7[Thu IMPLICIT signal]
        B8[AI học & cải thiện]
        B1 --> B2 --> B3 --> B4 --> B5 --> B6 --> B7 --> B8
        B8 -.Loop.-> B1
    end
    
    style AsIs fill:#fee2e2,stroke:#dc2626,stroke-width:3px
    style ToBe fill:#d1fae5,stroke:#10b981,stroke-width:3px
```

---

## 4. 3 loại Signal thu được từ To-be

```mermaid
graph TB
    A[User tương tác với V-AI] --> B{Loại signal}
    
    B -->|1| C[IMPLICIT<br/>Ngầm]
    B -->|2| D[EXPLICIT<br/>Trực tiếp]
    B -->|3| E[CORRECTION<br/>Sửa lỗi]
    
    C --> C1[• Click vào quán #2<br/>• Bỏ qua quán #1, #3<br/>• Thời gian xem<br/>• Scroll behavior]
    
    D --> D1[• Chọn quick-reply: 🍜<br/>• Thumbs up/down future<br/>• Rating sao future<br/>• Share với bạn]
    
    E --> E1[• Sửa location từ HN → HCM<br/>• Ghi đè gợi ý<br/>• Report sai<br/>• Chọn quán khác]
    
    C1 --> F[Database: User behavior]
    D1 --> F
    E1 --> F
    
    F --> G[Phân tích pattern:<br/>12h + làm gì = ăn 75%<br/>User thích phở > bún]
    
    G --> H[Fine-tune model]
    
    H --> I[Lần sau gợi ý tốt hơn]
    
    style A fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#fff
    style B fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#fff
    style C fill:#1e3a8a,stroke:#1e40af,stroke-width:2px,color:#fff
    style D fill:#dc2626,stroke:#b91c1c,stroke-width:2px,color:#fff
    style E fill:#64748b,stroke:#475569,stroke-width:2px,color:#fff
    style F fill:#0891b2,stroke:#0e7490,stroke-width:2px,color:#fff
    style G fill:#0891b2,stroke:#0e7490,stroke-width:2px,color:#fff
    style H fill:#0891b2,stroke:#0e7490,stroke-width:2px,color:#fff
    style I fill:#10b981,stroke:#059669,stroke-width:3px,color:#fff
```

---

## 5. Data Flywheel: V1 → V2 → V3

```mermaid
graph TB
    subgraph V1[" V1: HIỆN TẠI (Vòng lặp đứng) "]
        A1[Nguồn dữ liệu:<br/>Không có - user bỏ qua]
        A2[Độ chính xác:<br/>Thấp - assume sai context]
        A3[Kết quả:<br/>User không dùng tiếp]
        A1 --> A2 --> A3
    end
    
    subgraph V2[" V2: TO-BE (Quick-reply + CTA) "]
        B1[Dữ liệu tổng hợp:<br/>600+ interactions<br/>User chọn gì, click gì]
        B2[Độ chính xác:<br/>60-75% - biết intent]
        B3[Kết quả:<br/>Gợi ý đúng context hơn]
        B1 --> B2 --> B3
    end
    
    subgraph V3[" V3: TƯƠNG LAI (Personalized) "]
        C1[Liên tục thu data:<br/>+ User history<br/>+ Location real-time<br/>+ Time of day]
        C2[Độ chính xác:<br/>75-85% - personalized]
        C3[Kết quả:<br/>Tự động gợi ý đúng<br/>không cần hỏi lại]
        C1 --> C2 --> C3
    end
    
    V1 ==>|Thêm quick-reply<br/>+ CTA buttons| V2
    V2 ==>|Thu thêm<br/>user history| V3
    
    style V1 fill:#fee2e2,stroke:#dc2626,stroke-width:2px
    style V2 fill:#fef3c7,stroke:#f59e0b,stroke-width:2px
    style V3 fill:#d1fae5,stroke:#10b981,stroke-width:2px
```

---

## 6. Timeline: Từ feedback → Model cải thiện

```mermaid
gantt
    title Tốc độ vòng lặp V-App (Mục tiêu < 2 tuần)
    dateFormat YYYY-MM-DD
    section Thu thập
    User chọn quick-reply (real-time)     :done, collect, 2024-01-01, 1d
    User click CTA (real-time)             :done, click, 2024-01-01, 1d
    section Xử lý
    Batch process 600+ interactions        :active, process, 2024-01-02, 5d
    Phân tích pattern (12h = ăn 75%)       :active, analyze, 2024-01-07, 2d
    section Model
    Fine-tune model với data mới           :finetune, 2024-01-09, 7d
    section Deploy
    A/B test 10% user                      :deploy, 2024-01-16, 2d
    Deploy 100% nếu tốt hơn                :deploy2, 2024-01-18, 1d
    section Kết quả
    User thấy gợi ý tốt hơn                :result, 2024-01-19, 7d
```

---

## 7. Sai lầm phá vỡ Flywheel (V-App hiện tại)

```mermaid
graph TD
    A[V-App build AI chatbot] --> B{Có thiết kế<br/>thu dữ liệu?}
    
    B -->|❌ KHÔNG| C[Sai lầm 1:<br/>Không có quick-reply<br/>Không có thumbs up/down]
    
    C --> D[User không thể<br/>cho feedback]
    D --> E[❌ Không thu được signal]
    E --> F[❌ AI không biết<br/>user thích gì]
    F --> G[❌ Lần sau vẫn<br/>trả lời generic]
    G --> H[❌ User bỏ qua]
    H --> I[❌ VÒNG LẶP ĐỨNG]
    
    B -->|✅ CÓ| J[Thêm quick-reply<br/>Thêm CTA buttons<br/>Thêm thumbs up/down]
    J --> K[User có thể<br/>tương tác]
    K --> L[✅ Thu được signal]
    L --> M[✅ AI học được<br/>user thích gì]
    M --> N[✅ Lần sau gợi ý<br/>đúng hơn]
    N --> O[✅ User dùng nhiều hơn]
    O --> P[✅ VÒNG LẶP QUAY]
    
    style A fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#fff
    style B fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#fff
    style C fill:#ef4444,stroke:#dc2626,stroke-width:2px,color:#fff
    style I fill:#7f1d1d,stroke:#991b1b,stroke-width:4px,color:#fff
    style J fill:#10b981,stroke:#059669,stroke-width:2px,color:#fff
    style P fill:#065f46,stroke:#047857,stroke-width:4px,color:#fff
```

---

## 8. Roadmap cải thiện V-App

```mermaid
graph LR
    subgraph Now[" 🔴 HIỆN TẠI "]
        A[Không có feedback<br/>Không có quick-reply<br/>Assume context]
    end
    
    subgraph Phase1[" 🟡 PHASE 1 (2 tuần) "]
        B[Thêm quick-reply buttons<br/>Thêm CTA Xem bản đồ<br/>Thu explicit + implicit signal]
    end
    
    subgraph Phase2[" 🟢 PHASE 2 (1 tháng) "]
        C[Thêm thumbs up/down<br/>Thêm Share với bạn<br/>Thu 600+ interactions]
    end
    
    subgraph Phase3[" 🔵 PHASE 3 (3 tháng) "]
        D[Personalized gợi ý<br/>Tự động detect context<br/>Không cần hỏi lại]
    end
    
    Now ==> Phase1
    Phase1 ==> Phase2
    Phase2 ==> Phase3
    
    style Now fill:#fee2e2,stroke:#dc2626,stroke-width:3px
    style Phase1 fill:#fef3c7,stroke:#f59e0b,stroke-width:3px
    style Phase2 fill:#d1fae5,stroke:#10b981,stroke-width:3px
    style Phase3 fill:#dbeafe,stroke:#3b82f6,stroke-width:3px
```

---

## 9. Metrics đo lường thành công

```mermaid
graph TB
    A[V-App Data Flywheel] --> B[Input Metrics]
    A --> C[Process Metrics]
    A --> D[Output Metrics]
    
    B --> B1[• % user chọn quick-reply<br/>• % user click CTA<br/>• Số interactions/user/day]
    
    C --> C1[• Thời gian từ feedback → model mới<br/>• Số data points thu được/tuần<br/>• % data quality cao]
    
    D --> D1[• Accuracy tăng: 30% → 75%<br/>• User retention tăng<br/>• Session length tăng<br/>• User quay lại nhiều hơn]
    
    style A fill:#3b82f6,stroke:#2563eb,stroke-width:3px,color:#fff
    style B fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#fff
    style C fill:#0891b2,stroke:#0e7490,stroke-width:2px,color:#fff
    style D fill:#10b981,stroke:#059669,stroke-width:2px,color:#fff
```

---

## 10. Checklist: V-App có vòng lặp tốt chưa?

```mermaid
graph TD
    A[V-App Data Flywheel] --> B{Thu được<br/>3 loại signal?}
    B -->|❌ Chưa| Z1[Thêm quick-reply<br/>Thêm CTA<br/>Thêm thumbs up/down]
    B -->|✅ Có| C{Track được<br/>user behavior?}
    
    C -->|❌ Chưa| Z2[Track click, time spent<br/>Track skip, scroll]
    C -->|✅ Có| D{Data về model<br/>< 2 tuần?}
    
    D -->|❌ Chưa| Z3[Tăng tốc pipeline<br/>Batch process nhanh hơn]
    D -->|✅ Có| E{Đo được<br/>accuracy tăng?}
    
    E -->|❌ Chưa| Z4[Setup A/B test<br/>So sánh before/after]
    E -->|✅ Có| F{Launch<br/>scope nhỏ?}
    
    F -->|❌ Chưa| Z5[Pilot với 1 thành phố<br/>hoặc 1 category trước]
    F -->|✅ Có| G[✅ VÒNG LẶP TỐT]
    
    Z1 --> A
    Z2 --> A
    Z3 --> A
    Z4 --> A
    Z5 --> A
    
    style A fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#fff
    style G fill:#10b981,stroke:#059669,stroke-width:4px,color:#fff
    style Z1 fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#fff
    style Z2 fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#fff
    style Z3 fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#fff
    style Z4 fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#fff
    style Z5 fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#fff
```

---

## Cách sử dụng

1. **Copy code Mermaid** từ các section trên
2. **Paste vào [mermaid.live](https://mermaid.live)** để xem preview
3. **Export PNG/SVG** để dùng trong:
   - Slide thuyết trình (Phần 4 - Share + vote)
   - Báo cáo bài tập
   - Portfolio case study

4. **Customize:**
   - Đổi màu sắc theo brand V-App
   - Thêm logo/icon
   - Điều chỉnh text cho phù hợp

---

## Tóm tắt: Key Takeaways

**Vấn đề hiện tại (As-is):**
- ❌ Không có quick-reply buttons
- ❌ Không có thumbs up/down
- ❌ Không có CTA actionable
- → Vòng lặp ĐỨNG

**Giải pháp (To-be):**
- ✅ Thêm quick-reply → thu explicit signal
- ✅ Thêm CTA buttons → thu implicit signal
- ✅ Track user behavior → biết preference
- → Vòng lặp HOẠT ĐỘNG

**Kết quả:**
- Accuracy tăng từ 30% → 75%+
- User retention tăng
- AI học được user thích gì
- Personalized gợi ý

---

*Dựa trên:*
- 01-ux-exercise.md (V-App case study)
- data-flywheel-guide.md (Framework)
- 04-reference-document.md (Microsoft Dragon, Feedback Loop)

