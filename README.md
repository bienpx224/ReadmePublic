# Dự án Web quản lý đặt đơn hàng : 

## Tổng quan : 
- Các tính năng trong dự án : Đăng kí, Đăng nhập, Dashboard thống kê, Quản lý đơn hàng của tôi, Tạo đơn hàng mới, Quản lý Đơn hàng của nhân viên, Cập nhật thông tin đơn hàng, Cập nhật thông tin Profile, Quản lý Danh sách user trong hệ thống. 
- Role User thì quản lý đơn hàng của họ, tạo đơn hàng mới, cập nhật đơn hàng, thông tin cá nhân. 
- Role Staff thì quản lý đơn hàng trong hệ thống, cập nhật thông tin đơn hàng, thông tin Tiền cọc của khách, thông tin cá nhân. 
- Role Admin thì bao gồm các quyền của User và Staff, bổ sung thêm quản lý danh sách User trong hệ thống, cập nhật thông user trong hệ thống. Xem thống kê báo cáo về tổng đơn hàng, tổng tiền, số lượng user,.. 
- Hiển thị thông báo lỗi nếu phía client validation bị lỗi, hoặc call API bị lỗi. 
## Tính năng Phía Web hiển thị: 
### Đăng ký : (Ưu tiên)
- Có màn đăng ký, cho phép nhập các thông tin. Có nút hoặc link ấn để quay lại màn Đăng nhập nếu User đã có tài khoản. 
- Thực hiện call tới API POST /auth/email/register 
### Đăng nhập : (Ưu tiên)
- Màn đăng nhập cho phép đăng nhập bằng Google login hoặc dùng email/pass đã đăng kí trong hệ thống. 

### Tính năng (Tab) màn Dashboard: (Ưu tiên hiện chỉ số chung chung cho User)
- Màn này sẽ hiển thị thống kê, tổng quan về 1 số chỉ số trong hệ thống, tuỳ theo role. 
- Với mỗi role vào hệ thống thì màn Dashboard sẽ hiển thị nội dung khác nhau : 
- Với Role User thì sẽ hiển thị thông tin đơn hàng của user đó : tổng số đơn hàng, Tổng đơn đã hoàn thành, tổng đơn đã gửi yêu cầu, tổng đơn đang chờ vận chuyển, tổng tiền đơn, tổng tiền cọc hiện tại, tổng tiền cọc đang trong trạng thái khoá, tổng tiền cọc thừa.
- Với Role Staff thì hiển thị thông tin tất cả đơn hàng trong hệ thống : Tổng số đơn hàng, tổng đơn đã hoàn thành, Tổng đơn hàng có trạng thái Sent Request, ..
- Với Role Admin thì hiển thị tổng quan thống kê về hệ thống : Tổng số đơn hàng đã hoàn thành, Tổng số tiền chênh lệch, Tổng số user trong hệ thống, Thống kế 
***Chi tiết đợi API, hiện tại sẽ hiển thị ưu tiên theo user và staff trước, phía Admin bổ sung sau***

### Tính năng (Tab) Đơn hàng của tôi - Hiển thị với mọi Role: (Ưu tiên)
- Màn này hiển thị danh sách đơn hàng, phân trang, lọc (dựa trên các trường thông tin đơn hàng) : Tất cả các đơn hàng của User hiện tại tạo ra : Sử dụng API Get /orders/my-orders 
- Có nút Thêm đơn hàng để thực hiện, Khi Thêm đơn hàng thì sẽ hiển thị ra Popup để nhập các thông tin đơn hàng và ấn Xác nhận Thêm đơn, call API Post /orders lưu vào hệ thống. 
- Khi click vào 1 đơn hàng trong danh sách thì sẽ hiển thị ra những thông tin chi tiết được phép xem của đơn hàng đó đối với role User, người dùng có thể cập nhật thông tin mới và thực hiện action Xác nhận cập nhật hoặc Xoá đơn hàng này. 

