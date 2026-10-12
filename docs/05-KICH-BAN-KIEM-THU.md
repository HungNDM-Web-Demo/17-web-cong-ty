# Kịch bản kiểm thử nghiệm thu — Website Công ty

> Test case theo use case trong `03-USE-CASE.md`. Phần nền (đăng nhập, phân quyền, đặt lại dữ liệu) dùng TC-SYS-01 đến TC-SYS-10 trong `ZDOCS/03-KIEN-TRUC/USE-CASE-NEN.md` §8.

---

## 1. Cách chạy

| Mục | Nội dung |
| :--- | :--- |
| Môi trường | Chạy cả hai chế độ: dữ liệu mẫu (`mock`) và BE thật (`api`) |
| Dữ liệu | Đặt lại dữ liệu demo trước mỗi lượt test; test case ghi "Đặt lại dữ liệu" ở bước 1 thì đặt lại ngay trước test đó |
| Tài khoản | Theo cột "Vai trò", dùng "Đăng nhập nhanh". Vai trò "Khách" chạy trong cửa sổ ẩn danh, không đăng nhập |
| Thiết bị | Test case vai trò Khách chạy ở 375×812 và 1440×900; vai trò khác chạy ở 1440×900 |
| Thứ tự | TC-10 đến TC-16 gửi form liên tiếp, chạy đúng thứ tự; bị chặn bởi giới hạn 3 lần trong 10 phút (BR-03) thì chờ đủ 10 phút |
| Đạt | Kết quả thực tế khớp toàn bộ cột "Kết quả mong đợi" |

**Dữ liệu mẫu dùng trong test**

- Công ty: tên thương hiệu "Nội thất Lam Sơn". Con số ấn tượng: "12 năm kinh nghiệm", "850+ công trình", "35 kiến trúc sư và kỹ sư", "98% khách hài lòng".
- Dịch vụ (6, 4 nổi bật): Thiết kế nội thất `thiet-ke-noi-that` từ 250.000 ₫/m² (nổi bật); Thi công nội thất trọn gói `thi-cong-noi-that-tron-goi` từ 4.500.000 ₫/m², quy trình 6 bước, gắn 5 dự án (nổi bật); Thiết kế kiến trúc từ 180.000 ₫/m² (nổi bật); Cải tạo nhà phố từ 2.800.000 ₫/m² (nổi bật); Nội thất văn phòng từ 3.200.000 ₫/m²; Sản xuất đồ gỗ theo yêu cầu `san-xuat-do-go-theo-yeu-cau` từ 4.200.000 ₫/m dài.
- Dự án (12, 6 nổi bật): Căn hộ 4 (2 dự án năm 2025, 2 dự án năm 2024), Nhà phố 3, Biệt thự 2, Văn phòng 2, Showroom 1. Dự án "Căn hộ 2 phòng ngủ 75 m²" `can-ho-2-phong-ngu-75-m2`: Thi công nội thất trọn gói, TP. Hồ Chí Minh, 2025, 75 m², 14 ảnh, nổi bật.
- Chuyên mục (4): Tin công ty, Kiến thức nội thất, Xu hướng thiết kế, Câu chuyện công trình.
- Bài viết (20): 16 Đã đăng (Kiến thức nội thất có 5 bài), 2 Nháp ("Xu hướng màu sắc nội thất 2027" đủ điều kiện đăng; "Bàn giao biệt thự Đà Nẵng" chưa có ảnh đại diện), 1 Hẹn giờ (8:00 ngày mai), 1 Đã gỡ "Thông báo nghỉ Tết Nguyên đán" `thong-bao-nghi-tet-nguyen-dan`. Bài ghim: "5 lưu ý khi thi công nội thất căn hộ chung cư", Kiến thức nội thất, 1.150 từ.
- Banner (6): 3 Đang hiển thị, 1 Chờ hiển thị (bắt đầu sau 3 ngày), 1 Hết hạn, 1 Tắt (không giới hạn ngày).
- Liên hệ (30, trải 90 ngày): 3 Mới (2 gửi hôm nay, 1 gửi cách đây 26 giờ), 5 Đang xử lý (4 giao `nhanvien` trong đó 1 Trễ hẹn, 1 giao `quanly`), 18 Đã xử lý (7 Tiềm năng, 11 Không phù hợp), 4 Spam. Trong 30 ngày gần nhất có 10 liên hệ Đã xử lý, 4 Tiềm năng. Trong 7 ngày gần nhất `nhanvien` nhận 3 liên hệ với thời gian phản hồi 1 giờ 20 phút, 2 giờ 10 phút, 30 phút.
- Tuyển dụng: Kiến trúc sư nội thất (Đang tuyển, 15 – 25 triệu, hạn nộp sau 20 ngày); Giám sát thi công (Đang tuyển, 14 – 20 triệu); Nhân viên kinh doanh dự án (Đang tuyển, Thỏa thuận); Kế toán tổng hợp (Hết hạn hôm qua). Số `0987654321` đã ứng tuyển Kiến trúc sư nội thất.

