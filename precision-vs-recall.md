# Precision hay Recall?

Mỗi sản phẩm nên ưu tiên **precision** (đừng nhầm) hay **recall** (đừng sót)?

| # | Sản phẩm | Ưu tiên | Lý do |
|---|----------|---------|-------|
| 1 | AI lọc nội dung cho app trẻ em | **Recall** | Bỏ sót nội dung xấu = trẻ thấy nội dung độc hại. Chặn nhầm nội dung lành chấp nhận được hơn. |
| 2 | Code autocomplete (kiểu Copilot) | **Precision** | Gợi ý sai code = dev tin theo → bug. Thà không gợi ý còn hơn gợi ý nhầm. |
| 3 | AI đọc X-quang phát hiện ung thư | **Recall** | Bỏ sót ca ung thư = bệnh nhân không được điều trị → nguy hiểm tính mạng. Nhầm dương tính thì bác sĩ kiểm tra lại được. |
| 4 | AI duyệt khoản vay ngân hàng | **Precision** | Duyệt nhầm người không đủ điều kiện = rủi ro tài chính. Thà từ chối nhầm còn hơn duyệt nhầm. |
| 5 | AI gợi ý bài hát (Spotify) | **Recall** | Bỏ sót bài hay = trải nghiệm kém. Gợi ý thêm vài bài không hợp lắm không sao, user tự skip được. |

**Đáp án: 1-R, 2-P, 3-R, 4-P, 5-R**
