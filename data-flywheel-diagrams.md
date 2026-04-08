# Data Flywheel — Diagrams (Mermaid)

**Hướng dẫn:** Copy code Mermaid vào editor hỗ trợ (GitHub, Notion, Obsidian) hoặc [mermaid.live](https://mermaid.live)

---

## 1. Vòng lặp Data Flywheel cơ bản

```mermaid
graph LR
    A[Người dùng<br/>sử dụng] --> B[Thu thập<br/>dữ liệu]
    B --> C[AI học từ<br/>dữ liệu]
    C --> D[Sản phẩm<br/>tốt hơn]
    D --> E[Thu hút<br/>thêm người dùng]
    E --> A
    
    style A fill:#1e3a8a,stroke:#1e40af,stroke-width:3px,color:#fff
    style B fill:#0891b2,stroke:#0e7490,stroke-width:2px,color:#fff
    style C fill:#0891b2,stroke:#0e7490,stroke-width:2px,color:#fff
    style D fill:#059669,stroke:#047857,stroke-width:2px,color:#fff
    style E fill:#059669,stroke:#047857,stroke-width:2px,color:#fff
```

---

## 2. Vòng lặp 4 bước (Ingest → Digest → Output → Repeat)

```mermaid
graph TB
    A[1. INGEST<br/>Thu thập signal] --> B[2. DIGEST<br/>Xử lý & phân tích]
    B --> C[3. OUTPUT<br/>Model cải thiện]
    C --> D[4. REPEAT<br/>User thấy kết quả tốt hơn]
    D --> A
    
    A1[• Implicit: click, time<br/>• Explicit: thumbs up/down<br/>• Correction: user sửa] -.-> A
    B1[• Phân loại lỗi<br/>• Tìm pattern<br/>• Qualitative analysis] -.-> B
    C1[• Fine-tune model<br/>• A/B test<br/>• Deploy] -.-> C
    D1[• Accuracy tăng<br/>• User hài lòng<br/>• Dùng nhiều hơn] -.-> D
    
    style A fill:#dc2626,stroke:#b91c1c,stroke-width:3px,color:#fff
    style B fill:#ea580c,stroke:#c2410c,stroke-width:3px,color:#fff
    style C fill:#ca8a04,stroke:#a16207,stroke-width:3px,color:#fff
    style D fill:#16a34a,stroke:#15803d,stroke-width:3px,color:#fff
```

---

## 3. V-App V-AI — As-is (Vòng lặp đứng)

```mermaid
graph TD
    A[User hỏi:<br/>'Hôm nay làm gì hay?'] --> B[V-AI trả lời<br/>assume Hà Nội, generic]
    B --> C{User tương tác?}
    C -->|Không| D[❌ User bỏ qua]
    C -->|Có nhưng không có nút feedback| D
    D --> E[❌ KHÔNG thu được signal]
    E --> F[❌ AI KHÔNG học được gì]
    F --> G[Vòng lặp ĐỨNG]
    
    style A fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#fff
    style B fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#fff
    style C fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#fff
    style D fill:#ef4444,stroke:#dc2626,stroke-width:3px,color:#fff
    style E fill:#ef4444,stroke:#dc2626,stroke-width:3px,color:#fff
    style F fill:#ef4444,stroke:#dc2626,stroke-width:3px,color:#fff
    style G fill:#7f1d1d,stroke:#991b1b,stroke-width:4px,color:#fff
```

---

## 4. V-App V-AI — To-be (Vòng lặp hoạt động)

```mermaid
graph TD
    A[User hỏi:<br/>'Hôm nay làm gì hay?'] --> B[V-AI hỏi lại:<br/>🍜 Ăn uống · 🏛️ Tham quan<br/>🎮 Giải trí · 📍 Gần tôi]
    B --> C[User chọn: 🍜 Ăn uống]
    C --> D[✅ Thu signal EXPLICIT:<br/>intent = ăn uống]
    D --> E[V-AI trả lời:<br/>3 quán phở gần đây]
    E --> F[User click Xem bản đồ<br/>cho quán #2]
    F --> G[✅ Thu signal IMPLICIT:<br/>preference = quán #2]
    G --> H[Dữ liệu về model]
    H --> I[AI học & cải thiện]
    I --> J[Lần sau gợi ý<br/>quán phở lên đầu]
    J --> A
    
    style A fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#fff
    style B fill:#8b5cf6,stroke:#7c3aed,stroke-width:2px,color:#fff
    style C fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#fff
    style D fill:#10b981,stroke:#059669,stroke-width:3px,color:#fff
    style E fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#fff
    style F fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#fff
    style G fill:#10b981,stroke:#059669,stroke-width:3px,color:#fff
    style H fill:#0891b2,stroke:#0e7490,stroke-width:2px,color:#fff
    style I fill:#0891b2,stroke:#0e7490,stroke-width:2px,color:#fff
    style J fill:#10b981,stroke:#059669,stroke-width:2px,color:#fff
```

---

## 5. Agency Progression: V1 → V2 → V3

```mermaid
graph TB
    subgraph V1[" V1: AUGMENTATION (Routing) "]
        A1[Nguồn dữ liệu:<br/>Synthetic / ít]
        A2[Độ chính xác:<br/>30-60%]
        A3[Kết quả:<br/>Dữ liệu → kết quả tệ]
        A1 --> A2 --> A3
    end
    
    subgraph V2[" V2: COPILOT (Gợi ý) "]
        B1[Dữ liệu tổng hợp:<br/>600K ca thực tế]
        B2[+ Chuyên gia đánh giá]
        B3[Độ chính xác:<br/>~75%]
        B4[Kết quả:<br/>Dữ liệu thật → nhảy vọt]
        B1 --> B2 --> B3 --> B4
    end
    
    subgraph V3[" V3: AUTOMATION (Tự động) "]
        C1[Liên tục thu<br/>dữ liệu mới]
        C2[Chuyên gia đánh giá<br/>hàng ngày]
        C3[Độ chính xác:<br/>83%+]
        C4[Kết quả:<br/>Data mới → tốt nửa]
        C1 --> C2 --> C3 --> C4
    end
    
    V1 ==> V2
    V2 ==> V3
    
    style V1 fill:#fee2e2,stroke:#dc2626,stroke-width:2px
    style V2 fill:#fef3c7,stroke:#f59e0b,stroke-width:2px
    style V3 fill:#d1fae5,stroke:#10b981,stroke-width:2px
```

---

## 6. Microsoft Dragon — Data Flywheel thực tế

```mermaid
graph LR
    subgraph Phase1[" Phiên bản V1 "]
        A[Nguồn dữ liệu:<br/>Synthetic]
        B[Độ chính xác:<br/>30-60%]
        C[Kết quả:<br/>Dữ liệu → kết quả tệ]
    end
    
    subgraph Phase2[" Phiên bản V2 "]
        D[Dữ liệu tổng hợp:<br/>600K ca + chuyên gia]
        E[Độ chính xác:<br/>~75%]
        F[Kết quả:<br/>Dữ liệu thật → nhảy vọt]
    end
    
    subgraph Phase3[" Phiên bản V3 "]
        G[Liên tục thu dữ liệu]
        H[Bác sĩ đánh giá hàng ngày]
        I[Độ chính xác:<br/>83%+]
    end
    
    Phase1 --> Phase2
    Phase2 --> Phase3
    Phase3 -.Loop liên tục.-> Phase3
    
    style Phase1 fill:#fecaca,stroke:#dc2626,stroke-width:3px
    style Phase2 fill:#fed7aa,stroke:#ea580c,stroke-width:3px
    style Phase3 fill:#86efac,stroke:#16a34a,stroke-width:3px
```

---

## 7. 3 loại Feedback Signal

```mermaid
graph TB
    A[User tương tác với AI] --> B{Loại signal}
    
    B -->|1| C[IMPLICIT<br/>Ngầm]
    B -->|2| D[EXPLICIT<br/>Trực tiếp]
    B -->|3| E[CORRECTION<br/>Sửa lỗi]
    
    C --> C1[• Thời gian xem<br/>• Cuộn trang<br/>• Bỏ qua<br/>• Click vào đâu]
    D --> D1[• Thumbs up/down<br/>• Rating sao<br/>• Báo cáo<br/>• Đánh dấu]
    E --> E1[• Sửa text AI viết<br/>• Đánh dấu sai<br/>• Ghi đè quyết định]
    
    C1 --> F[Thu thập vào database]
    D1 --> F
    E1 --> F
    
    F --> G[Phân tích & học]
    G --> H[Model cải thiện]
    
    style A fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#fff
    style B fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#fff
    style C fill:#1e3a8a,stroke:#1e40af,stroke-width:2px,color:#fff
    style D fill:#dc2626,stroke:#b91c1c,stroke-width:2px,color:#fff
    style E fill:#64748b,stroke:#475569,stroke-width:2px,color:#fff
    style F fill:#0891b2,stroke:#0e7490,stroke-width:2px,color:#fff
    style G fill:#0891b2,stroke:#0e7490,stroke-width:2px,color:#fff
    style H fill:#16a34a,stroke:#15803d,stroke-width:3px,color:#fff
```

---

## 8. Sai lầm phá vỡ Flywheel

```mermaid
graph TD
    A[Bắt đầu build AI product] --> B{Có thiết kế<br/>thu dữ liệu?}
    
    B -->|❌ Không| C[Sai lầm 1:<br/>Không có nút feedback]
    B -->|✅ Có| D{Thu đúng<br/>loại data?}
    
    C --> E[User không thể<br/>cho feedback]
    E --> F[❌ Không có signal]
    
    D -->|❌ Không| G[Sai lầm 2:<br/>Thu sai thứ]
    D -->|✅ Có| H{Data về<br/>model?}
    
    G --> I[Chỉ đếm lượt dùng<br/>không biết sai ở đâu]
    I --> F
    
    H -->|❌ Không| J[Sai lầm 3:<br/>Thu rồi không dùng]
    H -->|✅ Có| K[✅ Vòng lặp hoạt động]
    
    J --> L[Log đầy<br/>model không đổi]
    L --> F
    
    F --> M[VÒNG LẶP ĐỨNG]
    K --> N[Data Flywheel quay]
    
    style A fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#fff
    style B fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#fff
    style C fill:#ef4444,stroke:#dc2626,stroke-width:2px,color:#fff
    style D fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#fff
    style G fill:#ef4444,stroke:#dc2626,stroke-width:2px,color:#fff
    style H fill:#f59e0b,stroke:#d97706,stroke-width:2px,color:#fff
    style J fill:#ef4444,stroke:#dc2626,stroke-width:2px,color:#fff
    style K fill:#10b981,stroke:#059669,stroke-width:3px,color:#fff
    style M fill:#7f1d1d,stroke:#991b1b,stroke-width:4px,color:#fff
    style N fill:#065f46,stroke:#047857,stroke-width:4px,color:#fff
```

---

## 9. Timeline: Tốc độ vòng lặp (Metabolism)

```mermaid
gantt
    title Tốc độ vòng lặp Data Flywheel (Mục tiêu < 2 tuần)
    dateFormat YYYY-MM-DD
    section Thu thập
    User feedback (real-time)           :done, feedback, 2024-01-01, 1d
    section Xử lý
    Batch process data (1-7 ngày)       :active, process, 2024-01-02, 7d
    section Model
    Fine-tune model (1-2 tuần)          :finetune, 2024-01-09, 14d
    section Deploy
    A/B test & deploy (1 ngày)          :deploy, 2024-01-23, 1d
    section Kết quả
    User thấy cải thiện (2-4 tuần)      :result, 2024-01-24, 28d
```

---

## 10. So sánh: Synthetic vs Real Data

```mermaid
graph LR
    subgraph Synthetic[" Synthetic Data "]
        A1[Tự tạo data]
        A2[Accuracy: 30-60%]
        A3[Effort: Thấp]
        A4[Dùng cho: V1 launch]
        A1 --> A2 --> A3 --> A4
    end
    
    subgraph Real[" Real Data "]
        B1[User thật]
        B2[Accuracy: 60-75%]
        B3[Effort: Trung bình]
        B4[Dùng cho: V2 scale]
        B1 --> B2 --> B3 --> B4
    end
    
    subgraph Expert[" Real + Expert "]
        C1[User + Chuyên gia]
        C2[Accuracy: 75-83%+]
        C3[Effort: Cao]
        C4[Dùng cho: V3 optimize]
        C1 --> C2 --> C3 --> C4
    end
    
    Synthetic ==> Real
    Real ==> Expert
    
    style Synthetic fill:#fecaca,stroke:#dc2626,stroke-width:2px
    style Real fill:#fed7aa,stroke:#ea580c,stroke-width:2px
    style Expert fill:#86efac,stroke:#16a34a,stroke-width:2px
```

---

## 11. Data Flywheel vs Alexa Effect (Vòng xoáy đi xuống)

```mermaid
graph TB
    subgraph Good[" ✅ Data Flywheel (Vòng lặp tốt) "]
        A1[Chất lượng tốt] --> A2[User dùng nhiều]
        A2 --> A3[Thu nhiều data]
        A3 --> A4[AI càng tốt]
        A4 --> A1
    end
    
    subgraph Bad[" ❌ Alexa Effect (Vòng xoáy xuống) "]
        B1[Chất lượng kém] --> B2[User ngừng dùng]
        B2 --> B3[Mất data]
        B3 --> B4[AI càng kém]
        B4 --> B1
    end
    
    style Good fill:#d1fae5,stroke:#10b981,stroke-width:3px
    style Bad fill:#fee2e2,stroke:#dc2626,stroke-width:3px
```

---

## 12. Checklist: Vòng lặp tốt

```mermaid
graph TD
    A[Vòng lặp Data Flywheel] --> B{Thu được<br/>3 loại signal?}
    B -->|✅| C{Có nút<br/>feedback?}
    B -->|❌| Z[❌ Fail]
    
    C -->|✅| D{Track<br/>behavior?}
    C -->|❌| Z
    
    D -->|✅| E{Cho user<br/>sửa kết quả?}
    D -->|❌| Z
    
    E -->|✅| F{Data về model<br/>< 2 tuần?}
    E -->|❌| Z
    
    F -->|✅| G{Đo được<br/>accuracy tăng?}
    F -->|❌| Z
    
    G -->|✅| H{Launch<br/>scope nhỏ?}
    G -->|❌| Z
    
    H -->|✅| I{Có expert<br/>review?}
    H -->|❌| Z
    
    I -->|✅| J[✅ Vòng lặp TỐT]
    I -->|❌| K[⚠️ Vòng lặp OK<br/>nhưng chưa tối ưu]
    
    style A fill:#3b82f6,stroke:#2563eb,stroke-width:2px,color:#fff
    style J fill:#10b981,stroke:#059669,stroke-width:4px,color:#fff
    style K fill:#f59e0b,stroke:#d97706,stroke-width:3px,color:#fff
    style Z fill:#ef4444,stroke:#dc2626,stroke-width:3px,color:#fff
```

---

## Hướng dẫn sử dụng

1. **Copy code Mermaid** từ các section trên
2. **Paste vào:**
   - GitHub README.md (tự render)
   - [mermaid.live](https://mermaid.live) (preview & export PNG/SVG)
   - Notion (dùng `/code` → chọn Mermaid)
   - Obsidian (cài plugin Mermaid)
   - VS Code (cài extension Markdown Preview Mermaid)

3. **Customize:**
   - Đổi text trong `[]` để phù hợp sản phẩm của bạn
   - Đổi màu: `fill:#HEX_COLOR`
   - Thêm/bớt node theo nhu cầu

---

*Tài liệu tham khảo:*
- data-flywheel-guide.md
- 01-ux-exercise.md (V-App case study)
- 04-reference-document.md (Microsoft Dragon)