---

## 2. Test case

### 2.1. Trang công khai

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-01 | UC-01 | Trang chủ trên điện thoại | Khách | 1. Mở `/` ở 375×812 2. Chờ 7 giây | Banner có 3 slide (không có banner Chờ hiển thị, Hết hạn, Tắt), tự sang slide 2 sau 6 giây; 4 dịch vụ nổi bật; 4 con số ấn tượng; 6 dự án nổi bật; 3 bài mới với bài ghim đứng đầu; nút Gọi, Zalo nổi; không cuộn ngang |
| TC-02 | UC-01 | Menu điện thoại, trang Giới thiệu | Khách | 1. Bấm nút menu 2. Chọn "Giới thiệu" | Menu có đủ 7 mục; trang Giới thiệu có lịch sử, tầm nhìn, sứ mệnh, giá trị cốt lõi, đội ngũ, chứng nhận |
| TC-03 | UC-01 | Không có banner đang hiển thị | Biên tập viên, Khách | 1. Tắt cả 3 banner Đang hiển thị 2. Khách tải lại trang chủ | Khối banner hiện ảnh tĩnh mặc định kèm tên công ty, khẩu hiệu; các khối khác vẫn hiển thị đúng |
| TC-04 | UC-01 | Ảnh banner lỗi tải | Khách | 1. Đặt lại dữ liệu 2. Dùng công cụ dành cho nhà phát triển chặn tải ảnh banner 3. Tải lại trang chủ | Banner hiện nền màu thương hiệu kèm tiêu đề, nút; bố cục không vỡ, không khoảng trắng lớn |
| TC-05 | UC-02 | Chi tiết dịch vụ | Khách | 1. Mở `/dich-vu/thi-cong-noi-that-tron-goi` | Có quy trình 6 bước, giá "từ 4.500.000 ₫/m²", câu hỏi thường gặp, 3 dự án liên quan, nút "Nhận báo giá" |
| TC-06 | UC-02 | Lọc dự án | Khách | 1. Mở `/du-an` 2. Chọn loại Căn hộ 3. Chọn năm 2025 | Bước 2: 4 dự án. Bước 3: 2 dự án, có "Căn hộ 2 phòng ngủ 75 m²"; đường dẫn giữ bộ lọc |
| TC-07 | UC-02 | Đọc bài viết | Khách | 1. Mở bài "5 lưu ý khi thi công nội thất căn hộ chung cư" | Có ngày đăng dạng dd/MM/yyyy; "6 phút đọc" (1.150 ÷ 200 = 5,75, làm tròn lên); 3 bài liên quan cùng chuyên mục Kiến thức nội thất; nút chia sẻ Facebook, Zalo, sao chép link |
| TC-08 | UC-02 | Nội dung không công khai | Khách | 1. Mở `/tin-tuc/thong-bao-nghi-tet-nguyen-dan` 2. Mở `/sitemap.xml` | Bước 1: trang 404 có ô tìm kiếm, link về trang chủ. Bước 2: có 16 bài đã đăng, 6 dịch vụ, 12 dự án; không có bài Nháp, Hẹn giờ, Đã gỡ |
| TC-09 | UC-02 | Thẻ SEO của bài viết | Khách | 1. Mở bài ở TC-07, xem mã nguồn trang | Có `<title>`, `meta description`, `og:title`, `og:image`, `link rel="canonical"`, dữ liệu có cấu trúc kiểu `Article` |

