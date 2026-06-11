---
title: "Toán Mỗi Ngày"
description: "Bài luyện toán lặp lại ngắt quãng cho iPhone và iPad"
---

# Chính sách quyền riêng tư — Toán Mỗi Ngày

**Ngày hiệu lực:** 2026-05-21
**Cập nhật gần nhất:** 2026-06-10

Chính sách này mô tả cách ứng dụng iOS Toán Mỗi Ngày ("Ứng dụng") xử lý thông tin của bạn. Chính sách áp dụng từ v1.0 trở đi, bao gồm mô hình chia sẻ CloudKit một gia đình ở v3 (thay thế cách chia sẻ theo hồ sơ ở v2.0).

## Tóm tắt dễ hiểu

- Chúng tôi không vận hành bất kỳ máy chủ nào. Chúng tôi không thu thập bất kỳ thông tin cá nhân nào.
- Mọi thứ ở lại trên thiết bị của bạn trừ khi bạn bật **đồng bộ iCloud**; khi đó Apple, không phải chúng tôi, lưu nó trong tài khoản iCloud riêng tư của bạn.
- Ứng dụng chỉ dùng micrô khi bạn đang trả lời một bài toán ở chế độ giọng nói. Âm thanh được xử lý bằng nhận dạng giọng nói của Apple (trên thiết bị, cấp Siri) và bị loại bỏ ngay; chúng tôi không bao giờ lưu trữ, tải lên hay phân tích nó.
- Không có trình theo dõi của bên thứ ba, quảng cáo hay SDK phân tích nào.

## Những gì Ứng dụng lưu trên thiết bị của bạn

- **Hồ sơ.** Tên, emoji, màu và cài đặt theo hồ sơ.
- **Trạng thái lặp lại ngắt quãng.** Với mỗi thẻ (ví dụ `7 + 8`): ngày ôn kế tiếp đã lên lịch, độ khó, độ ổn định và số lần ôn.
- **Hoạt động.** Số lần ôn đã hoàn thành mỗi ngày theo hồ sơ (dùng cho chip chuỗi ngày và màn hình Thống kê).
- **Lỗi.** Một hàng đợi các bài toán bạn vừa trả lời sai, để Ứng dụng có thể đưa lại.
- **Tùy chọn.** Các công tắc toàn ứng dụng, chẳng hạn đồng bộ iCloud có bật hay không.

Tất cả những thứ này được ghi vào thư mục Tài liệu được cô lập riêng của Ứng dụng và vào `UserDefaults`. Ứng dụng không thể đọc dữ liệu của ứng dụng khác, và ứng dụng khác không thể đọc dữ liệu của Ứng dụng.

## Những gì Ứng dụng tùy chọn lưu trong iCloud

Đồng bộ iCloud **mặc định tắt**. Khi bạn bật (biểu tượng bánh răng → **Cài đặt → Đồng bộ → Dùng iCloud**), Ứng dụng ghi cùng dữ liệu mô tả ở trên vào iCloud riêng tư của bạn qua API **CloudKit** của Apple. Đây là iCloud của bạn, chỉ bạn truy cập được trên các thiết bị đăng nhập cùng một ID Apple. Chúng tôi không có quyền truy cập.

- Dữ liệu được đồng bộ chính xác: hồ sơ, trạng thái thẻ, hoạt động, lỗi và (tùy chọn) siêu dữ liệu chia sẻ gia đình (một tên hiển thị bạn chọn cho gia đình mình).
- Đồng bộ iCloud **không** bao gồm nội dung của bất kỳ bản ghi giọng nói nào hay bất kỳ phân tích nào.
- Khi bạn đăng nhập bằng một ID Apple khác, Ứng dụng phát hiện thay đổi và tắt đồng bộ cho đến khi bạn bật lại một cách rõ ràng, để dữ liệu không bị âm thầm tải lên một tài khoản khác.
- Xóa một hồ sơ từ **Quản lý hồ sơ** sẽ gỡ hồ sơ khỏi thiết bị và (khi iCloud truy cập được trên ID Apple ban đầu) khỏi bản sao iCloud của bạn nữa.

