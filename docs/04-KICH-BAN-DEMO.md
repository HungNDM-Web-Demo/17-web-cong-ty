# Kịch bản demo — Website Công ty

> Dùng khi trình bày cho chủ doanh nghiệp vừa và nhỏ, trưởng phòng marketing cần làm mới website. Thời lượng 12–15 phút. Dữ liệu mẫu là công ty nội thất "Nội thất Lam Sơn". Đi theo một ngày của website: khách tìm thấy và gửi yêu cầu, nhân viên gọi lại, biên tập viên đăng bài, chủ doanh nghiệp xem hiệu quả.

---

## 1. Chuẩn bị trước buổi demo

- [ ] Mở sẵn link demo, thử "Đăng nhập nhanh" cả 3 vai trò
- [ ] Đặt lại dữ liệu demo (thanh công cụ demo → Đặt lại dữ liệu) để Tổng quan có 2 liên hệ mới hôm nay và 1 liên hệ quá hạn
- [ ] Đổi tên, logo, màu theo thương hiệu khách (Cài đặt → Thương hiệu) nếu đã có; nói trước với khách nội dung mẫu là công ty nội thất
- [ ] Mở hai cửa sổ: một cửa sổ khung điện thoại (375×812 hoặc điện thoại thật) cho phần Khách, một cửa sổ máy tính cho trang quản trị
- [ ] Chuẩn bị sẵn: 1 ảnh banner rộng từ 1920 px, nội dung bài viết khoảng 800 từ kèm 1 ảnh minh họa (dán vào, không gõ trước mặt khách), 8 ảnh công trình nhà phố
- [ ] Nếu chạy link online: thử dán link một bài viết vào Zalo để chắc ảnh xem trước hiện ra (link `localhost` không tạo được ảnh xem trước)

| Link | Ghi chú |
| :--- | :--- |
| FE | `http://localhost:3117` hoặc link online |
| Swagger | `https://localhost:7117/swagger` (khi khách hỏi về tích hợp) |

| Tài khoản | Vai trò | Dùng để cho xem |
| :--- | :--- | :--- |
| `admin` | Quản trị viên | Phân quyền, thương hiệu |
| `quanly` | Biên tập viên | Bài viết, dự án, dịch vụ, banner, nội dung trang, Tổng quan, báo cáo liên hệ |
| `nhanvien` | Nhân viên | Nhận và xử lý liên hệ, hồ sơ ứng tuyển |
| (không cần) | Khách | Website công khai, form liên hệ |

Mật khẩu: giá trị `DEMO_PASSWORD` trong `.env`, hoặc bấm "Đăng nhập nhanh".

---

## 2. Câu chuyện demo

> Mở đầu: "Anh/chị hình dung một khách hàng vừa tìm thấy website của công ty mình trên điện thoại. Em đi đúng một ngày: khách gửi yêu cầu, nhân viên gọi lại, bộ phận marketing đăng bài, và anh/chị biết website mang về bao nhiêu khách."

| # | Vai trò | Thao tác | Điểm cần nhấn mạnh |
| :---: | :--- | :--- | :--- |
| 1 | Khách | Mở trang chủ trên khung điện thoại: banner trượt, dịch vụ nổi bật, con số "850+ công trình", dự án nổi bật, nút Gọi, Zalo nổi | Phần lớn khách xem bằng điện thoại; trang tải nhanh, chữ rõ, nút bấm vừa ngón tay |
| 2 | Khách | Mở Dự án, lọc "Căn hộ", mở "Căn hộ 2 phòng ngủ 75 m²", vuốt xem ảnh | Ảnh công trình thật là thứ thuyết phục khách nhất; khách lọc đúng loại nhà của mình |
| 3 | Khách | Vào dịch vụ "Thi công nội thất trọn gói": quy trình 6 bước, giá "từ 4.500.000 ₫/m²"; bấm "Nhận báo giá", nhập tên, số điện thoại, diện tích 75 m², gửi | Form ngắn, dịch vụ chọn sẵn; khách nhận mã yêu cầu và lời hẹn gọi lại trong 24 giờ |
| 4 | Nhân viên | Đổi vai trò sang Nhân viên ở cửa sổ máy tính: chuông báo 4 liên hệ mới; mở liên hệ vừa gửi, bấm "Nhận xử lý" | Liên hệ không lẫn trong hộp thư email; ai nhận người đó chịu trách nhiệm |
| 5 | Nhân viên | Bấm số để gọi; ghi nhật ký "Đã trao đổi, hẹn khảo sát thứ Bảy 9:00", đặt giờ hẹn gọi lại | Lịch sử chăm sóc nằm trên hệ thống; nhân viên nghỉ việc cũng không mất khách |
| 6 | Nhân viên | Lọc "Quá hạn": thấy liên hệ gửi hôm qua chưa ai nhận, nhãn đỏ | Hệ thống tự nhắc khách bị bỏ quên, không đợi khách gọi lại phàn nàn |
| 7 | Biên tập viên | Đổi vai trò sang Biên tập viên; viết bài "5 lưu ý khi chọn gỗ công nghiệp cho tủ bếp": dán nội dung, chèn ảnh, xem khu SEO và bản xem trước Google; bấm "Đăng ngay" | Đăng bài như soạn Word; tiêu đề, mô tả SEO điền sẵn, có đếm ký tự, không cần biết kỹ thuật |
| 8 | Khách | Tải lại Tin tức trên khung điện thoại: bài mới đứng đầu, "4 phút đọc"; bấm chia sẻ Zalo | Đăng xong là lên ngay; link chia sẻ có ảnh, tiêu đề đẹp |
| 9 | Biên tập viên | Thêm banner "Ưu đãi tháng này: tặng bản vẽ 3D khi thi công trọn gói", hiển thị 30 ngày tới; xem trang chủ trên khung điện thoại | Chạy ưu đãi theo mùa không cần gọi lập trình viên; hết hạn banner tự ẩn |
| 10 | Biên tập viên | Thêm dự án "Nhà phố 4 tầng 5×18 m" với 8 ảnh, bật nổi bật: hệ thống báo đã đủ 6; bỏ nổi bật một dự án cũ rồi bật lại | Cập nhật hồ sơ năng lực ngay khi bàn giao công trình; trang chủ luôn gọn |
| 11 | Biên tập viên | Mở Tổng quan: liên hệ 30 ngày theo nguồn, tỉ lệ tiềm năng, bài xem nhiều; mở Báo cáo liên hệ theo người xử lý | Biết website mang về bao nhiêu khách, nguồn nào hiệu quả, ai phản hồi chậm |
| 12 | Quản trị viên | Đổi sang Quản trị viên, đổi màu thương hiệu và logo theo công ty khách; mở lại trang chủ | Website mang nhận diện của khách ngay trước mặt; phân quyền tách người viết nội dung với người cài đặt |

