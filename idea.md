# PocketOps — Tác nghiệp buồng phòng khi kết nối gián đoạn

**Đề xuất MVP cho nhóm 6 người trong 6 tuần.** Trọng tâm là lưu công việc tại hiện trường và đồng bộ đúng khi có kết nối, với một luồng từ nhận việc đến nghiệm thu. Khả năng hoàn thành phụ thuộc kỹ năng, thiết bị và phạm vi thực tế của nhóm; lợi ích kinh doanh cần được kiểm chứng qua khảo sát và pilot.

## 1. Bài toán và người dùng mục tiêu

PocketOps hỗ trợ nhân viên buồng phòng ghi nhận checklist, hoàn tất nhiệm vụ và báo hỏng kèm ảnh tại khách sạn/resort có kết nối không ổn định. Giám sát theo dõi kết quả, xử lý ngoại lệ và nghiệm thu trên dashboard; lễ tân xem thông tin đã được máy chủ chấp nhận.

Phân khúc khảo sát ban đầu là khách sạn/resort 3–5 sao tại Việt Nam có quy trình bàn giao giữa nhiều bộ phận. Cần xác định cơ sở nào thực sự gặp vấn đề, đang dùng PMS nào và có thể tiếp cận để thử nghiệm. Mở rộng sang Đông Nam Á được xem xét sau khi có bằng chứng tại phân khúc ban đầu.

| Vai trò | Công việc cần hỗ trợ |
| --- | --- |
| Nhân viên buồng phòng | Nhận việc, làm checklist, ghi nhận hoàn tất và báo hỏng ngay tại phòng, kể cả khi tạm mất mạng. |
| Giám sát | Xem tiến độ, nghiệm thu và xử lý các cập nhật bị xung đột. |
| Kỹ thuật | Nhận phiếu có mã phòng/thiết bị, mô tả và ảnh khi ảnh đã được tải lên. |
| Lễ tân | Xem kết quả nghiệm thu, tình trạng chặn phòng và thời điểm cập nhật. |
| Người mua/quản lý | Đánh giá công đối soát, độ trễ bàn giao và chi phí triển khai so với cách làm hiện tại. |

### Các vấn đề cần xác thực tại hiện trường

- **Ghi nhận bị gián đoạn:** nhân viên không hoàn tất được thao tác hoặc phải nhập lại khi mất kết nối. Cần quan sát lỗi trên thiết bị và ứng dụng thực tế, thay vì mặc định mọi giải pháp hiện hành đều mất dữ liệu.
- **Thông tin bàn giao đến chậm:** nguyên nhân có thể nằm ở dọn phòng, chờ giám sát, chờ mạng, truyền dữ liệu hoặc cập nhật PMS. Cần đo từng đoạn để biết PocketOps tác động vào đâu.
- **Báo hỏng thiếu ngữ cảnh:** thiếu vị trí, thông tin thiết bị hoặc ảnh có thể gây trao đổi và di chuyển bổ sung. Chưa có cơ sở khẳng định giảm một tỷ lệ cố định thời gian sửa chữa.
- **Đối soát qua nhiều kênh:** giám sát có thể phải tổng hợp giấy, bộ đàm và tin nhắn. Cần đo thời gian và tần suất sai lệch trước khi đặt mục tiêu cải thiện.

**Giới hạn của offline-first:** lưu thành công trên điện thoại giúp nhân viên tiếp tục công việc, nhưng lễ tân chỉ nhận được cập nhật sau khi có đường truyền và hệ thống chấp nhận dữ liệu. Ứng dụng không loại bỏ thời gian chờ kết nối hoặc chờ nghiệm thu.

## 2. Giải pháp hiện có và giả thuyết khác biệt

Offline đã xuất hiện trong các sản phẩm vận hành khách sạn. So sánh cần theo từng sản phẩm và phạm vi chức năng được công bố, không suy rộng từ một ứng dụng sang toàn bộ nhóm PMS.