## Chia sẻ gia đình

Ở v3, việc chia sẻ diễn ra ở cấp **gia đình** thay vì theo hồ sơ. Mở biểu tượng bánh răng → **Cài đặt → Gia đình → Thiết lập gia đình**, đặt tên gia đình và mời người thân qua bảng chia sẻ iOS tiêu chuẩn (Tin nhắn, Mail hoặc AirDrop).

- Mọi hồ sơ trên thiết bị của chủ sở hữu đều thuộc gia đình. Mời một người thân sẽ chia sẻ tất cả cùng lúc.
- Dữ liệu nằm trong **iCloud của chủ sở hữu gia đình**. Người tham gia không lưu một bản sao riêng trong iCloud của họ; hoạt động học của họ được ghi trực tiếp vào CloudKit của chủ sở hữu qua mô hình phân quyền CKShare giới hạn theo vùng của Apple.
- Tham gia một gia đình là **không thể hoàn tác trên thiết bị tham gia**: các hồ sơ cục bộ hiện có của người tham gia bị thay bằng hồ sơ của gia đình. Trước khi tham gia, Ứng dụng cung cấp tùy chọn **Xuất hồ sơ ra tệp** để bạn lưu một bản sao JSON dữ liệu hiện tại và nhập lại sau nếu đổi ý.
- Nếu chủ sở hữu giải tán gia đình (Cài đặt → Gia đình → Giải tán) hoặc đăng xuất iCloud, người tham gia mất quyền truy cập trực tiếp ở lần đồng bộ kế tiếp. Bộ nhớ đệm cục bộ của các hồ sơ gia đình trở thành của riêng họ (không có việc xóa không thể hoàn tác khi rời đi).
- Người tham gia có thể rời gia đình bất cứ lúc nào (Cài đặt → Gia đình → Rời). Khi rời, họ giữ các hồ sơ gia đình trên thiết bị của mình như của riêng họ.
- Giới hạn `CKShare` của Apple là 100 người tham gia cho mỗi mục chia sẻ. Quy mô gia đình tự nhiên là khoảng 6.

## Xuất / Nhập (sao lưu JSON)

Trong **Cài đặt → Sao lưu** bạn có thể:

- **Xuất hồ sơ ra tệp**: lưu một tệp JSON chứa mọi hồ sơ trên thiết bị hiện tại (bất kể trạng thái gia đình). Hữu ích như một bản sao lưu thủ công hoặc trước các thao tác không thể hoàn tác.
- **Nhập hồ sơ từ tệp**: khôi phục một bản xuất trước đó. Chế độ **Hợp nhất** thêm các hồ sơ còn thiếu và cập nhật các hồ sơ hiện có nếu bản sao nhập vào mới hơn. Chế độ **Thay thế** xóa các hồ sơ cục bộ và cài bộ đã nhập; chỉ khả dụng khi bạn không ở trong một gia đình.

## Micrô và nhận dạng giọng nói

Khi chế độ giọng nói bật, trong lúc bạn trả lời một bài toán, Ứng dụng:

1. Thu âm thanh micrô trực tiếp bằng `AVAudioEngine`.
2. Truyền nó tới `SFSpeechRecognizer` (khung của Apple). Trên các thiết bị iOS hiện đại, việc nhận dạng chạy trên thiết bị theo mặc định; một số cấu hình có thể dùng máy chủ nhận dạng giọng nói của Apple.
3. Đọc các chữ số đã chuyển lời và chấm câu trả lời.
4. Dừng thu ngay khi có câu trả lời cuối cùng.

Chúng tôi không lưu giữ âm thanh, bản chuyển lời hay bất kỳ tín hiệu phái sinh nào. Chúng tôi không truyền âm thanh cho bất kỳ bên nào ngoài `SFSpeechRecognizer` của Apple. Ứng dụng yêu cầu `NSMicrophoneUsageDescription` và `NSSpeechRecognitionUsageDescription` ở lần dùng đầu tiên; nếu một trong hai quyền bị từ chối, chế độ giọng nói tự động tắt và dùng bàn phím số trên màn hình.