> Kết: "Toàn bộ nội dung anh/chị vừa thấy là dữ liệu mẫu. Bản triển khai sẽ dùng logo, màu, ảnh dự án và dịch vụ thật của công ty mình, gắn tên miền riêng."

---

## 3. Câu hỏi khách hay hỏi

| Câu hỏi | Trả lời gợi ý |
| :--- | :--- |
| Tên miền, hosting ai đứng tên? Mỗi năm tốn những khoản gì? | Tên miền đăng ký đứng tên công ty anh/chị. Chi phí hằng năm gồm tên miền và máy chủ; chứng chỉ SSL (ổ khóa https) có thể dùng loại miễn phí. Bên em báo giá cụ thể theo đuôi tên miền và dung lượng. |
| Website có phải đăng ký với Bộ Công Thương không? | Website chỉ giới thiệu công ty, không có đặt hàng, thanh toán trực tuyến thì không phải thông báo. Nếu sau này bán hàng trực tuyến thì cần thông báo website thương mại điện tử với Bộ Công Thương; bên em hỗ trợ thủ tục. |
| Làm xong có lên top Google không? | Website đã chuẩn SEO kỹ thuật: tốc độ, tiêu đề, mô tả, sitemap, hiển thị tốt trên điện thoại. Thứ hạng còn phụ thuộc nội dung và thời gian, nên bên em không cam kết top; trang quản trị giúp anh/chị đăng bài đều đặn để lên hạng bền vững. |
| Nhân viên không rành công nghệ có tự sửa được không? | Được. Sửa nội dung như soạn Word, có nút xem trước; phân quyền giúp người viết bài không đụng vào cài đặt hệ thống. |
| Có liên hệ mới thì báo về điện thoại, Zalo được không? | Demo báo bằng chuông trên trang quản trị và email giả lập. Bản triển khai gửi email thật, có thể thêm thông báo qua Zalo OA hoặc Telegram cho nhóm kinh doanh (Zalo OA tính phí theo tin nhắn). |
| Chuyển nội dung từ website cũ sang được không? | Được. Bên em khảo sát số trang, số bài; website cũ dùng WordPress thì chuyển bài viết, ảnh tự động và giữ đường dẫn cũ bằng chuyển hướng để không mất thứ hạng Google. |
| Có gắn Google Analytics, Facebook Pixel, chat Messenger, Zalo không? | Có. Demo đã có nút Zalo, Messenger; mã Google Analytics, Google Tag Manager, Facebook Pixel gắn khi triển khai. |
| Có làm song ngữ Việt, Anh không? | Có. Mỗi nội dung có thêm bản tiếng Anh, khách chuyển ngôn ngữ ở đầu trang; nội dung chưa dịch thì hiện bản tiếng Việt. |
| Thông tin khách để lại có an toàn không? | Chỉ người được cấp quyền mới xem; mỗi lần xuất danh sách đều ghi nhật ký; form có ô khách đồng ý cho dùng thông tin để liên hệ, phù hợp quy định bảo vệ dữ liệu cá nhân. |

---

## 4. Sau buổi demo

- [ ] Ghi lại yêu cầu khách nêu thêm vào `01-TONG-QUAN-NGHIEP-VU.md`
- [ ] Ghi lại: các trang, dịch vụ cần có; có tuyển dụng, song ngữ không; tên miền hiện có; website cũ (nền tảng, số bài); ai cập nhật nội dung; mấy người nhận liên hệ
- [ ] Xin khách logo, màu thương hiệu, 5–10 ảnh dự án thật để dựng bản demo mang thương hiệu khách
- [ ] Gửi link demo và tài khoản `quanly`, `nhanvien` cho khách tự trải nghiệm (nếu đồng ý)
