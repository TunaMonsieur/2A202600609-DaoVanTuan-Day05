# Workshop — Mổ App AI Thật
**Sản phẩm:** MoMo — Moni  
**Người thực hiện:** Đào Văn Tuân
**Ngày:** 03/06/2026

---

## 1. Sản phẩm được chọn

**MoMo — Moni** — Trợ thủ tài chính, phân tích chi tiêu, chatbot trong app MoMo.

---

## 2. Promise vs Reality

**Product hứa gì?**  
Moni là trợ thủ tài chính cá nhân: hiểu chi tiêu của bạn, phân tích thói quen, đưa gợi ý tiết kiệm, trả lời câu hỏi tài chính tự nhiên bằng tiếng Việt.

**User nào được hứa sẽ được giúp?**  
Người dùng MoMo muốn kiểm soát tài chính cá nhân — theo dõi chi tiêu, đặt mục tiêu tiết kiệm, ra quyết định mua sắm dựa trên tình hình thực tế.

**Kỳ vọng AI làm được task nào?**
- Phân tích danh mục chi tiêu theo tháng
- Gợi ý có/không mua một món đồ dựa trên số dư/thu nhập
- Lập kế hoạch tiết kiệm cụ thể có con số

**Điểm gãy quan sát được:**

| Query thử | Kỳ vọng | Thực tế |
|---|---|---|
| "Tôi có nên mua iPhone không?" | Gợi ý dựa trên số dư/thu nhập cá nhân | Không hiểu intent — fallback chung chung |
| "Giúp tôi tiết kiệm 2 triệu tháng sau" | Lập kế hoạch cụ thể theo danh mục | Trả tips chung, không có action, không hỏi lại |

---

## 3. 4 Paths

### Happy path
Khi user hỏi đúng keyword Moni hiểu (ví dụ: "tháng này tôi tiêu bao nhiêu?"), Moni pull được số liệu và hiển thị danh mục chi tiêu. User thấy con số cụ thể, hài lòng.

### Low-confidence path
**Chưa có trong product.** Khi Moni không chắc intent (ví dụ: "mua iPhone có ổn không?"), hệ thống không hỏi lại, không show options, không chuyển người — chỉ fallback generic. User không có cách nào biết Moni đang không chắc.

### Failure path
**Không có signal thất bại rõ ràng.** Moni trả lời sai hoặc chung chung mà không thông báo giới hạn. User không biết AI đang fail hay đang đúng — không có "Tôi không có đủ thông tin để trả lời câu này."

### Correction path
**Không có.** Khi user push back ("tôi không thể cắt ăn ngoài"), Moni không rebalance, không lưu preference, không điều chỉnh plan. Correction biến mất, conversation kết thúc.

---

## 4. Finding thành quyết định product

**Finding chính:**

```
Khi user đặt financial goal cụ thể ("tiết kiệm 2 triệu tháng sau"),
AI respond bằng tips chung không dựa trên data cá nhân,
hậu quả là user không có plan khả thi, mất tin tưởng vào tính năng AI.
Lỗi thuộc layer: Intent (không hỏi lại để làm rõ) + Data-tool (không pull lịch sử chi tiêu) + UX Recovery (không có correction path).
Nên sửa bằng: (1) clarification question trước khi respond goal bất kỳ, (2) pull data 30 ngày từ MoMo wallet để personalize, (3) correction log khi user push back — rebalance sang danh mục khác.
```

**Finding phụ:**

```
Khi user hỏi quyết định mua hàng ("có nên mua iPhone không?"),
AI không nhận ra intent tài chính cá nhân, fallback mà không giải thích,
hậu quả là user bị kẹt, không biết phải hỏi lại thế nào.
Lỗi thuộc layer: Intent + UX Recovery.
Nên sửa bằng: low-confidence path — nhận diện intent mơ hồ, hỏi lại "Bạn muốn biết mình có đủ tiền không, hay so sánh với mục tiêu tiết kiệm?"
```

---

## 5. Sketch As-is / To-be

### As-is — Path 2: "Giúp tôi tiết kiệm 2 triệu tháng sau"

```
User gửi goal
    ↓
Moni nhận intent "tiết kiệm"
    ↓
(Điểm gãy) Trả tips chung chung ("hạn chế ăn ngoài, mua sắm...")
    ↓
Không tạo plan, không hỏi thu nhập/chi tiêu
    ↓
User bị kẹt — không biết làm gì tiếp theo
```

**Root cause:** Không access data cá nhân + không hỏi lại để clarify.

---

### To-be — Path 2 đã sửa

```
User gửi goal
    ↓
Hỏi lại 1 câu: "Tháng này bạn đã tiết kiệm được chưa?"
    ↓
Pull data: chi tiêu 30 ngày, danh mục lớn nhất
    ↓
Plan cụ thể: "Cắt 800k ăn ngoài + 1.2tr mua sắm"
    ↓
User đồng ý?
  → Có: Handoff — Button "Đặt mục tiêu" → tạo saving goal trong app
         → Reminder hàng tuần, tracking tự động
  → Không thể: Correction log — rebalance sang danh mục khác
                → Plan điều chỉnh: "Cắt 2tr từ giải trí thay vì ăn"
```

**4 điểm thêm mới:** hỏi lại · data pull · handoff · correction  
**Không thay đổi UI** — chỉ thay đổi conversation logic.

---


> **SPEC change:** Moni cần thêm clarification step bắt buộc trước khi respond bất kỳ financial goal nào — input là intent + data từ MoMo wallet, output là plan có con số cụ thể theo danh mục, kèm handoff action và correction path khi user push back.