### 2.2. Liên hệ

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-10 | UC-03 | Gửi liên hệ hợp lệ | Khách, Nhân viên | 1. Mở `/lien-he` 2. Nhập "Nguyễn Thị Lan", `0912 345 678`, để trống email, dịch vụ Thi công nội thất trọn gói, ngân sách 300–500 triệu, diện tích 75, nội dung "Cần báo giá thi công nội thất căn hộ 2 phòng ngủ 75 m²", tick đồng ý 3. Gửi 4. Nhân viên mở Quản lý liên hệ | Thông báo "Cảm ơn Nguyễn Thị Lan", mã dạng `LH{yyMMdd}{nnn}`, hẹn "trong vòng 24 giờ". Liên hệ trạng thái Mới, nguồn "Trang Liên hệ", số lưu `0912345678`, có thời điểm đồng ý; nhật ký có 1 email giả lập gửi hộp thư nhận liên hệ, không có email gửi khách; chuông từ 3 lên 4 |
| TC-11 | UC-03 | Kiểm tra số điện thoại | Khách | 1. Lần lượt nhập rồi rời ô: `0123456789`, `091234567`, `+84 912 345 678`, `028 3823 4567` | Hai số đầu báo "Số điện thoại chưa đúng"; `+84 912 345 678` hợp lệ, lưu `0912345678`; `028 3823 4567` hợp lệ, lưu `02838234567` |
| TC-12 | UC-03 | Thiếu điều kiện bắt buộc | Khách | 1. Nhập đủ thông tin, không tick đồng ý 2. Tick đồng ý, sửa nội dung còn "Báo giá" (8 ký tự) | Bước 1 nút "Gửi" vô hiệu. Bước 2 báo "Nội dung tối thiểu 10 ký tự" |
| TC-13 | UC-03 | Nhận báo giá từ trang dịch vụ | Khách | 1. Mở `/dich-vu/thiet-ke-noi-that` 2. Bấm "Nhận báo giá", nhập "Trần Văn Hùng", `0978 111 222`, nội dung "Thiết kế căn hộ 68 m²", tick đồng ý, gửi | Hộp thoại có sẵn dịch vụ Thiết kế nội thất; liên hệ lưu nguồn "Nhận báo giá" |
| TC-14 | UC-03 | Gửi trùng trong 24 giờ | Khách, Nhân viên | 1. Sau TC-10, gửi lại với `0912345678`, nội dung "Bổ sung: muốn thi công xong trước Tết" | Khách thấy thông báo với đúng mã của TC-10; không có liên hệ mới; nhật ký liên hệ cũ có dòng "Khách gửi lại" kèm nội dung bổ sung; chuông không tăng |
| TC-15 | UC-03 | Giới hạn 3 lần trong 10 phút | Khách | 1. Từ một máy chưa gửi form trong 10 phút, gửi liên tiếp 4 liên hệ hợp lệ với 4 số điện thoại khác nhau | 3 lần đầu thành công; lần 4 báo "Anh/chị đã gửi nhiều lần, vui lòng thử lại sau 10 phút hoặc gọi hotline", không lưu |
| TC-16 | UC-03 | Trường bẫy bot | Khách, Nhân viên | 1. Dùng công cụ dành cho nhà phát triển điền giá trị vào trường ẩn của form, gửi 2. Nhân viên lọc Spam | Khách thấy thông báo thành công; liên hệ nằm ở trạng thái Spam, không có email giả lập, chuông không tăng |