### Tính năng (Tab) Quản lý đơn hàng - Hiển thị với Role Staff trở lên : (Ưu tiên)
- Màn này hiển thị Danh sách đơn hàng, phân trang, lọc tìm kiếm (Các trường thông tin đơn hàng) : Tất cả đơn hàng trong HỆ THỐNG : Sử dụng API Post /orders/staff-orders-all 
- Khi click vào 1 đơn hàng trong danh sách thì sẽ hiển thị ra tất cả các thông tin chi tiết của đơn hàng đó, có thể cập nhật thông tin và thực hiện action Xác nhận cập nhật. 
- Trong hiển thị thông tin chi tiết đơn hàng, có nút ấn Xem lịch sử đơn hàng -> Hiển thị lịch sử thông tin đơn hàng cho từng lần cập nhật : Tạo, thay đổi như nào, ai thay đổi, ...  
- Staff có thể thực kiểm tra thông tin đơn hàng, ấn chuyển trạng thái đơn hàng. 

### Tính năng (Tab) Quản lý Đơn vị Ship - Hiển thị với Role Staff trở lên : (Ưu tiên)
- Màn này hiển thị Danh sách các đơn vị Ship trong hệ thống, có phân trang, lọc (Tên, Mô tả, Trạng thái)
- Có nút Thêm mới để thực hiện thêm 1 đơn vị Ship mới vào hệ thống gồm các thông tin : Tên, Link Sheet, Trạng thái hoạt động, Ghi chú
- Khi ấn vào 1 đơn vị Ship thì sẽ hiển thị ra thông tin chi tiết của Ship đó, có thể chỉnh sửa thông tin, ấn Xác nhận Cập nhật để thay đổi thông tin. 

### Tính năng (Tab) Quản lý User - Hiển thị với Role Staff trở lên : (Ưu tiên)
- Màn này hiển thị Danh sách Tất cả user có trong hệ thống, có phân trang, lọc (Role, Trạng thái, tìm kiếm theo tên, email, địa chỉ)
- Khi ấn vào 1 User thì sẽ hiển thị ra thông chi tiết của User đó. Có thể chỉnh sửa 1 số thông tin của User khác (tiền cọc, ghi chú, )
- Role thấp hơn thì không Chỉnh sửa cập nhật được các user role cao hơn.
- Trong đây sẽ có nút Nhập thêm tiền cọc cho User : Trong trường hợp User đã gửi tiền cọc qua trung gian, nhân viên xác nhận thì sẽ thực hiện thêm tiền cọc vào User đó. 

### Tính năng Thông báo : 
- Ở cạnh hình Profile góc phải trên cùng có nút chuông thông báo. 
- Hệ thống sẽ interval thực hiện call API get thông báo của user đó : Hiển thị noti, báo đỏ, toast, tiếng kêu và có thay đổi text (Thông báo mới) trên title của web. 


### Tính năng My Profile : (Ưu tiên)
- Hiển thị thông tin tài khoản, thông tin cá nhân đã đăng nhập. 
- Cho phép thực hiện chỉnh sửa 1 số thông cá nhân. 

## Backend : 
### Tính năng : 
- Triển khai xây dựng dự án chứa logic, cơ sở dữ liệu, bộ API cho các tính năng đăng kí, đăng nhập, đơn hàng, quản lý ship, quản lý người dùng, lịch sử người dùng. 
- Các tính năng, logic và API trong hệ thống sẽ cần lưu ý để trả về phù hợp với từng role (User, Staff, Admin) trong hệ thống. Đảm bảo quyền hạn từng Role mới được thực hiện những tác vụ nào, xem được những dữ liệu nào. 

### Cơ sở dữ liệu chính cho Order và User : 

**Quan hệ**: ORDER <-- n-1 --> USER (Một User có thể có nhiều Order)

#### Bảng ORDER

