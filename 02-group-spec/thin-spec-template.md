
# Template — Thin SPEC Cuối Day 05 (StayMate AI)

Thin SPEC không phải PRD đầy đủ. Đây là bản cam kết đủ rõ để sáng Day 06 nhóm build ngay.


## 1. Track, product/app và user

* **Track:** Travel & Hospitality (Khách sạn / Resort nghỉ dưỡng phức hợp — In-Stay Hospitality)
* **Product/app thật:** StayMate AI — Trợ lý lưu trú trong phòng (In-Room Concierge / Service-on-Demand)
* **User cụ thể:** Khách đang lưu trú tại resort phức hợp (ví dụ: Vinpearl, các khu nghỉ dưỡng lớn), gồm gia đình có trẻ nhỏ/người già và nhóm bạn trẻ. Họ có nhu cầu hỏi đáp tiện ích và đặt dịch vụ nội khu (amenity, nhà hàng, spa, shuttle, late check-out) một cách tức thời, ngại gọi lễ tân chờ lâu và ngại tải/đăng nhập app đặt phòng (Zero-Install).
* **Nhóm có phải user thật không? Nếu không, khác ở đâu?:** Có, các thành viên đều từng lưu trú tại resort/khách sạn và gặp các điểm gãy: gọi lễ tân bận máy (E01, E04), thông tin tiện ích mỗi nơi nói một kiểu (E02, E05), đặt nhà hàng/spa rời rạc (E03, E08). Điểm khác biệt duy nhất là nhóm có nền tảng công nghệ nên dễ định hình giải pháp AI hơn khách phổ thông.

## 2. Evidence summary

| Evidence | Nguồn | User/pain nói lên điều gì? | SPEC phải đổi gì? |
|---|---|---|---|
| Hỏi tiện ích phải gọi lễ tân, tổng đài bận máy / chờ lâu (E01, E04). | Self-use & review Booking/Agoda | Khách muốn phản hồi tức thời cho nhu cầu nhỏ nhưng gấp, không muốn chờ điện thoại. | Bỏ kênh gọi điện làm mặc định. Để AI concierge trả lời FAQ tiện ích ngay trong phòng qua QR. |
| Thông tin tiện ích rải rác, giờ giấc mâu thuẫn (E02, E05). | Self-use & TripAdvisor | Khách thiếu nguồn tin cậy thống nhất để ra quyết định trong ngày. | AI trả lời từ một nguồn dữ liệu thống nhất (single source of truth), nêu rõ giờ cập nhật/nguồn. |
| Đặt nhà hàng/spa rời rạc, gọi từng nơi, dễ mất slot (E03, E08). | Self-use & Agoda | Quy trình đặt dịch vụ phân mảnh khiến khách nản và bỏ cuộc; hết slot không có phương án thay. | Gom yêu cầu về một hội thoại; AI draft yêu cầu + gợi ý khung giờ thay thế khi hết slot. |
| App nặng/lỗi đăng nhập, khách ngại tự phục vụ (E06). | Google Play | Rào cản onboarding chặn việc tự phục vụ qua app native. | Dùng Web App/Zalo Mini App qua QR (Zero-Install/Zero-Login), không cần tài khoản. |

## 3. Pain statement

```text
User là khách đang lưu trú tại resort phức hợp (gia đình có trẻ nhỏ/người già, nhóm bạn trẻ) đang gặp khó ở bước hỏi đáp tiện ích và đặt dịch vụ nội khu ngay trong lúc ở phòng,
vì kênh duy nhất thường là gọi lễ tân — hay bận máy/chờ lâu (E01, E04), thông tin tiện ích rải rác và mâu thuẫn (E02, E05), đặt nhà hàng/spa phải gọi từng nơi và dễ mất slot (E03, E08), trong khi app đặt phòng lại nặng và lỗi đăng nhập (E06),
dẫn tới user mất thời gian chờ đợi, bỏ lỡ dịch vụ muốn dùng và trải nghiệm lưu trú bị giảm giá trị.
Bằng chứng chính là các review trên Google Play/Booking/Agoda/TripAdvisor phàn nàn "gọi lễ tân mãi không bắt máy", "hỏi mỗi người nói một kiểu giờ tiện ích" và "đặt bàn gọi số nội bộ không ai nghe, lên tới nơi hết bàn".
```

## 4. Build slice

```text
Cho khách đang lưu trú tại resort, đang ở trong phòng và có nhu cầu hỏi tiện ích hoặc đặt một dịch vụ đơn giản,
prototype sẽ dùng AI (Gemini API) phân tích ngữ cảnh (số phòng + thời điểm lấy từ QR, dữ liệu tiện ích/slot dịch vụ giả lập) và tạo một hội thoại concierge ngắn (Conversational UI),
trả lời tức thời FAQ tiện ích từ nguồn dữ liệu thống nhất và tiếp nhận yêu cầu dịch vụ đơn giản (xin amenity, đặt bàn nhà hàng, đặt slot spa, xin late check-out) bằng 2-3 nút phản hồi nhanh, AI draft yêu cầu rồi định tuyến tới đúng bộ phận,
và xử lý failure mode (dịch vụ hết slot, hoặc yêu cầu vượt chính sách như đổi/hủy booking, hoàn tiền, khiếu nại) bằng cách gợi ý phương án thay thế ngay trong chatbox và hiển thị nút [Chuyển lễ tân] để escalate sang người thật.
```

## 5. Auto/Aug decision

Chọn một:

- [ ] **Augmentation:** AI gợi ý/draft/phân loại, user quyết cuối.
- [x] **Conditional automation:** AI tự làm trong case hẹp; case mơ hồ/rủi ro chuyển người.
- [ ] **Automation:** AI tự quyết và tự hành động.

