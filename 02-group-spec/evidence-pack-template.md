
# Evidence Pack — StayMate AI

Nộp kèm thin SPEC cuối Day 05.

>

## 1. Nhóm và track

**Tên nhóm:** Group A9
**Thành viên nhóm:**
- Phan Võ Trọng Tiển — 2A202600781
- Võ Tấn Trung  — 2A202600642
- Đào Văn Tuân — 2A202600609
- Nguyễn Bá Thành — 2A202600675

**Track:** Travel & Hospitality (Khách sạn / Resort nghỉ dưỡng phức hợp — In-Stay Hospitality)  
**Product/app đã chọn:** StayMate AI — Trợ lý lưu trú trong phòng (In-Room Concierge / Service-on-Demand)  
**Build slice đang nghĩ:** Web App/Zalo Mini App kích hoạt qua mã QR đặt trong phòng hoặc trên thẻ phòng (Zero-Install, không cần đăng nhập app). Khi quét, hệ thống tự nhận diện số phòng + thời điểm hiện tại và mở một hội thoại concierge ngắn (Conversational UI dùng Gemini API). AI trả lời ngay các câu hỏi về tiện ích (giờ buffet, hồ bơi, shuttle, gym, spa) và tiếp nhận yêu cầu dịch vụ đơn giản (xin thêm khăn/nước, đặt bàn nhà hàng, đặt slot spa, xin late check-out) bằng 2–3 nút phản hồi nhanh, thay vì bắt khách gọi điện lễ tân hoặc lục trong app đặt phòng nặng nề.

## 2. Self-use evidence

Nhóm tự dùng app/workflow lưu trú thật và ghi lại điểm gãy.

| Evidence ID | Observation | Screenshot/link | Path liên quan | Điều học được |
|---|---|---|---|---|
| **E01** | Muốn hỏi "hồ bơi mấy giờ đóng cửa, buffet sáng tới mấy giờ" nhưng phải gọi lễ tân; tổng đài nội bộ bận máy hoặc đổ chuông lâu, phải xuống tận quầy hỏi. | [E01.jpg](evidence/E01.jpg)<br>![E01](evidence/E01.jpg) | **Failure (Service Latency / High Friction)** | Tránh ép khách gọi điện. Để AI trả lời FAQ tiện ích tức thời ngay trong phòng qua QR, giảm tải cho lễ tân. |
| **E02** | Thông tin tiện ích nằm rải rác: tờ rơi trong phòng, TV menu, app riêng, bảng thông báo sảnh — giờ giấc còn mâu thuẫn nhau, không biết tin cái nào. | [E02.png](evidence/E02.png)<br>![E02](evidence/E02.png) | **Low-confidence** | Cần một nguồn trả lời thống nhất (single source of truth) để AI tóm tắt nhanh, có ghi rõ nguồn/giờ cập nhật. |
| **E03** | Đặt bàn nhà hàng / spa trong resort phải gọi từng nơi hoặc đi tới quầy từng dịch vụ; quy trình rời rạc, dễ nản và bỏ cuộc. | `evidence/E03.png` *(chưa chụp)* | **Failure / Correction** | Gom yêu cầu dịch vụ về một hội thoại. AI draft yêu cầu, chuyển bộ phận phù hợp; khách xác nhận bằng nút bấm. |

## 3. User / review / social evidence

Nguồn có thể là review App Store/Play, Booking/Agoda/TripAdvisor, group Facebook du lịch, comment, phỏng vấn nhanh, hoặc nguồn public khác.


### 3.1. Fitted Evidences (Khớp trực tiếp với Trợ lý lưu trú & Dịch vụ theo yêu cầu)

Các bằng chứng/review khớp với pain points về độ trễ phản hồi của lễ tân, thiếu thông tin tiện ích thống nhất, quy trình đặt dịch vụ rời rạc và rào cản gọi điện.