### 2.3. Xử lý liên hệ

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-17 | UC-05 | Nhận, ghi nhật ký, hoàn tất | Nhân viên | 1. Mở liên hệ của TC-10, bấm "Nhận xử lý" 2. Thêm nhật ký: Gọi điện, Đã trao đổi, "Hẹn khảo sát thứ Bảy 9:00" 3. Bấm "Hoàn tất", chọn Tiềm năng, ghi chú "Khách chốt lịch khảo sát" | Bước 1: trạng thái Đang xử lý, người xử lý `nhanvien`, có thời điểm nhận. Bước 3: trạng thái Đã xử lý, kết quả Tiềm năng; liên hệ không còn trong bộ lọc Mới |
| TC-18 | UC-05 | Hoàn tất khi chưa có nhật ký | Nhân viên | 1. Nhận liên hệ của TC-13 2. Bấm "Hoàn tất" ngay | Báo "Cần ít nhất 1 nhật ký chăm sóc trước khi hoàn tất"; trạng thái vẫn Đang xử lý |
| TC-19 | UC-05 | Hai người cùng nhận | Nhân viên, Quản trị viên | 1. Mở cùng một liên hệ Mới ở hai trình duyệt, đăng nhập `nhanvien` và `admin` 2. `nhanvien` bấm "Nhận xử lý" 3. `admin` bấm "Nhận xử lý" | Bước 3 báo "Liên hệ đã được {tên của nhanvien} nhận"; người xử lý vẫn là `nhanvien` |
| TC-20 | UC-05 | Liên hệ quá hạn | Nhân viên | 1. Đặt lại dữ liệu 2. Lọc "Quá hạn" | Có đúng 1 liên hệ: gửi cách đây 26 giờ, trạng thái Mới, nhãn đỏ "Quá hạn" |
| TC-21 | UC-05 | Phạm vi của nhân viên | Nhân viên | 1. Lọc trạng thái Đang xử lý 2. Mở link chi tiết của liên hệ đang giao cho `quanly` | Bước 1: chỉ thấy 4 liên hệ giao cho mình, 1 liên hệ có nhãn "Trễ hẹn". Bước 2: báo không có quyền xem |
| TC-22 | UC-05 | Spam và khôi phục | Nhân viên | 1. Đánh dấu spam một liên hệ Mới gửi hôm nay 2. Lọc Spam, bấm "Khôi phục" | Bước 1: trạng thái Spam, chuông từ 3 xuống 2. Bước 2: về Mới, chưa có người xử lý, chuông về 3 |
| TC-23 | UC-05 | Mở lại cần lý do | Nhân viên | 1. Mở một liên hệ Đã xử lý của `nhanvien`, bấm "Mở lại", để trống lý do 2. Nhập "Khách gọi lại đổi diện tích", xác nhận | Bước 1 nút xác nhận vô hiệu. Bước 2 liên hệ về Đang xử lý, lý do ghi vào nhật ký |
| TC-24 | UC-05 | Chuyển người xử lý | Biên tập viên, Nhân viên | 1. Biên tập viên chọn một liên hệ Đang xử lý của `nhanvien`, chuyển cho `quanly` 2. Đổi sang Nhân viên xem danh sách | Liên hệ có trong "Của tôi" của `quanly`; danh sách của `nhanvien` không còn liên hệ đó |

