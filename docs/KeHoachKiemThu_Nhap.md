KẾ HOẠCH KIỂM THỬ NHÁP – SWAG LABS (SAUCEDEMO)
COMP1307 – Kiểm thử phần mềm cơ bản | Hướng A | Nhóm 9 | 4 thành viên
Trạng thái: bản nháp trước Buổi 4; chưa xác nhận các lỗi/rủi ro.
Ứng dụng luyện tập: https://www.saucedemo.com/

1. Mục tiêu
- Kiểm thử chức năng ứng dụng thương mại điện tử mẫu; xác minh yêu cầu với các dữ liệu hợp lệ/không hợp lệ, trạng thái và quy tắc nghiệp vụ.
- Mục tiêu toàn kỳ dành cho nhóm 4 người: 5 chức năng, tối thiểu 80 test case thủ công, 3 trường áp dụng EP/BVA, 2 kỹ thuật hộp đen khác, 2 hàm hộp trắng, 20 unit test, 10 kịch bản UI tự động. Mốc Buổi 7: ≥ 40 test case.
- Ghi nhận trung thực kết quả/bug có minh chứng; không tạo lỗi giả để đủ số lượng.
2. Phạm vi
Mã	Trong phạm vi	Ngoài phạm vi
F01	Đăng nhập và trạng thái tài khoản luyện tập	Dò mật khẩu/quét bảo mật
F02	Sắp xếp sản phẩm theo tên/giá	Quản trị dữ liệu hàng hóa
F03	Thêm sản phẩm, số đếm giỏ	Quản trị kho thật
F04	Xóa sản phẩm, giỏ rỗng/có hàng	Hệ thống giao nhận
F05	Checkout mô phỏng, dữ liệu bắt buộc, tổng tiền, xác nhận	Thanh toán ngân hàng thực


Cần giảng viên xác nhận việc tách F03 và F04 thành hai chức năng độc lập.
3. Cách tiếp cận
- Khảo sát ứng dụng rồi viết đặc tả/giả định có thể kiểm chứng. Không tự tạo yêu cầu tối đa về độ dài khi chưa xác minh.
- EP/BVA: First Name, Last Name, Postal Code: dữ liệu rỗng/không rỗng và độ dài 0/1; thêm dữ liệu giỏ hàng 0/1/2 để xét biên trạng thái.
- Bảng quyết định: các tổ hợp trường bắt buộc ở checkout. Chuyển trạng thái: giỏ hàng rỗng → thêm → xóa một phần → xóa hết.
- Hộp trắng: tự viết hai hàm mô phỏng calculate_cart_total(items) và validate_checkout_info(first,last,postal); phân tích CFG, V(G), đường cơ sở, đo bao phủ nhánh ≥80%.
- Kiểm thử đơn vị: Python/pytest; UI: Playwright hoặc Selenium; CI: GitHub Actions khi push/PR; quản lý lỗi: GitHub Issues; thực hiện ít nhất một lần hồi quy.
- Không dùng JMeter/ZAP/Burp lên hệ thống công cộng. Chỉ dùng tài khoản/dữ liệu luyện tập, không dữ liệu thật.
4. Tiêu chí đầu vào
1. Đã xác nhận 5 chức năng và có điều kiện kiểm thử mô tả được cho từng chức năng.
2. Trang thử nghiệm truy cập được, có ghi nhận trình duyệt, ngày giờ, tài khoản luyện tập.
3. Ca kiểm thử chuẩn bị thực thi đều có bước, dữ liệu và kết quả mong đợi rõ ràng.
4. Cả 4 thành viên có quyền dùng tài liệu/kho GitHub và trách nhiệm đã phân công.
5. Tiêu chí đầu ra dự kiến
1. Chạy 100% ca nằm trong phạm vi vòng kiểm thử đã thống nhất và ghi trạng thái thực tế.
2. Ít nhất 95% ca đã chạy ở trạng thái Pass; Fail/Blocked có lý do và issue/biện pháp.
3. Không còn lỗi nghiêm trọng cao chưa xử lý trên 5 luồng, hoặc đã có chấp thuận rủi ro rõ ràng.
4. Có 20 unit test, 10 UI test, CI chạy thành công trên bản cuối.
5. RTM bao phủ 100% các yêu cầu thuộc phạm vi được duyệt, có báo cáo kết thúc.
Các ngưỡng chất lượng là đề xuất của nhóm trong bản nháp, chưa phải quy định cố định của giảng viên.

