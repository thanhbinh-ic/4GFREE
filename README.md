# V2Ray Heroku
**Nếu bạn cần triển khai V2Ray VLESS，thì qua bài viết này [vless](https://github.com/bclswl0827/v2ray-heroku/tree/vless)**
********************************************************************************************************
## Giới thiệu:
Đây là một repository được fork lại từ https://github.com/bclswl0827/v2ray-heroku với chức năng là tạo ra một server V2Ray trên heroku một cách đơn giản nhất.

Heroku sẽ không khuyến khích việc này nên các bạn cần phải fork lại dự án này để không bị heroku chặn.

Với nhu cầu không quá cao thì heroku chính là giải pháp hoàn hảo cho anh em muốn dùng V2Ray để dùng 4G miễn phí:

2TB mỗi tháng
550 giờ mỗi tháng (~23 ngày, dĩ nhiên bạn cần ngủ 8 tiếng 1 ngày nên 550 giờ là quá đủ)

#### Đây là speedtest server heroku lúc 20h37 tại quận 4 HCM

![e27c4be5a5876dd934964](https://user-images.githubusercontent.com/92734523/139078147-8e621d87-0380-4b60-92ac-104635f6a771.jpg)

********************************************************************************************************

## Tổng quan

Dự án V2Ray WebSocket trên Heroku phải được sử dụng một cách hợp lý nếu không sẽ bị chặn

Sau khi triển khai, mỗi khi khởi động sẽ tải bản V2Ray mới nhất

## Truy cập CloudFlare

Hai phương pháp sau có thể kết nối ứng dụng với CloudFlare, từ đó tăng tốc độ ở một mức độ nhất định:

1. Liên kết tên miền với ứng dụng và kết nối tên miền với CloudFlare
2. Reverse proxy thông qua CloudFlare worker 

## Lưu ý

 1. **Xin đừng lạm dụng dự án này, có rất ít dịch vụ miễn phí như Heroku, hãy sử dụng và trân trọng**
 2. Nếu bạn sử dụng tên miền để kết nối với CloudFlare, vui lòng xem xét bật TLS 1.3 
 3. Hầu hết các địa chỉ AWS IPv4 đã bị Twitter chặn 

## Triển khai

### Video hướng dẫn

[![4G Free](https://img.youtube.com/vi/79jkqGWi0zU/0.jpg)](https://www.youtube.com/watch?v=79jkqGWi0zU)
[![4G Free 02](https://user-images.githubusercontent.com/82952557/139373288-74b8eb53-4f67-4202-866b-677bf2f60173.jpg)](https://youtu.be/98AGGL1ayv8)

### Đối số

Các đối số sẽ dùng trong quá trình cài đặt。

| Đối số | Mặc định | Diễn giải |
| :--- | :--- | :--- |
| `ID` | `ad806487-2d26-4636-98b6-ab85cc8521f7` | VMess user ID |
| `AID` | `64` | AlterID，Số từ 0 đến 65535 |
| `WSPATH` | `/` | |

### Bắt đầu

 1. Fork lại dự án này về `Github` của bạn, sửa lại tên dự án thành tên bất kỳ không nên chứa hai từ khóa `v2ray` và `heroku`
 2. Sửa file `README.md`, kéo xuống dòng 61 sửa link template thành link dự án `Github` của bạn (hoặc có thể sửa link sau khi bấm nút `Deploy` bên dưới)
 
> [![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https://github.com/thanhbinh-ic/4GFREE)

 3. Quay lại trang chủ của dự án, Click nút `Deploy to Heroku`
 4. Tạo app bên Heroku:
   - App name: không nên chứa hai từ khóa `v2ray` và `heroku`
   - Choose a region: `United States`
   - Lưu lại `AlterID` và `UUID`
   - Click `Deploy app`
   - Sau khi tạo xong app bấm nút `View`
 5. Trình duyệt sẽ mở ra 1 tab Bad Request, lưu lại địa chỉ url của nó (bỏ phần `https://`)
 6. Mở app V2Ray trên điện thoại, chọn thêm `Vmess`
   - Remarks: đặt tên bất kì
   - Address: địa chỉ url Bad Request
   - Port: `443`
   - ID, AlterID: nhập `UUID` và `AlterID` của app Heroku
   - Security: `auto`
   - Network: `ws`
   - Tls: `tls`
   - SNI: điền host bug theo nhà mạng
   - AllowInsecure: `true`
   
![IMG_20211029_094240](https://user-images.githubusercontent.com/82952557/139365095-14bf2375-52c6-426e-aa66-b3e852cdaeb7.jpg)