| Evidence ID | Quote / review / observation | Nguồn / Cách tìm | User là ai? | Pain/failure mode |
|---|---|---|---|---|
| **E04** | "Gọi lễ tân mãi không bắt máy, muốn xin thêm khăn với nước suối mà chờ gần 30 phút chưa thấy ai lên." | Review resort trên Booking/Agoda — search resort + `lễ tân` / `dịch vụ phòng`. *(Trích dẫn đại diện, nhóm sẽ verify lại link gốc trước M1.)* | Khách lưu trú cần dịch vụ phòng cơ bản. | **Service Latency** (Yêu cầu nhỏ nhưng phản hồi chậm, trải nghiệm tụt). |
| **E05** | "Không biết hồ bơi, phòng gym, shuttle ra biển mấy giờ chạy, hỏi mỗi người nói một kiểu." | TripAdvisor — mục *Tiện nghi*, review 3–4 điểm. | Khách gia đình lần đầu tới resort. | **Information Gap** (Thông tin tiện ích không thống nhất, khó ra quyết định trong ngày). |
| **E06** | "App đặt phòng nặng, đăng nhập hoài báo lỗi, vào web mới được. Ở trong phòng muốn đặt thêm dịch vụ cũng ngại mở app." | Google Play — app `Vinpearl`, lọc 1–2 sao, search `đăng nhập` / `lỗi`.<br>[E06.jpg](evidence/E06.jpg)<br>![E06](evidence/E06.jpg) | Khách muốn tự phục vụ qua điện thoại. | **App Onboarding Failure** (Củng cố lý do dùng Web App/QR không cần tài khoản). |
| **E07** | "Muốn đổi giờ check-out trễ mà phải xuống quầy xếp hàng, nhân viên còn không chắc chính sách thế nào." | Booking review — search `check-out` / `đổi giờ`. | Khách bận, cần đổi/hủy linh hoạt. | **Policy Opacity & Friction** (Chính sách đổi/hủy không rõ, quy trình thủ công). |
| **E08** | "Đặt bàn nhà hàng buffet tối mà gọi số nội bộ không ai nghe, lên tới nơi thì hết bàn." | Agoda review — search `nhà hàng` / `đặt bàn`. | Khách muốn đặt dịch vụ ăn uống nội khu. | **Booking Coordination Failure** (Không đặt trước được, mất slot, hụt trải nghiệm). |

### 3.2. Unfitted Evidences (Bằng chứng không phù hợp / Placeholder)

Các bằng chứng thu thập được nhưng không thuộc phạm vi xử lý trực tiếp của Trợ lý lưu trú & Dịch vụ theo yêu cầu (đặt làm placeholder/backlog hoặc bỏ qua):

| Evidence ID | Quote / review / observation | Nguồn / Cách tìm | User là ai? | Lý do không khớp (Unfitted) |
|---|---|---|---|---|
| **E09** | "Đặt phòng online bị trừ tiền hai lần, hoàn tiền cả tháng chưa thấy." | Google Play — app Vinpearl, search `hoàn tiền`. | Khách giao dịch thanh toán trước. | **Lỗi giao dịch/thanh toán**: Nằm ngoài phạm vi hỏi đáp & đặt dịch vụ tại chỗ trong lúc lưu trú. |
| **E10** | "Bãi biển bị rác, nước hồ không sạch lắm." | TripAdvisor — review cơ sở vật chất. | Khách đánh giá chất lượng vật lý. | **Vấn đề vận hành/cơ sở vật chất**: Không phải bài toán phần mềm AI concierge có thể xử lý. |

Nếu chưa có nguồn ngoài nhóm, ghi rõ:

```text
Đây là giả định dựa trên khảo sát sơ bộ và review công khai trên Google Play/Booking/Agoda/TripAdvisor. Nhóm sẽ kiểm chứng thực tế bằng cách phỏng vấn nhanh 5-7 khách từng lưu trú tại resort phức hợp về hành vi hỏi đáp tiện ích và đặt dịch vụ nội khu trước checkpoint M1 Day 06, đồng thời đính kèm link review gốc cho từng mã E.
```

## 4. Competitor / analog evidence