| Trường dữ liệu   | Kiểu dữ liệu | Hiển thị với Role | Mô tả                                                                                                                                                                                                                                                                                                                        |
|------------------|--------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id               | string       | user              | ID của đơn hàng trong hệ thống - hệ thống tự tạo ra                                                                                                                                                                                                                                                                         |
| userId           | string       | user              | ID của người tạo đơn hàng                                                                                                                                                                                                                                                                                                   |
| userName         | string       | user              | Name của người tạo đơn hàng                                                                                                                                                                                                                                                                                                 |
| userPicture      | string       | user              | Picture của người tạo đơn hàng                                                                                                                                                                                                                                                                                              |
| staffId          | string       | user              | ID của nhân viên chịu trách nhiệm chính đơn này                                                                                                                                                                                                                                                                            |
| staffName        | string       | user              | Name của nhân viên chịu trách nhiệm chính đơn này                                                                                                                                                                                                                                                                          |
| staffPicture     | string       | user              | Picture của nhân viên chịu trách nhiệm chính đơn này                                                                                                                                                                                                                                                                       |
| orderId          | string       | user              | Mã đặt hàng                                                                                                                                                                                                                                                                                                                 |
| orderDate        | Datetime     | user              | Ngày đặt hàng                                                                                                                                                                                                                                                                                                               |
| expectedDate     | Datetime     | user              | Ngày dự kiến nhận hàng                                                                                                                                                                                                                                                                                                      |
| deliveryDate     | Datetime     | user              | Ngày giao hàng dự kiến                                                                                                                                                                                                                                                                                                      |
| itemName         | string       | user              | Tên mặt hàng, mỗi đơn hàng này là 1 mặt hàng được đặt                                                                                                                                                                                                                                                                      |
| quantity         | number       | user              | Số lượng mặt hàng                                                                                                                                                                                                                                                                                                           |
| itemLink         | string       | user              | Link mặt hàng                                                                                                                                                                                                                                                                                                               |
| color            | string       | user              | Màu mặt hàng                                                                                                                                                                                                                                                                                                                |
| addressBuyer     | string       | user              | Địa chỉ người mua                                                                                                                                                                                                                                                                                                           |
| sitePrice        | number       | user              | Giá trên site                                                                                                                                                                                                                                                                                                               |
| shipPrice        | number       | staff             | Giá bên Ship                                                                                                                                                                                                                                                                                                                |
| lastPrice        | number       | staff             | Thành tiền cho User                                                                                                                                                                                                                                                                                                         |
| noteSellerRate   | number       | staff             | Ghi chú về rate giữa các bên                                                                                                                                                                                                                                                                                                |
| status           | enum         | user              | Trạng thái đơn hàng: <br>- Draft (Bản nháp)<br>- SentRequest (Khách đã gửi yêu cầu đơn hàng)<br>- Rejected (Nhân viên đã từ chối)<br>- Accepted (Đã chấp nhận đơn hàng, đang gửi đi bên Ship)<br>- ShipProcessing (Bên Ship đã nhận đơn, đang tiến hành vận chuyển)<br>- Cancelled (Đã huỷ bỏ đơn hàng)<br>- Completed (Đã hoàn thành đơn hàng) |
| shipTrackId      | string       | staff             | TrackID đơn hàng này của bên ship                                                                                                                                                                                                                                                                                          |
| shipMailOrder    | string       | staff             | Mail order bên ship                                                                                                                                                                                                                                                                                                         |
| shipOrderId      | string       | staff             | OrderID đơn hàng này của bên ship                                                                                                                                                                                                                                                                                           |
| shipNote         | string       | staff             | Bên ship note lại ghi chú về đơn hàng (Ví dụ: lí do huỷ đơn - Hết hàng)                                                                                                                                                                                                                                                    |
| staffNote        | string       | staff             | Nhân viên note lại ghi chú của đơn hàng (VD: Khách quan trọng, hàng về cần gọi điện báo trực tiếp)                                                                                                                                                                                                                         |
| depositAmount    | number       | staff             | Số tiền đã đặt cọc cho đơn hàng này                                                                                                                                                                                                                                                                                        |
| userNote         | string       | user              | Khách note lại lưu ý ghi chú về đơn hàng (VD: Vận chuyển cẩn thận hàng dễ vỡ, Hàng lấy size S)

| shipId           | string       | staff              |  Id của bên ship chịu trách nhiệm vận chuyển của đơn hàng này, lựa chọn 1 trong list Đơn vị Ship trong hệ thống 

| shipLink         | string       | staff              |  Link google sheet có chứa đơn hàng này giữa staff và bên ship. 