| Giải pháp | Thông tin từ nguồn chính thức | Ý nghĩa với PocketOps |
| --- | --- | --- |
| Flexkeeping | Có mô tả cập nhật trạng thái offline và đồng bộ sau khi kết nối lại; có lưu ý riêng về tệp đính kèm. [Nguồn](https://help.mews.com/s/article/using-flexkeeping-on-ios-and-android-devices-while-offline). | Cần so sánh độ bền dữ liệu và luồng gửi ảnh cụ thể; chỉ có offline chưa đủ tạo khác biệt. |
| protel Housekeeping | Có chế độ offline ở vùng không có WLAN và đồng bộ khi trở lại vùng phủ sóng. [Nguồn](https://help.protel.net/housekeeping/en_US/web/Einleitung.htm). | Kịch bản mất sóng trong khách sạn đã được đối thủ đề cập. |
| hotelkit | FAQ cho biết hệ thống chỉ truy cập được khi online. [Nguồn](https://hotelkit.net/faq/). | Có thể khảo sát nhu cầu tại cơ sở đang dùng giải pháp phụ thuộc mạng. |
| Giấy, bộ đàm, tin nhắn | Cách sử dụng và đối soát cần được khảo sát tại từng cơ sở. | PocketOps phải chứng minh thuận tiện hơn trong công việc thực tế. |

Đây là mô tả của nhà cung cấp được đối chiếu ngày 02/11/2026, chưa phải kết quả kiểm thử độc lập của nhóm.

**Giả thuyết khác biệt cần kiểm chứng:** một luồng đơn giản, giữ được checklist và ảnh qua gián đoạn kết nối/đóng mở ứng dụng, hiển thị rõ tình trạng đồng bộ và không để cập nhật cũ ghi đè trạng thái vận hành quan trọng. Giá trị thương mại còn phụ thuộc trải nghiệm, tích hợp, chi phí và khả năng triển khai tại khách sạn.

QR là tiện ích nhận diện phòng/thiết bị. Người dùng vẫn có thể chọn hoặc nhập mã thủ công; chưa coi QR là lợi thế độc quyền.

### Cách xác định quy mô thị trường

Chưa dùng con số doanh thu hoặc số lượng cơ sở khi thiếu nguồn, năm và phạm vi thống nhất. Không lấy toàn bộ thị trường PMS/phần mềm hospitality làm thị trường trực tiếp của PocketOps.

| Phạm vi | Cách xác định |
| --- | --- |
| TAM | Doanh thu tiềm năng từ nhóm cơ sở phù hợp, theo địa lý xác định và giả định giá có ghi rõ. |
| SAM | Phần cơ sở có nhu cầu, thiết bị, PMS và điều kiện triển khai mà nhóm có thể phục vụ. |
| SOM | Phần có thể tiếp cận và chuyển đổi với nguồn lực bán hàng, hỗ trợ và triển khai thực tế. |

Ước lượng ban đầu đi từ số cơ sở đủ điều kiện và mức phí dự kiến mỗi cơ sở/năm. Đây là mô hình giả định cho đến khi có dữ liệu khảo sát và thử nghiệm trả phí.

## 3. Phạm vi MVP: một luồng tác nghiệp xuyên suốt

**Luồng chính:** nhận nhiệm vụ dọn phòng → checklist offline → báo hỏng kèm một ảnh nếu cần → đồng bộ → giám sát nghiệm thu → lễ tân thấy kết quả đã được xác nhận.

| Thành phần | Phạm vi tối thiểu |
| --- | --- |
| Chuẩn bị đầu ca | Đăng nhập và tải danh sách phòng, nhiệm vụ, checklist, thông tin nhận diện khi có mạng. |
| Mobile | Xem nhiệm vụ đã tải, cập nhật checklist và ghi nhận hoàn tất khi offline. Chỉ báo đã lưu sau khi ghi nhận bền vững thành công. |
| Báo hỏng | Gắn phòng/thiết bị, mô tả và tối đa một ảnh cho mỗi phiếu trong MVP. Cho nhập thông tin thủ công nếu thiếu danh mục hoặc QR. |
| Đồng bộ | Hàng đợi bền vững, gửi lại có kiểm soát, chống hiệu ứng trùng và nhận thay đổi được máy chủ chấp nhận về client. |
| Dashboard giám sát | Xem tiến độ, phiếu báo hỏng, nghiệm thu và xử lý thủ công cập nhật xung đột. Dùng online trong MVP. |
| Màn hình lễ tân | Xem kết quả nghiệm thu, lệnh chặn bảo trì và thời điểm cập nhật; phân biệt thông tin PocketOps với PMS. |
| PMS gateway | Mô phỏng giao tiếp PMS khi chưa xác nhận quyền truy cập môi trường thật; ghi rõ trạng thái mô phỏng. |

**Để sau MVP:** đặt phòng, thanh toán, định giá, kho phụ tùng, lịch bảo trì định kỳ, tối ưu phân công, phân tích nâng cao và bộ kết nối nhiều PMS. Một phiên bản bảo trì độc lập có thể được khảo sát, nhưng chưa phải hướng chuyển đổi sản phẩm đã được lựa chọn.

### Hiển thị tình trạng dữ liệu

| Nhãn cho người dùng | Ý nghĩa kỹ thuật |
| --- | --- |
| Đã lưu trên thiết bị / Chờ đồng bộ | LOCAL_SAVED: đã ghi bền vững trên máy, chưa được máy chủ chấp nhận. |
| Máy chủ đã xác nhận | SERVER_ACCEPTED: máy chủ đã kiểm tra và chấp nhận; chưa mặc nhiên đồng nghĩa PMS đã cập nhật. |
| PMS mô phỏng đã xác nhận | PMS_MOCK_CONFIRMED: gateway giả lập đã xử lý theo kịch bản demo. |
| PMS đã xác nhận | PMS_CONFIRMED: chỉ dùng khi adapter thật nhận được xác nhận cập nhật từ PMS. |
| Cần xử lý / Gửi chưa thành công | Thao tác xung đột, bị từ chối hoặc gặp lỗi; hiển thị lý do và hướng xử lý phù hợp. |

Không trình bày việc một thiết bị đã đánh dấu hoàn tất như thể lễ tân hoặc PMS đã nhận thông tin đó.

## 4. Quy tắc dữ liệu và đồng bộ

### Lưu cục bộ và gửi lại

- Ghi thay đổi và bản ghi outbox trong giao dịch cơ sở dữ liệu cục bộ trước khi báo đã lưu. Ảnh được lưu vào vùng tệp do ứng dụng quản lý; outbox giữ tham chiếu đến tệp hợp lệ.
- Mỗi thao tác có operationId ổn định qua các lần gửi lại. Máy chủ dùng ID này để tránh tạo hiệu ứng trùng khi đã xử lý nhưng phản hồi xác nhận bị mất.
- Tách gửi thông tin phiếu/trạng thái khỏi tải ảnh. Ảnh chưa gửi xong không chặn các cập nhật độc lập; dashboard báo rõ ảnh còn chờ.
- Giữ thứ tự các thao tác phụ thuộc nhau trên cùng nhiệm vụ. Tránh một FIFO toàn cục khiến một ảnh hoặc bản ghi lỗi chặn mọi công việc khác.
- Thử gửi khi ứng dụng hoạt động và có thể liên lạc với máy chủ. Lỗi tạm thời được thử lại với backoff; lỗi quyền, dữ liệu hoặc xung đột được xử lý riêng.
- Kéo thay đổi từ máy chủ về bằng cơ chế đơn giản theo phiên bản/con trỏ. Hiển thị thời điểm đồng bộ gần nhất và các thao tác chưa được xác nhận.

Tác vụ nền thực hiện theo cơ chế của từng hệ điều hành. Không cam kết đồng bộ trong cửa sổ mạng 1–2 giây, kể cả khi ứng dụng đang mở; thời gian còn phụ thuộc đường truyền, xác thực, máy chủ và lịch chạy của OS. [Apple Background Tasks](https://developer.apple.com/documentation/backgroundtasks/choosing-background-strategies-for-your-app), [Android WorkManager](https://developer.android.com/develop/background-work/background-tasks/persistent/getting-started/define-work).

Đăng nhập lần đầu và nạp dữ liệu đầu ca cần kết nối. Trước pilot phải xác định chính sách dùng thiết bị chung, đăng xuất và giữ thao tác chưa gửi; không tự xóa công việc đang chờ mà không có cách đối soát. Phạm vi bảo vệ dữ liệu được đánh giá bằng các tình huống kiểm thử cụ thể, không có cam kết không mất dữ liệu trong mọi sự cố thiết bị hoặc ứng dụng.

### Phân biệt hoàn tất dọn phòng và đủ điều kiện giao phòng

MVP dùng mô hình gọn, không xây dựng engine workflow tổng quát:

| Dữ liệu | Trách nhiệm |
| --- | --- |
| Cleaning task | Nhiệm vụ của một lượt dọn cụ thể, trạng thái hoàn tất và kết quả nghiệm thu. |
| Maintenance hold | Lệnh chặn phòng do vấn đề kỹ thuật, độc lập với việc đã dọn sạch. |
| Occupancy snapshot | Thông tin có khách/trống phòng từ PMS mô phỏng hoặc adapter thật; mobile buồng phòng không tự thay đổi. |

OPERA phân biệt Clean với Inspected và có Out of Order/Out of Service. Vì vậy, đánh dấu đã dọn không được tự suy ra phòng đã đủ điều kiện giao khách. [Oracle Room Status](https://docs.oracle.com/en/industries/hospitality/opera-cloud/24.4/ocsuh/t_room_status_mobile_app.htm).

Máy chủ kiểm tra operationId, taskId/cleaningCycleId, phiên bản dữ liệu, quyền người gửi và điều kiện chuyển trạng thái. Không dùng Last-Write-Wins theo thời gian trên client cho quyết định liên quan giao phòng. Hoàn tất cleaning task không được tự gỡ maintenance hold hoặc đổi occupancy.

Ví dụ: máy A lưu hoàn tất dọn phòng 402 khi offline; máy B ghi nhận sự cố cần chặn phòng. Khi A gửi lại, hệ thống có thể ghi nhận công việc dọn theo quy tắc hợp lệ nhưng không được tự xóa lệnh chặn. Nếu có xung đột, bản cập nhật được giữ để giám sát xử lý trên dashboard; mobile chỉ cần báo trạng thái và thông tin tối thiểu.

Quy tắc hiển thị khả năng bàn giao trong demo dựa trên kết quả nghiệm thu, occupancy và maintenance hold đã được xác nhận. Khi triển khai thật, quy tắc phải phù hợp chính sách khách sạn/PMS; dashboard PocketOps không tự thay thế quyết định của PMS khi chưa có tích hợp được kiểm chứng.

### Ảnh sự cố

Nén và điều chỉnh kích thước ảnh trên thiết bị, đồng thời giữ đủ chi tiết nhận diện lỗi. Ngưỡng dung lượng được chọn sau khi thử ảnh và mạng mục tiêu, không cố định mọi ảnh phải dưới 300 KB. Giữ tệp để thử lại khi upload gián đoạn và có trạng thái xác nhận riêng cho ảnh.

## 5. Định hướng công nghệ: KMP cho Android/iOS (trước đây gọi là KMM)

**PocketOps sử dụng Kotlin Multiplatform để chia sẻ logic giữa Android và iOS, kết hợp Jetpack Compose trên Android và SwiftUI trên iOS.** Đây là mô hình shared business logic + native UI. Kotlin Multiplatform Mobile (KMM) là tên sản phẩm trước đây; JetBrains đã thống nhất tên gọi Kotlin Multiplatform (KMP), kể cả khi chỉ nhắm Android và iOS. [Thông báo tên gọi của JetBrains](https://blog.jetbrains.com/kotlin/2023/07/update-on-the-name-of-kotlin-multiplatform/).

Trong phương án này, phần dùng chung tập trung vào nghiệp vụ và dữ liệu. Giao diện, điều hướng và tích hợp hệ điều hành được triển khai riêng trên từng nền tảng. Compose Multiplatform là lựa chọn chia sẻ UI khác của hệ sinh thái KMP; MVP hiện chọn Compose Android và SwiftUI. [Tổng quan KMP](https://kotlinlang.org/docs/multiplatform/kmp-overview.html).

### Phân chia module và trách nhiệm

| Module / source set dự kiến | Nội dung |
| --- | --- |
| shared/commonMain | Domain model, quy tắc kiểm tra dữ liệu phía client, repository, schema/truy vấn SQLDelight, outbox, thuật toán đồng bộ/gửi lại, Ktor Client và kotlinx.serialization; Coroutines/Flow/StateFlow cho xử lý bất đồng bộ và luồng dữ liệu. |
| shared/androidMain | Khởi tạo AndroidSqliteDriver, Ktor engine OkHttp và các adapter cần API Android. |
| shared/iosMain | Khởi tạo NativeSqliteDriver, Ktor engine Darwin và các adapter cần API iOS có thể gọi từ Kotlin/Native. |
| androidApp | Jetpack Compose, ViewModel Android, điều hướng, camera/QR và tích hợp WorkManager để kích hoạt đồng bộ. |
| iosApp | SwiftUI, ObservableObject hoặc cơ chế quan sát trạng thái phù hợp, điều hướng, AVFoundation cho camera/QR và tích hợp tác vụ nền của iOS. |
| Backend / dashboard / PMS gateway | Thành phần triển khai riêng: xác thực, kiểm tra lệnh phía máy chủ, lưu dữ liệu tập trung, xử lý xung đột, giao diện quản lý và kết nối PMS. |

SwiftUI nằm trong ứng dụng Swift/Xcode, không nằm trong source set Kotlin iosMain. UI đọc dữ liệu qua repository của shared module; cơ sở dữ liệu cục bộ phục vụ trạng thái trên từng thiết bị. Máy chủ vẫn kiểm tra quyền, phiên bản và quy tắc nghiệp vụ khi chấp nhận lệnh, kể cả khi client đã kiểm tra trước.

### Lưu trữ và kết nối mạng

**SQLDelight** sinh API Kotlin có kiểm tra kiểu từ schema và truy vấn SQL. Schema, truy vấn và logic repository có thể dùng chung; SQLite driver và nơi lưu tệp được cấu hình theo nền tảng. Mỗi thiết bị có cơ sở dữ liệu riêng, không phải một SQLite dùng chung trực tiếp giữa Android và iOS. [SQLDelight Multiplatform](https://sqldelight.github.io/sqldelight/latest/multiplatform_sqlite/).

**Ktor Client** chia sẻ cấu hình HTTP, DTO, serialization và luồng gọi API trong commonMain; engine cụ thể được khởi tạo theo nền tảng, dự kiến OkHttp trên Android và Darwin trên iOS. Theo dõi kết nối là tín hiệu để thử gửi; chỉ phản hồi hợp lệ từ máy chủ mới xác nhận thao tác đã được chấp nhận. [Ktor client engines](https://ktor.io/docs/client-engines.html).

Ảnh được lưu qua adapter tệp của nền tảng và được tham chiếu từ outbox. Chụp ảnh, nhận diện QR, nén ảnh và quyền truy cập thiết bị được tích hợp bằng API/thư viện phù hợp từng nền tảng; không mặc định các phần này đều nằm trong commonMain. Trên Android, CameraX cung cấp luồng camera và cần kết hợp thành phần nhận diện mã nếu triển khai quét QR.

### Đồng bộ dùng chung, lịch chạy theo nền tảng

Shared module chứa cách đọc outbox, tạo request, xử lý xác nhận, phân loại lỗi, backoff và nhận thay đổi từ server. Android/iOS chịu trách nhiệm khởi động hoặc tiếp tục một lượt đồng bộ trong điều kiện mà hệ điều hành cho phép.

- **Android:** đồng bộ khi ứng dụng hoạt động và dùng WorkManager cho công việc nền bền vững phù hợp.
- **iOS:** đồng bộ khi ứng dụng hoạt động; lên lịch tác vụ nền bằng API iOS phù hợp. Thời điểm và thời lượng được chạy phụ thuộc hệ điều hành.
- **Cả hai:** phối hợp các nguồn kích hoạt để tránh nhiều lượt đồng bộ cùng xử lý một outbox; vẫn cần operationId và kiểm tra lệnh phía server.

KMP chia sẻ thuật toán, không cung cấp một bộ lập lịch nền chung thay thế WorkManager hoặc cơ chế iOS. Không suy ra khả năng chạy nền tức thì chỉ từ việc dùng KMP/Ktor; các giới hạn tại mục 4 vẫn áp dụng.

### Tích hợp shared module với Swift

Phần Kotlin cho iOS được biên dịch bằng Kotlin/Native và có thể đóng gói thành framework/XCFramework để ứng dụng Swift sử dụng. Hướng tích hợp dự kiến là xuất framework qua Objective-C interop; có thể dùng SKIE nếu phù hợp bộ phiên bản Kotlin và thư viện của dự án.

SKIE hỗ trợ trình bày Flow/StateFlow thành AsyncSequence để Swift tiêu thụ thuận tiện hơn. Lớp Swift vẫn quản lý vòng đời quan sát, cập nhật UI trên MainActor và xử lý hủy tác vụ; SKIE không thay thế SwiftUI hoặc cơ chế chạy nền của iOS. [Tài liệu SKIE về Flow](https://skie.touchlab.co/features/flows).

### Điều kiện triển khai và kiểm chứng

Giá trị mong đợi là giảm viết lặp nghiệp vụ, dùng chung hợp đồng dữ liệu và kiểm thử được logic đồng bộ trên nhiều nền tảng. Tỷ lệ chia sẻ code, hiệu năng, bộ nhớ và thời lượng pin là kết quả cần đo, chưa gắn với một tỷ lệ hoặc mức bảo đảm cố định.

Dùng commonTest cho logic độc lập nền tảng; kiểm thử riêng driver, lưu tệp, camera, vòng đời và tác vụ nền trên Android/iOS. Nhóm cần sớm chốt bộ phiên bản Kotlin, Gradle/Android plugin, SQLDelight, Ktor và SKIE tương thích, đồng thời có môi trường macOS/Xcode phù hợp để build và kiểm thử iOS.

### Nhân sự dự kiến

Giữ cơ cấu ban đầu: **1 dev shared core, 2 dev Android, 2 dev iOS, 1 dev backend**. Dev shared core giữ đầu mối kiến trúc; ít nhất một thành viên phù hợp cùng phát triển/review core và outbox để tránh phụ thuộc vào một người. Chốt hợp đồng dữ liệu sớm để UI và backend phát triển song song.

Dev backend giữ đầu mối API, dữ liệu và gateway. Người thực hiện giao diện dashboard phải được phân công theo kỹ năng thực tế khi chốt phạm vi; không để dashboard thành hạng mục không có chủ sở hữu hoặc mặc định chuyển dev iOS sang web/backend.

- Nếu giữ Android và iOS vì yêu cầu hoặc mục tiêu học tập, cả hai cùng làm bộ tính năng nhỏ và sớm chạy được một luồng xuyên suốt qua shared core đến máy chủ.
- Nếu hai nền tảng không cần thiết và nguồn lực hạn chế, chọn nền tảng chính theo kỹ năng/thiết bị pilot; nền tảng thứ hai có thể chứng minh chia sẻ core ở phạm vi nhỏ hơn.
- Cần tính đến máy Mac, thiết bị kiểm thử và kinh nghiệm tích hợp. Không coi native tự bảo đảm FPS hoặc thời lượng pin.

### Ưu tiên trong giới hạn sáu tuần

1. Xác nhận yêu cầu nền tảng, thiết bị và quyền PMS; chốt mô hình nhiệm vụ, hợp đồng API, người phụ trách dashboard và phạm vi nghiệm thu.
2. Sớm chứng minh luồng nhận việc → lưu local/outbox → máy chủ chấp nhận → dashboard cập nhật trên các nền tảng sẽ nghiệm thu.
3. Hoàn thiện checklist, báo hỏng/ảnh, nghiệm thu và xử lý xung đột tối giản.
4. Dành thời gian kiểm thử gián đoạn, đo trên thiết bị và hoàn thiện demo. Chỉ mở rộng QR hoặc adapter PMS thật khi không ảnh hưởng luồng chính.

Đây là thứ tự ưu tiên dự kiến, chưa phải bảo đảm tiến độ hoặc kế hoạch triển khai chi tiết.

## 6. Tích hợp PMS và ranh giới demo

**Mặc định dùng PMS mô phỏng khi chưa xác nhận quyền truy cập ngoài nhóm.** Dashboard và demo phải ghi rõ thông tin nào đến từ mô phỏng. Gateway giả lập kiểm tra được hợp đồng và luồng nội bộ, chưa chứng minh tích hợp được với nhà cung cấp PMS.

Nếu đã có môi trường thật phù hợp, quyền hợp lệ và đủ thời gian, nhóm có thể thử một adapter thật; không bắt buộc xây thêm mock riêng chỉ để đáp ứng hình thức. Điều kiện truy cập phải được xác minh với môi trường cụ thể. Cloudbeds có API và quy trình cấp quyền/tích hợp; OPERA Cloud có OHIP cùng điều kiện sử dụng và production. [Cloudbeds API](https://www.cloudbeds.com/api/), [Oracle OHIP FAQ](https://docs.oracle.com/en/industries/hospitality/integration-platform/ohipu/c_faqs.htm).

Không suy ra tổng chi phí/thời gian tích hợp chỉ từ phí gọi API. Cần xem cả công phát triển, quyền truy cập, thủ tục đối tác, cấp quyền của cơ sở và hỗ trợ triển khai.

Khi chưa thử luồng thật, chưa cam kết rút ngắn bàn giao trong PMS sản xuất. Có thể xem xét pilot tách biệt nếu khách sạn chấp nhận rõ cách đối soát; không trình bày pilot đó như đồng bộ PMS tự động.

## 7. Tiêu chí nghiệm thu kỹ thuật và demo

Các tiêu chí sau là mục tiêu cần triển khai và kiểm thử, chưa phải kết quả đã đạt.

| Tình huống | Kết quả cần chứng minh |
| --- | --- |
| Làm việc offline rồi đóng/mở ứng dụng | Checklist, phiếu và ảnh đã báo lưu vẫn còn; khôi phục được trạng thái chờ đồng bộ. |
| Máy chủ xử lý xong nhưng phản hồi xác nhận bị mất | Gửi lại cùng operationId mà không tạo phiếu hoặc hiệu ứng nghiệp vụ trùng. |
| Gửi bản hoàn tất cũ sau khi có maintenance hold | Không tự gỡ lệnh chặn; giữ xung đột để giám sát xử lý nếu cần. |
| Bản cập nhật thuộc lượt dọn trước được gửi muộn | Không tác động nhầm nhiệm vụ hoặc lượt dọn mới của cùng phòng. |
| Upload ảnh gián đoạn | Ảnh còn để retry; thông tin phiếu và cập nhật độc lập vẫn được đồng bộ. |
| Giám sát thay đổi dữ liệu trên máy chủ | Dashboard và client nhận trạng thái đã được chấp nhận, phân biệt với thao tác local còn chờ. |
| Cập nhật không đủ quyền hoặc chuyển trạng thái sai | Máy chủ từ chối có lý do; giao diện không trình bày như đã được chấp nhận. |

Demo gồm tải dữ liệu đầu ca, bật chế độ máy bay, làm checklist và chụp ảnh, đóng/mở ứng dụng, khôi phục kết nối rồi đối chiếu dashboard. Bổ sung tình huống mất phản hồi xác nhận và hai thiết bị cập nhật khác nhau để chứng minh xử lý đồng bộ.

Đo riêng thời gian ghi local, thời gian gửi đến khi máy chủ chấp nhận, thời gian dashboard/client nhận thay đổi và thời gian tải ảnh. Báo cáo foreground/background, thiết bị/OS, điều kiện mạng, kích thước hàng đợi và phân bố độ trễ. Chỉ chốt ngưỡng hiệu năng sau khi xác định điều kiện nghiệm thu; không lấy một lần demo nhanh làm bảo đảm thời gian thực hoặc an toàn trong mọi tình huống.

## 8. Kiểm chứng giá trị vận hành

Trước khi xem là sản phẩm thương mại, cần quan sát và trao đổi với buồng phòng, giám sát, kỹ thuật, lễ tân và người có quyền mua. Phỏng vấn ít cơ sở tạo tín hiệu định hướng, chưa đủ kết luận cho toàn thị trường.

| Giả thuyết | Dữ liệu cần thu thập |
| --- | --- |
| Mất mạng gây mất thao tác hoặc nhập lại | Tần suất, vị trí, ứng dụng/thiết bị, công việc bị ảnh hưởng và thời gian xử lý lại. |
| Tự gửi cập nhật giúp giảm thời gian bàn giao | Thời điểm dọn xong, nghiệm thu xong, có thể liên lạc máy chủ, máy chủ nhận và PMS/lễ tân nhận thông tin. |
| Ảnh/mã thiết bị giảm trao đổi hoặc di chuyển bổ sung | Số lần hỏi lại, lượt lấy thêm dụng cụ/phụ tùng và thời gian xử lý theo loại sự cố. |
| Dashboard giảm công đối soát | Thời gian tổng hợp, số cuộc gọi/tin nhắn và số ngoại lệ trước/sau pilot. |
| Khách sạn chấp nhận công cụ bổ sung | Quy trình được chấp nhận, yêu cầu tích hợp, người mua, ngân sách và điều kiện thử nghiệm/trả phí. |

Nếu có pilot, so sánh với baseline trong các ca có đặc điểm tương đương và ghi nhận khác biệt về nhân sự, số phòng, công suất hoặc loại công việc. Kết quả giúp quyết định tiếp tục, thu hẹp hay đổi giả thuyết; chưa đưa ra trước tỷ lệ giảm thời gian hoặc mức tăng hài lòng.

**Kết quả mong đợi của MVP:** một luồng có thể trình diễn và kiểm tra được qua mất mạng, gửi lại và xung đột; kèm số liệu kỹ thuật và bằng chứng ban đầu về mức phù hợp với quy trình khách sạn. Mức tiết kiệm chi phí và khả năng bán sản phẩm là kết quả cần nghiên cứu tiếp.