| App / mô hình tham khảo | Họ xử lý task này thế nào? | Pattern học được | Có áp dụng trong 1 ngày không? |
|---|---|---|---|
| **Marriott Bonvoy / Hilton Honors (Mobile Key & Digital Concierge)** | Cho khách chat yêu cầu dịch vụ (xin khăn, đặt nhà hàng) ngay trong app, định tuyến tới bộ phận phù hợp và báo trạng thái xử lý. | **Service-request routing & status tracking:** gom yêu cầu về một luồng chat, có vòng đời trạng thái. | Cắt giảm scope: app của chuỗi lớn rất nặng. Nhóm học pattern "chat → định tuyến yêu cầu" nhưng triển khai dạng Web App/Zalo Mini App qua QR, không cần tài khoản. |
| **Zalo Mini App / WeChat Mini Program — QR gọi món tại bàn (Analog)** | Quét QR tại bàn để tự nhận diện vị trí, hiển thị menu, gọi món/thanh toán mà không cần tải app hay đăng nhập. | **Physical Touchpoint Integration & Zero-Install:** QR mang sẵn ngữ cảnh (số bàn ↔ số phòng). | Có. Đặt QR trong phòng/trên thẻ phòng để tự truyền số phòng + thời điểm vào chatbot, kích hoạt câu chào concierge thông minh thay vì điền form/đăng nhập. |

## 5. Evidence -> Insight

```text
Evidence nổi bật nhất:
Trong lúc lưu trú, khách liên tục có những nhu cầu nhỏ nhưng gấp (hỏi giờ tiện ích, xin amenity, đặt bàn/spa, đổi giờ check-out) nhưng kênh duy nhất là gọi lễ tân — vốn hay bận máy, chờ lâu, thông tin mỗi nơi nói một kiểu. App đặt phòng thì nặng và lỗi đăng nhập nên khách ngại mở.

Insight:
Khách lưu trú không chỉ cần "biết thông tin resort" (surface need).
Họ cần một concierge phản hồi tức thời, không ma sát (Zero-Install/Zero-Login) để được trả lời đúng và đặt được dịch vụ ngay tại phòng,
vì các review cho thấy điểm gãy nằm ở độ trễ phản hồi và sự rời rạc của quy trình đặt dịch vụ, chứ không phải thiếu dịch vụ.

Opportunity:
AI có thể giúp bằng cách dùng QR trong phòng để tự nắm số phòng + thời điểm (Zero-Input), dùng Gemini API tạo hội thoại concierge: tự trả lời FAQ tiện ích từ nguồn dữ liệu thống nhất và draft/định tuyến các yêu cầu dịch vụ đơn giản tới đúng bộ phận, đồng thời chuyển người thật khi gặp đổi/hủy booking, khiếu nại hoặc yêu cầu vượt chính sách.
```

## 6. Evidence đổi SPEC như thế nào?

- [x] Đổi user chính.
- [x] Đổi pain statement.
- [x] Đổi build slice.
- [x] Đổi Auto/Aug decision.
- [x] Đổi 4 paths.
- [x] Đổi failure mode.
- [ ] Đổi owner/test plan.

Ghi rõ 1-2 thay đổi quan trọng:

```text
Trước evidence, nhóm định làm một app tra cứu tiện ích resort đầy đủ (danh bạ dịch vụ, bản đồ, menu) yêu cầu khách tải app và đăng nhập tài khoản thành viên để xem thông tin và gọi điện đặt dịch vụ.

Sau evidence, nhóm đổi thành một Web App/Zalo Mini App siêu nhẹ (Zero-Install) kích hoạt bằng QR trong phòng. AI concierge (Gemini API) tự nhận số phòng + thời điểm, trả lời FAQ tiện ích từ một nguồn dữ liệu thống nhất và tiếp nhận yêu cầu dịch vụ đơn giản bằng nút bấm; với đổi/hủy booking hay khiếu nại thì chuyển lễ tân (conditional automation).

Lý do: Điểm gãy lớn nhất theo review không phải thiếu dịch vụ mà là độ trễ phản hồi và quy trình rời rạc khi phải gọi/đi tới từng quầy. Hội thoại concierge qua QR giảm tối đa ma sát, trả lời tức thời và giảm tải cho lễ tân.
```