| createdAt        | Date         |                   | Thời gian tạo đơn hàng                                                                                                                                                                                                                                                                                                      |
| updatedAt        | Date         |                   | Thời gian cập nhật đơn hàng                                                                                                                                                                                                                                                                                                 |
| deletedAt        | Date         |                   | Thời gian xoá đơn hàng                                                                                                                                                                                                                                                                                                      |

#### Bảng USER

| Trường dữ liệu   | Kiểu dữ liệu | Role được phép sửa | Mô tả                                                               |
|------------------|--------------|---------------------|---------------------------------------------------------------------|
| id               | string       | user                | ID của người dùng                                                    |
| email            | string       | user                | Email đăng nhập                                                      |
| password         | string       | user                | Mật khẩu đăng nhập (đã mã hóa), có thể null khi đăng nhập bằng Google |
| provider         | string       | user                | Phương thức đăng nhập (email/google), mặc định là email             |
| socialId         | string       | user                | ID từ mạng xã hội (Google), null khi đăng nhập bằng email           |
| firstName        | string       | user                | Tên                                                                  |
| lastName         | string       | user                | Họ                                                                   |
| photo            | file         | user                | Ảnh đại diện người dùng                                              |
| role             | enum         | user                | Role của người dùng (User/Staff/Admin/System)                        |
| status           | enum         | user                | Trạng thái tài khoản (active/inactive)                              |
| depositAmount    | number       | staff               | Số tiền đặt cọc của User                                            |
| depositLocking   | number       | staff               | Số tiền đặt cọc đang khoá chờ đơn hàng của User                     |
| totalAmount      | number       | staff               | Tổng số tiền hàng đã hoàn thành của User                            |
| createdAt        | Date         |                     | Thời gian tạo tài khoản                                             |
| updatedAt        | Date         |                     | Thời gian cập nhật tài khoản                                        |
| deletedAt        | Date         |                     | Thời gian xoá tài khoản                                             |


#### Bảng Ship

| Trường dữ liệu   | Kiểu dữ liệu | Role được phép sửa | Mô tả                                                               |
|------------------|--------------|---------------------|---------------------------------------------------------------------|
| id               | string       | staff                | ID của người dùng                                                    |
| shipName         | string       | staff                | Tên của bên Ship                                                      |
| shipNote         | string       | staff                | Ghi chú                                                               |
| shipLink         | string       | staff                | Link google sheet chứa các đơn hàng làm việc với bên ship này         |
| shipStatus       | enum         | staff                | Trạng thái bên Ship, Link Sheet này : Active, InActive, Completed     |

#### Bảng Lịch sử hoạt động : 
- Lưu trữ tất cả lịch sử hoạt động của Người dùng trong hệ thống, lịch sử thay đổi của đơn hàng : Giúp nắm rõ quá trình, không bị mất, sai lệch thông tin. 
- Ví dụ : Người dùng A đã Đăng nhập vào lúc nào. Đơn hàng được tạo khi nào, với các thông tin gì, bởi ai. Đơn hàng được thay đổi bởi ai, những thông tin gì, khi nào...
#### Bảng Thông báo : 
- Tạo thông báo, lưu thông báo của từng người dùng về các hoạt động, thay đổi trong hệ thống, giúp người dùng nhận thông tin 1 cách nhanh, dễ dàng. 
- Ví dụ : Khi đơn hàng của Người dùng được Xác nhận, người dùng sẽ nhận được thông báo Đơn hàng đã được xác nhận, xác nhận bởi ai. 
    + Khi Người dùng thực hiện tạo đơn hàng mới, Nhân viên sẽ nhận được thông báo : Người dùng A đã tạo đơn hàng mới, cần xác nhận. 


### Service Cập nhật Google Sheet đơn hàng của Staff và Ship : 
- Thực hiện Service chạy mỗi 5p / lần, đọc các Link google sheet chứa nơi tổng hợp đơn giữa staff và bên ship.
- Thực hiện kiểm tra các đơn hàng, thông tin đơn hàng và kiểm tra với thông tin trong hệ thống, xem đơn hàng có cập nhật gì mới không (Thông tin, trạng thái, )
- Mỗi khi đơn hàng được ACCEPTED, sẽ thực hiện cập nhật thông tin, tạo đơn hàng của user vào trong file sheet để gửi yêu cầu ship tới bên Ship. 