6. Phân tích rủi ro (K × A, đánh giá giả định)
Mã	Loại	Rủi ro	K	A	Điểm	Giảm thiểu
DA01	Dự án	Kỹ năng viết UI test còn yếu	4	4	16	Làm 2 test mẫu, review chéo
SP01	Sản phẩm	Tổng tiền checkout hiển thị sai	3	5	15	Kiểm tra tính toán theo yêu cầu đã xác nhận
SP02	Sản phẩm	Giỏ hàng không đồng bộ sau thêm/xóa	3	4	12	Chuyển trạng thái, hồi quy
DA02	Dự án	Giao diện thay đổi làm hỏng locator	3	4	12	Locator ổn định, Page Object
DA03	Dự án	Chậm do phân công thiếu rõ ràng	3	4	12	Issues, kiểm tra hằng buổi
SP03	Sản phẩm	Điều hướng sai trạng thái đăng nhập	2	5	10	Bảng quyết định theo trạng thái phiên
SP04	Sản phẩm	Sắp xếp sản phẩm không đúng tùy chọn	3	3	9	So sánh toàn danh sách
DA04	Dự án	CI lỗi vì môi trường thiếu ổn định	3	3	9	Pin phiên bản, đọc log


Điểm 15–25: cao; 8–14: trung bình; 1–7: thấp. Các điểm đánh giá phải rà soát lại sau khi khảo sát ứng dụng.
7. Phân công
Thành viên	Vai trò dự kiến	Việc chính
Trần Minh Quân – 50.01.104.126	Điều phối	Phiếu đăng ký, test plan, README, tổng hợp
Nguyễn Huỳnh Ngọc Nhân – 50.01.104.106	Phân tích	Đăng nhập/sắp xếp, đặc tả, EP/BVA, RTM
Nguyễn Đăng Khôi – 50.01.104.077	Hộp trắng	Giỏ hàng, chuyển trạng thái, unit test
Kha Thái Bảo – 50.01.104.011	Tự động hóa	Checkout, UI test, GitHub Actions


Mọi thành viên đều tham gia chạy test, quản lý bug, review và có commit riêng.
8. Lịch trình
Mốc	Công việc
Trước Buổi 4	Nộp phiếu đăng ký LMS, kế hoạch nháp GitHub
Buổi 4–6	Khảo sát, đặc tả, ca kiểm thử vòng 1
Buổi 7	≥40 ca, RTM sơ bộ, báo cáo tiến độ
Buổi 7–8	Hộp đen, phân tích 2 hàm hộp trắng
Buổi 9	Unit test, CI
Buổi 10	UI automation, hồi quy, báo cáo, slide/video
7 ngày sau Buổi 10	Nộp đủ hồ sơ theo hướng dẫn


9. Ước lượng ba điểm sơ bộ
Dùng E=(a+4m+b)/6, SD=(b-a)/6 (giờ):
- Yêu cầu & kế hoạch: a=6, m=9, b=15 → E=9,50; SD=1,50.
- Test case & thực thi thủ công: a=28, m=40, b=58 → E=41,00; SD=5,00.
- UI/unit automation & CI: a=18, m=30, b=48 → E=31,00; SD=5,00.
- Tổng E = 81,50 giờ công ước lượng sơ bộ (không cộng SD trực tiếp).