### 2.4. Quản trị nội dung

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-25 | UC-04 | Đăng bài mới | Biên tập viên, Khách | 1. Viết bài "5 lưu ý khi chọn gỗ công nghiệp cho tủ bếp", chuyên mục Kiến thức nội thất, ảnh đại diện có văn bản thay thế, tóm tắt 120 ký tự, nội dung 800 từ 2. Bấm "Đăng ngay" 3. Khách mở `/tin-tuc` | Slug `5-luu-y-khi-chon-go-cong-nghiep-cho-tu-bep`; trong 60 giây bài đứng đầu danh sách Tin tức, hiện "4 phút đọc" (800 ÷ 200); có trong `sitemap.xml` |
| TC-26 | UC-04 | Đăng khi thiếu điều kiện | Biên tập viên | 1. Mở bài Nháp "Bàn giao biệt thự Đà Nẵng", sửa nội dung còn 200 ký tự 2. Bấm "Đăng ngay" | Liệt kê 2 mục thiếu: "Cần ảnh đại diện có văn bản thay thế", "Nội dung tối thiểu 300 ký tự"; bài giữ trạng thái Nháp |
| TC-27 | UC-04 | SEO mặc định và cảnh báo độ dài | Biên tập viên | 1. Mở bài "5 lưu ý khi thi công nội thất căn hộ chung cư", xóa trống tiêu đề SEO 2. Lưu | Tiêu đề SEO tự điền "5 lưu ý khi thi công nội thất căn hộ chung cư \| Nội thất Lam Sơn" (45 + 3 + 16 = 64 ký tự); bộ đếm 64/60 kèm cảnh báo vàng; vẫn lưu được |
| TC-28 | UC-04 | Hẹn giờ đăng | Biên tập viên, Khách | 1. Mở bài Nháp "Xu hướng màu sắc nội thất 2027", hẹn giờ bằng hiện tại + 2 phút 2. Đổi thành hiện tại + 6 phút, lưu 3. Chờ 7 phút, khách mở Tin tức | Bước 1 báo "Giờ hẹn phải sau thời điểm hiện tại ít nhất 5 phút". Bước 2 bài trạng thái Hẹn giờ, chưa có ở Tin tức. Bước 3 bài Đã đăng, có ở Tin tức, ngày đăng bằng giờ hẹn |
| TC-29 | UC-04 | Sửa bài đã đăng, đổi slug | Biên tập viên, Khách | 1. Sửa bài ở TC-07, đổi slug thành `luu-y-thi-cong-noi-that-chung-cu`, lưu 2. Khách mở slug cũ | Ngày đăng giữ nguyên, trang bài có "Cập nhật {hôm nay}"; slug cũ chuyển hướng 301 tới slug mới |
| TC-30 | UC-04 | Xóa bài đã từng đăng | Biên tập viên | 1. Chọn bài Đã gỡ "Thông báo nghỉ Tết Nguyên đán" | Nút "Xóa" vô hiệu, gợi ý giữ ở trạng thái Đã gỡ |
| TC-31 | UC-06 | Thêm dự án | Biên tập viên, Khách | 1. Thêm "Nhà phố 4 tầng mặt tiền 5 m": Nhà phố, dịch vụ Cải tạo nhà phố, Hà Nội, 2026, 360 m², ảnh bìa có văn bản thay thế, 8 ảnh 2. Bấm "Lưu và hiển thị" 3. Khách lọc Nhà phố ở `/du-an` | Slug `nha-pho-4-tang-mat-tien-5-m`; lọc Nhà phố ra 4 dự án, có dự án mới |
| TC-32 | UC-06 | Nổi bật quá 6 | Biên tập viên | 1. Bật nổi bật cho dự án ở TC-31 2. Bỏ nổi bật một dự án cũ, bật lại cho dự án mới | Bước 1 báo "Trang chủ hiển thị tối đa 6, hãy bỏ bớt một mục". Bước 2 thành công, trang chủ có dự án mới trong 6 dự án nổi bật |
| TC-33 | UC-06 | Xóa dịch vụ đang dùng | Biên tập viên | 1. Xóa dịch vụ Thi công nội thất trọn gói | Từ chối, báo dịch vụ đang gắn với dự án và liên hệ, gợi ý "Ẩn" |
| TC-34 | UC-06 | Ẩn dịch vụ | Biên tập viên, Khách | 1. Ẩn dịch vụ Sản xuất đồ gỗ theo yêu cầu 2. Khách mở `/dich-vu` và `/dich-vu/san-xuat-do-go-theo-yeu-cau` | Danh sách còn 5 dịch vụ; link chi tiết trả 404; dịch vụ không còn trong `sitemap.xml` |
| TC-35 | UC-08 | Thêm banner | Biên tập viên, Khách | 1. Đặt lại dữ liệu 2. Thêm banner "Ưu đãi tháng này: tặng bản vẽ 3D khi thi công trọn gói", ảnh 1920×800 có văn bản thay thế, hiển thị từ hôm nay tới hôm nay + 30 ngày, bật 3. Khách tải trang chủ | Banner trạng thái Đang hiển thị; trang chủ có 4 slide |
| TC-36 | UC-08 | Vượt 5 banner đang bật | Biên tập viên | 1. Sau TC-35, bật banner đang Tắt | Báo "Tối đa 5 banner đang bật" (3 Đang hiển thị + 1 Chờ hiển thị + 1 mới = 5); banner giữ trạng thái Tắt |
| TC-37 | UC-08 | Ảnh banner không đạt | Biên tập viên | 1. Thêm banner với ảnh máy tính rộng 1280 px, để trống văn bản thay thế 2. Lưu | Báo 2 lỗi: "Ảnh máy tính cần rộng tối thiểu 1440 px", "Cần văn bản thay thế"; không lưu |
| TC-38 | UC-08 | Sửa con số ấn tượng | Biên tập viên, Khách | 1. Nội dung trang → tab Trang chủ, đổi "850+ công trình" thành "870+ công trình", lưu 2. Khách tải lại trang chủ | Trong 60 giây trang chủ hiện "870+ công trình" |