## ĐÁNH GIÁ HIỆU QUẢ VÀ THỜI GIAN TRIỂN KHAI

### Thời gian triển khai dự kiến
- **Giai đoạn 1 (Phát triển cơ bản)**: 1 - 3 tuần
  - Xây dựng cơ sở dữ liệu và API endpoints
  - Phát triển giao diện người dùng cơ bản
  - Triển khai chức năng đăng ký, đăng nhập và quản lý đơn hàng, quản lý người dùng, quản lý ship, tự động dữ liệu google sheet,... cơ bản đủ tính năng cho luồng làm việc 
  - Triển khai dự án lên server, domain, publish dự án tới mọi người dùng. 
  - Kiểm thử và triển khai thí điểm
- **Giai đoạn 2 (Phát triển đầy đủ)**: 0.5 - 2 tháng
  - Hoàn thiện tất cả chức năng hiện tại.
  - Bổ sung thêm tính năng mới : Quản lý thông tin cá nhân, Thông báo, Thống kê, Báo cáo chi tiết số liệu theo từng giờ, từng phút, từng ngày cho mỗi role, giúp theo dõi quan sát được hiệu năng hệ thống, tiến độ các đơn hàng, doanh thu hệ thống. 
  - Thực hiện testing, chỉnh sửa theo yêu cầu nghiệp vụ cho phù hợp. 
  - Tối ưu hóa hiệu suất và UX/UI

- **Tổng thời gian dự kiến**: 3 tháng từ lúc bắt đầu đến khi đưa vào sử dụng

### Nhân sự triển khai
- 1 Backend Developers
- 1 Frontend Developers
- 1 QA Engineer
- 1 UI/UX Designer (bán thời gian)

### Lợi ích kinh doanh
- **Giảm 40-50% thời gian xử lý đơn hàng** thông qua tự động hóa quy trình, nhân viên chỉ cần kiểm tra và kiểm duyệt, không cần nhập liệu. 
- **Tiết kiệm 30% chi phí nhân sự** trong quy trình vận hành đơn hàng
- **Giảm 25% lỗi trong quá trình xử lý đơn hàng** nhờ validation và quy trình chuẩn hóa
- **Tăng 45% khả năng theo dõi và minh bạch** trong toàn bộ quy trình, theo dõi nắm bắt chi tiết, rõ ràng về lịch sử hoạt động của người dùng, của đơn hàng. 
- **Cải thiện 30% mức độ hài lòng của khách hàng** nhờ cập nhật thông tin kịp thời, UI/UX thân thiện, dễ sử dụng. Khách sẽ thấy được sự chuyên nghiệp hơn, tăng uy tín. 
- **Tăng 15% năng suất nhân viên** nhờ công cụ quản lý tập trung
- **Tiết kiệm 70% thời gian tạo báo cáo và thống kê** cho ban lãnh đạo, xem thống kê số liệu bất cứ lúc nào 1 cách nhanh chóng, dễ dàng, nắm bắt lợi nhuận doanh thu tức thời (hàng giờ, hàng ngày, hàng tuần, hàng tháng)

### Tiềm năng : 
- Tiết kiệm dài hạn 25-40% chi phí vận hành hàng năm
- Tăng khả năng mở rộng quy mô kinh doanh, đơn hàng và khách hàng mà không cần tăng nhân sự tuyến tính, vẫn đảm bảo được dữ liệu đơn hàng chi tiết tỉ mỉ, không bị sai lệch, sót lọt dữ liệu. 
- Tiếp cận tệp khách hàng, dễ dàng thu hút người dùng sử dụng quá trình vận chuyển đơn hàng hơn nhờ sự chuyên nghiệp, thân thiện dễ dùng, minh bạch.

---

*Dự án Web Quản lý Đặt đơn hàng không chỉ là một hệ thống phần mềm - đây là giải pháp chuyển đổi số toàn diện mang lại lợi thế cạnh tranh rõ rệt, tối ưu hóa vận hành và nâng cao trải nghiệm khách hàng.*