## Nhật ký chẩn đoán

Ứng dụng phát ra các sự kiện chẩn đoán phi cấu trúc qua khung `OSLog` tiêu chuẩn của Apple (ví dụ "phiên học kết thúc, đúng=12 sai=3"). Các nhật ký này:

- Ở lại trên thiết bị.
- Chỉ bạn thấy được, trong Console.app khi thiết bị kết nối với máy Mac.
- Dùng phân loại quyền riêng tư `.private` của Apple cho bất kỳ giá trị nào có thể nhận dạng (id hồ sơ, tên hồ sơ), nên các giá trị đó được che trong bản phát hành.

Chúng tôi không thu thập, truy xuất hay truyền nội dung `OSLog`.

## Dữ liệu chúng tôi KHÔNG thu thập

- Tên, email hay thông tin liên hệ của bạn.
- Vị trí của bạn.
- Bất kỳ mã định danh thiết bị nào (IDFA, IDFV, id quảng cáo).
- Báo cáo sự cố ngoài những gì Apple có thể thu thập qua cài đặt iOS của bạn.
- Bất kỳ phân tích hay đo từ xa hành vi nào.
- Thông tin thanh toán hay hóa đơn (giao dịch mua hoàn toàn do Apple xử lý).

## Quyền riêng tư của trẻ em

Toán Mỗi Ngày được thiết kế để an toàn cho trẻ em. Vì Ứng dụng không thu thập thông tin cá nhân và không liên hệ bên thứ ba, nó đáp ứng định nghĩa "không có thông tin cá nhân" của COPPA. Chúng tôi không hiển thị quảng cáo, và không có tài khoản hay tính năng mạng xã hội. Toán Mỗi Ngày có một giao dịch mua trong ứng dụng một lần duy nhất (mở khóa ứng dụng đầy đủ); vì ứng dụng dành cho trẻ em, một cổng xác minh người lớn được hiển thị trước mọi giao dịch mua, theo yêu cầu của quy tắc danh mục Trẻ em của Apple. Mọi khoản thanh toán và mọi lần đổi mã đều do Apple xử lý qua App Store. Ứng dụng không bao giờ thấy hay lưu thông tin thanh toán của bạn.

## Lựa chọn của bạn

- **Tắt chế độ giọng nói** bất cứ lúc nào theo hồ sơ (Cài đặt → Chế độ giọng nói), hoặc toàn cục bằng cách từ chối quyền micrô trong cài đặt iOS.
- **Tắt đồng bộ iCloud** bất cứ lúc nào (biểu tượng bánh răng → Cài đặt → Đồng bộ → Dùng iCloud → tắt). Tắt không xóa các bản sao iCloud; xóa từng hồ sơ riêng lẻ nếu bạn muốn gỡ chúng.
- **Giải tán hoặc rời một gia đình** (Cài đặt → Gia đình → Giải tán / Rời) để ngừng chia sẻ. Giải tán sẽ thu hồi quyền truy cập của người tham gia vào gia đình bạn; rời đi giữ các hồ sơ gia đình trên thiết bị bạn như của riêng bạn.
- **Xuất hồ sơ ra một tệp** (Cài đặt → Sao lưu → Xuất) và giữ nó cục bộ — một bản sao lưu thủ công không bao giờ chạm đến iCloud.
- **Đặt lại tiến trình của một hồ sơ** mà không xóa hồ sơ (cài đặt hồ sơ → Đặt lại).
- **Xóa một hồ sơ** (Quản lý hồ sơ → vuốt hoặc chạm để xóa) — cũng gỡ bản sao iCloud khi đồng bộ đang bật. Lặp lại theo từng hồ sơ để gỡ tất cả.

## Thay đổi chính sách này

Nếu chúng tôi thay đổi chính sách này, phiên bản mới sẽ có tại cùng URL với ngày **Cập nhật gần nhất** được cập nhật. Các thay đổi quan trọng cũng sẽ được ghi trong ghi chú phát hành của Ứng dụng.

## Liên hệ

Có câu hỏi về chính sách này hay dữ liệu của bạn? Email **spacedmath@gmail.com**.