### 2.5. Tổng quan và báo cáo

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-39 | UC-07 | Tổng quan của Biên tập viên | Biên tập viên | 1. Đặt lại dữ liệu 2. Đăng nhập nhanh Biên tập viên | Vào `/admin`; thẻ: Mới hôm nay 2, Chưa nhận 3, Quá hạn 1, Tỉ lệ tiềm năng 30 ngày 40,0% (4 ÷ 10); biểu đồ 30 ngày chia theo nguồn; 5 liên hệ mới nhất; bài hẹn giờ 8:00 ngày mai |
| TC-40 | UC-07 | Tổng quan cập nhật theo liên hệ mới | Khách, Biên tập viên | 1. Khách gửi 1 liên hệ hợp lệ với số `0933 555 777` 2. Biên tập viên tải lại Tổng quan | Mới hôm nay 3, Chưa nhận 4 |
| TC-41 | UC-07 | Tổng quan của nhân viên | Nhân viên | 1. Đặt lại dữ liệu 2. Đăng nhập nhanh Nhân viên 3. Gõ thẳng `/admin/reports` | Thẻ: Mới chưa nhận 3, Của tôi đang xử lý 4, Quá hạn 1, Trễ hẹn của tôi 1; không có tỉ lệ tiềm năng, biểu đồ, bài xem nhiều. Bước 3 chuyển tới `/forbidden` |
| TC-42 | UC-07 | Thời gian phản hồi theo người xử lý | Biên tập viên | 1. Mở Báo cáo liên hệ, chọn 7 ngày, tab Theo người xử lý | Dòng `nhanvien`: 3 liên hệ đã nhận, thời gian phản hồi trung bình "1 giờ 20 phút" ((80 + 130 + 30) ÷ 3 = 80 phút) |
| TC-43 | UC-07 | Khoảng ngày quá dài | Biên tập viên | 1. Chọn Tùy chọn từ 01/01/2025 tới hôm nay | Báo lỗi khoảng tối đa 366 ngày |
| TC-44 | UC-07 | Xuất Excel có ghi nhật ký | Biên tập viên, Quản trị viên | 1. Ở Quản lý liên hệ lọc Đã xử lý, bấm "Xuất Excel" 2. Quản trị viên mở Nhật ký thao tác | File có 18 dòng; nhật ký có dòng xuất của `quanly` kèm bộ lọc "Đã xử lý" và số dòng 18 |

### 2.6. Tuyển dụng

| Mã | UC | Tình huống | Vai trò | Các bước | Kết quả mong đợi |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TC-45 | UC-09 | Ứng tuyển hợp lệ | Khách | 1. Mở tin Kiến trúc sư nội thất 2. Nhập "Phạm Minh Tuấn", `0901 234 567`, email, CV PDF 1,2 MB, bấm "Nộp hồ sơ" | Thông báo "Đã nhận hồ sơ", mã dạng `UV{yyMMdd}{nnn}`; hồ sơ trạng thái Mới ở trang quản trị |
| TC-46 | UC-09 | CV không hợp lệ | Khách | 1. Tải CV PDF 6 MB 2. Tải CV dạng JPG | Mỗi lần báo lỗi riêng: "CV tối đa 5 MB", "Chỉ nhận PDF, DOC, DOCX" |
| TC-47 | UC-09 | Ứng tuyển trùng | Khách | 1. Nộp tin Kiến trúc sư nội thất với số `0987 654 321` | Báo "Bạn đã ứng tuyển vị trí này ngày dd/MM/yyyy", không tạo hồ sơ mới |
| TC-48 | UC-09 | Tin hết hạn | Khách | 1. Mở `/tuyen-dung` 2. Mở link tin Kế toán tổng hợp | Bước 1 danh sách có 3 tin Đang tuyển, không có Kế toán tổng hợp. Bước 2 trang tin có nhãn "Đã hết hạn", không có form ứng tuyển |
| TC-49 | UC-10 | Xử lý hồ sơ | Nhân viên | 1. Mở hồ sơ của TC-45 2. Đổi trạng thái Hẹn phỏng vấn, ghi chú "Phỏng vấn 14:00 thứ Năm" | Bước 1 trạng thái tự chuyển Đã xem. Bước 2 lưu trạng thái và ghi chú |

---

## 3. Biên bản chạy thử

| Ngày | Người test | Chế độ | Số TC đạt / tổng | Lỗi ghi nhận |
| :--- | :--- | :--- | :---: | :--- |
| | | | | |
