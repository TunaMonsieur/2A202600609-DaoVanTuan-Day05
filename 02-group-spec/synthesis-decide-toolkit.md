# Toolkit — Từ Evidence Đến Build Slice

Dùng sau khi nhóm đã có evidence. Mục tiêu là chốt một build slice đủ nhỏ cho Day 06.

**Nhóm:** 4Ae · **Track:** Travel & Hospitality · **Product:** Vinpearl / MyVinpearl  
**Slice chốt:** **Gợi ý tour, buffet và dịch vụ** (không lịch trình theo ngày/giờ)

## 1. Gom evidence thành cụm

| Cụm (workflow/pain) | Evidence hỗ trợ |
|---|---|
| "Có nhiều tour/buffet/dịch vụ nhưng không biết chọn cái nào" | Self-use: nhiều tab Safari, VinWonders, buffet, combo; public: catalog tách rời. |
| "Khó so sánh dịch vụ nào hợp gia đình có trẻ em" | Self-use: không biết ưu tiên Safari vs VinWonders vs buffet; phỏng vấn đề xuất. |
| "Muốn đổi hướng gợi ý (buffet vs tour)" | Correction path trong thin SPEC. |
| "AI gợi ý gói/giá không thật" | ChatGPT pattern; failure giá/tồn kho real-time. |
| "Input mơ hồ" | Low-confidence path. |

## 2. Viết insight

```text
User gia đình có trẻ em chuẩn bị đi Vinpearl Phú Quốc không chỉ cần xem catalog tour, vé và buffet.
Họ cần danh sách gợi ý có lọc — tour, buffet, dịch vụ nào đáng cân nhắc, vì sao — rồi tự book trên kênh chính thức,
vì self-use: thông tin rải nhiều trang, khó so sánh; pain là chọn dịch vụ, không xếp lịch từng giờ (MVP).
```

## 3. Viết opportunity

```text
Cơ hội là dùng AI để augment chọn dịch vụ — form + catalog mẫu → 5–8 gợi ý + lý do + chỉnh chat,
giúp user rút ngắn thời gian duyệt catalog và tự tin trước khi book,
kiểm soát rủi ro: chỉ catalog; user quyết; không bịa giá/giờ/tồn kho real-time.
```

## 4. Chọn build slice

| Câu hỏi | Nhóm 4Ae |
|---|---|
| User cụ thể? | **Đạt.** Gia đình 2+1, Phú Quốc 3N2Đ, đang chọn tour/buffet/dịch vụ. |
| Task đủ hẹp? | **Đạt.** Form → list gợi ý → chỉnh chat; demo 3–5 phút. |
| AI decision rõ? | **Đạt.** AI lọc + giải thích; user book. |
| Failure path rõ? | **Đạt.** Low-confidence, real-time giá/tồn kho, correction, ngoài catalog. |
| Có evidence? | **Đạt.** Self-use + TripAdvisor/Klook + phỏng vấn planned. |

## 5. Quyết định

| Tình huống | Áp dụng |
|---|---|
| Ý tưởng quá rộng | **Đã cắt:** bỏ itinerary planner, fatigue, cost cả chuyến → backlog. |
| Rủi ro cao | **Augmentation**, catalog-only. |
| Demo 1 ngày | Form + service cards + 1 vòng chat correction + `services.json`. |

## 6. Câu chốt cuối

```text
Dựa trên self-use (nhiều tab tour/buffet/dịch vụ, khó chọn lọc cho gia đình) và pattern TripAdvisor/Klook,
nhóm sẽ build AI gợi ý tour, buffet và dịch vụ Vinpearl — form + 5–8 gợi ý từ catalog + chỉnh chat,
cho gia đình có trẻ em chuẩn bị chuyến đi Phú Quốc,
để giải quyết pain không biết tour/buffet/dịch vụ nào phù hợp,
bằng AI augment lọc và giải thích — user tự book,
test failure path gợi ý ngoài catalog / bịa giá real-time.
```

## 7. Backlog

- Lịch trình theo ngày/sáng/chiều/tối, fatigue check
- Ước tính chi phí cả chuyến (phòng + vé + ăn tổng)
- Booking, payment, MyVinpearl đầy đủ, FAQ chung
- Giá/giờ/tồn kho real-time, auto đặt tour
- API catalog Vinpearl live (MVP: `services.json`)