**Lý do chọn:** Các nhu cầu hỏi tiện ích (FAQ) và yêu cầu amenity đơn giản có rủi ro thấp, đáp án rõ ràng → AI có thể tự xử lý tức thời để giảm tải lễ tân. Nhưng các thao tác có rủi ro về tiền/chính sách (đổi-hủy booking, hoàn tiền, khiếu nại) cần con người quyết định. Conditional automation cho phép AI tự động trong vùng an toàn và chủ động chuyển người ngay khi vượt ngưỡng.  
**Human role:** reviewer / decider / trainer / rescuer / none
- **rescuer (lễ tân/nhân viên):** nhận escalate khi AI không chắc, dịch vụ hết slot phức tạp, hoặc yêu cầu vượt chính sách.
- **decider (khách):** bấm xác nhận yêu cầu dịch vụ do AI draft trước khi gửi đi.

## 6. Four paths

| Path | Prototype phải thể hiện gì? |
|---|---|
| **Happy** | Khách quét QR trong phòng (Phòng 1208, 9:30 sáng). StayMate mở hội thoại: *"Chào anh/chị ở phòng 1208! Em có thể giúp gì ạ? Một số việc nhanh: 1. Giờ buffet sáng & hồ bơi, 2. Xin thêm khăn/nước, 3. Đặt bàn tối nay."* Khách bấm option 1 → AI trả lời ngay: *"Buffet sáng tới 10:00, hồ bơi mở 6:00–21:00, shuttle ra biển mỗi 30 phút."* (nguồn dữ liệu thống nhất). |
| **Low-confidence** | AI không chắc ý định hoặc thiếu dữ liệu (QR không gắn được số phòng / câu hỏi mơ hồ). StayMate hỏi lại bằng nút: *"Để em hỗ trợ đúng, anh/chị đang cần việc nào ạ?"* kèm `[Hỏi tiện ích]`, `[Đặt dịch vụ]`, `[Gặp lễ tân]`. |
| **Failure** | Khách đặt slot spa 18:00 nhưng khung giờ vừa kín. AI không im lặng mà cập nhật: *"Rất tiếc, 18:00 đã kín. Em còn 16:30 hoặc 19:30, anh/chị chọn giúp em nhé?"* kèm nút `[Chọn 16:30]`, `[Chọn 19:30]`, `[Chuyển lễ tân]`. |
| **Correction** | Khi khách bấm `[Chuyển lễ tân]` hoặc gõ *"Tôi muốn đổi phòng / hoàn tiền dịch vụ"* (vượt chính sách), AI lập tức dừng tự xử lý, tóm tắt yêu cầu và chuyển sang lễ tân, đồng thời ghi nhận phản hồi vào profile tạm của phiên lưu trú (VD: khách không thích gợi ý spa, ưu tiên dịch vụ trong nhà) để các gợi ý sau bám đúng nhu cầu. |

## 7. Failure mode nguy hiểm nhất

```text
Nếu khách yêu cầu một thao tác có hệ quả về tiền hoặc chính sách (đổi/hủy booking, hoàn tiền, khiếu nại tính phí sai) mà AI lại "tự tin" xác nhận như một yêu cầu dịch vụ thường,
AI có thể hứa hẹn sai (báo đã hủy/đã hoàn) trong khi hệ thống resort chưa thực sự xử lý,
hậu quả là khách hiểu nhầm, tranh chấp tiền bạc và mất niềm tin vào resort.
Prototype sẽ xử lý bằng một "danh sách intent rủi ro" (đổi/hủy, hoàn tiền, thanh toán, khiếu nại): khi phát hiện intent này, AI KHÔNG tự xác nhận, mà chuyển ngay sang chế độ escalate — tóm tắt yêu cầu cho khách xem, hiển thị nút [Chuyển lễ tân] và nêu rõ "việc này sẽ do nhân viên xác nhận", đồng thời log lại để nhân viên xử lý.
Owner kiểm thử path này là Tạ Duy Xuân.
```

## 8. Owner plan cho sáng Day 06

| Thành viên | Việc phụ trách (Day 06) | Bằng chứng cần có trong repo |
|---|---|---|
| Phan Võ Trọng Tiển - 2A202600781 | **Đầu việc 1**: Thiết kế Kịch bản & Dữ liệu giả lập | Dữ liệu giả lập tiện ích resort (giờ giấc), danh mục dịch vụ, slot spa/nhà hàng và bản đồ số phòng ↔ QR trong repo. |
| Nguyễn Bá Thành - 2A202600675 | **Đầu việc 2**: Lập trình Giao diện | Code Frontend Web/Zalo Mini App hiển thị hội thoại concierge, nút phản hồi nhanh và nút [Chuyển lễ tân]. |
| Võ Tấn Trung - 2A202600642 | **Đầu việc 3**: Thiết lập Prompt & AI Logic | System Prompt cho Gemini, danh sách intent rủi ro, và cấu trúc JSON input/output (intent, slot, action) trong SPEC. |
| Đào Văn Tuân - 2A202600609 | **Đầu việc 4**: Backend & Kết nối API | API Server kết nối Gemini API + Mock API tiện ích/slot dịch vụ + định tuyến yêu cầu tới "bộ phận" giả lập. |
| Phan Võ Trọng Tiển - 2A202600781 | **Đầu việc 5**: Kiểm thử kịch bản lỗi & Chuẩn bị Demo | Video demo 3 phút + Script thuyết trình + Slide nhóm + Kịch bản kiểm thử Failure Path (hết slot & intent rủi ro escalate). |
