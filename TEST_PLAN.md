# KẾ HOẠCH KIỂM THỬ NHÁP – SWAG LABS

COMP130702 – Nhóm 6 WiggleWorm · Bài nhóm 3.2 · Phiên bản 0.1, ngày 03/11/2026

Đề tài chính: số 1, kiểm thử ứng dụng thương mại điện tử mẫu Swag Labs, hướng A.
Đề tài dự phòng: số 3, kiểm thử biểu mẫu và thành phần web trên DemoQA.
Nhóm trưởng: Nguyễn Minh Đại. Kho nhóm: https://github.com/ChuongNguyenNHC/EduReg-Testing-WiggleWorm

Đây là kế hoạch dự kiến, chưa phải báo cáo kết quả thực thi. Tên kho còn chứa EduReg là tên kỹ thuật hiện tại; đối tượng của kế hoạch này là Swag Labs. EduReg chỉ dùng cho bài thực hành cá nhân Buổi 3. Đề tài chờ giảng viên duyệt và xác nhận điều kiện không trùng nhóm khác.

## 1. Mục tiêu

Kiểm tra tính đúng đắn của luồng đăng nhập → chọn sản phẩm → giỏ hàng → checkout mô phỏng. Ưu tiên sai dữ liệu giỏ, sai tổng tiền và bỏ qua trường bắt buộc. Xây dựng hồ sơ có thể truy vết từ yêu cầu đến ca kiểm thử, kết quả và báo cáo lỗi.

Mục tiêu cuối kỳ cho nhóm 5 người theo hướng dẫn học phần:

- Kiểm thử 6 chức năng, thiết kế ít nhất 100 ca kiểm thử mức thấp, mỗi ca có bước thực hiện và kết quả mong đợi.
- Áp dụng EP/BVA cho 4 trường hoặc đại lượng dữ liệu. Dùng cả bảng quyết định và chuyển trạng thái.
- Phân tích hộp trắng 3 hàm mô phỏng, viết ít nhất 25 unit test và 12 kịch bản tự động UI.
- Mọi yêu cầu trong phạm vi có ít nhất một ca kiểm thử. Ghi rõ ca chưa chạy, bị chặn, đạt và không đạt.
- Hướng tới 10 báo cáo lỗi có minh chứng. Nếu không có đủ lỗi thật, báo cáo số thực tế và bằng chứng kiểm thử, không tạo lỗi giả để đủ số lượng.

Các số lượng trên là mục tiêu cuối kỳ, không phải yêu cầu hoàn tất ngay ở Buổi 3.

## 2. Phạm vi

| Mã | Chức năng trong phạm vi | Nội dung trọng tâm |
|---|---|---|
| SW01 | Đăng nhập | Tài khoản mẫu hợp lệ, sai thông tin, tài khoản bị khóa theo mô tả của ứng dụng |
| SW02 | Danh sách và chi tiết sản phẩm | Tên, ảnh, giá và sự nhất quán giữa các màn hình |
| SW03 | Sắp xếp sản phẩm | Thứ tự tên/giá theo từng chế độ, đổi chế độ liên tiếp |
| SW04 | Thêm sản phẩm vào giỏ | Đúng sản phẩm, cập nhật badge và nội dung giỏ |
| SW05 | Xóa sản phẩm khỏi giỏ | Xóa một/nhiều món, giỏ rỗng, tổng tiền sau khi xóa |
| SW06 | Checkout mô phỏng | Trường bắt buộc, tổng kết, subtotal/tax/total, Finish, Cancel/quay lại |

Ngoài phạm vi: thanh toán ngân hàng thật, tồn kho, voucher, giao hàng, hoàn tiền, quản trị hệ thống, API không được công bố và mã nguồn máy chủ. Không thực hiện kiểm thử tải hoặc quét bảo mật trên hệ thống công khai. Chỉ dùng thao tác chức năng thông thường, tài khoản mẫu và dữ liệu giả.

DemoQA chỉ triển khai nếu được duyệt chuyển đề tài. Khi chuyển phải cập nhật đặc tả, rủi ro, phân công và kế hoạch; không gộp kết quả của hai ứng dụng thành một bộ kiểm thử.

## 3. Cơ sở kiểm thử và môi trường

Đối tượng: https://www.saucedemo.com/. Bắt đầu từ tài khoản chuẩn do ứng dụng cung cấp, ghi tên tài khoản/biến thể sử dụng. Nhóm khảo sát rồi viết đặc tả giả định có mã yêu cầu. Các hành vi chưa có tài liệu phải ghi rõ cơ sở quan sát và điểm cần hỏi giảng viên, không tự kết luận là lỗi chỉ vì khác suy đoán.

Mỗi lần chạy ghi ngày giờ, URL, tài khoản, hệ điều hành, phiên bản trình duyệt, kích thước cửa sổ và dữ liệu ban đầu. Dự kiến dùng Chrome/Chromium làm môi trường chính, Firefox để kiểm tra tương thích. Chốt phiên bản thực tế trong nhật ký khi bắt đầu, không ghi phiên bản chưa cài đặt.

Công cụ: Excel cho ca kiểm thử/RTM; GitHub Issues cho lỗi; Python, pytest và coverage cho mã mô phỏng; Playwright cho UI; GitHub Actions cho CI. Mỗi ca độc lập cần reset giỏ hoặc phiên đăng nhập để tránh ảnh hưởng lẫn nhau.

Các điểm cần chốt trước Buổi 4–6:

1. Chính sách khoảng trắng và độ dài First Name, Last Name, Postal Code.
2. Postal Code có kiểm tra định dạng hay chỉ bắt buộc nhập. Không giả định quy tắc bưu chính Việt Nam cho ứng dụng mẫu.
3. Quy tắc thuế và làm tròn tiền. Phân biệt phép tính total = subtotal + tax hiển thị với việc xác minh công thức tax.
4. Hành vi checkout với giỏ rỗng, Cancel, Back và trạng thái sau Finish.
5. Giới hạn số sản phẩm khác nhau trong giỏ và khả năng thay đổi số lượng mà giao diện thực tế cho phép.

## 4. Cách tiếp cận

### 4.1 Kiểm thử tĩnh và thủ công

Rà soát đặc tả, loại bỏ yêu cầu mơ hồ. Thiết kế ca theo rủi ro, thực hiện smoke test trước mỗi đợt chạy. Ghi kết quả thực tế kèm ảnh/video cho lỗi, không đánh dấu Pass khi chưa chạy.

EP/BVA cho First Name, Last Name, Postal Code và số sản phẩm trong giỏ. Phân lớp rỗng/không rỗng, khoảng trắng, ký tự hợp lệ theo đặc tả. Dùng biên độ dài 0/1 và các giới hạn được xác nhận; nếu không có giới hạn trên thì ghi rõ, không tự đặt. Với giỏ, dùng 0/1/nhiều sản phẩm và biên số lượng tối đa quan sát được nếu có. Đây là số sản phẩm trong giỏ, không mặc định có ô nhập quantity.

Bảng quyết định: ba trường checkout đủ/thiếu, đủ 8 tổ hợp, đối chiếu hành vi tiếp tục/thông báo. Chuyển trạng thái: danh sách → giỏ có hàng/rỗng → nhập checkout → tổng kết → hoàn tất, cùng các nhánh Cancel/Back. Tổ chức ít nhất 2 phiên thăm dò có điều lệ về giỏ và checkout.

### 4.2 Hộp trắng và kiểm thử đơn vị

Nhóm tự viết 3 hàm mô phỏng: `calculate_subtotal(items)`, `calculate_order_total(subtotal, tax, discount=0)` và `validate_checkout_info(first_name, last_name, postal_code)`.

Phân tích CFG, V(G), đường cơ sở và thiết kế ít nhất 25 unit test tổng cộng. `discount=0` cho mọi kịch bản ánh xạ Swag Labs. Nếu giữ nhánh discount khác 0 để luyện hộp trắng thì ghi rõ là mở rộng của mô hình nhóm, ngoài phạm vi giao diện Swag Labs. Unit test và coverage chỉ phản ánh mã mô phỏng, không phải mã nguồn của trang công khai.

### 4.3 Tự động hóa và hồi quy

Thiết kế ít nhất 12 UI script ổn định, ưu tiên đăng nhập, sắp xếp, thêm/xóa giỏ và checkout. Mỗi script có tiền điều kiện, dữ liệu, bước và assertion. CI chạy unit test trên mỗi cập nhật mã; UI chạy tuần tự với quy mô nhỏ, không dùng làm công cụ tải. Lưu log và ảnh khi thất bại. Chạy lại ca lỗi và bộ hồi quy liên quan khi thay đổi script hoặc phiên bản môi trường.

## 5. Tiêu chí đầu vào

1. Đề tài và 6 chức năng đã được chốt với giảng viên; đặc tả giả định có phiên bản, các điểm mơ hồ đã được ghi nhận.
2. URL, tài khoản mẫu và trình duyệt hoạt động; smoke test đăng nhập → thêm giỏ → checkout chạy được hoặc đã có mô tả chặn cụ thể.
3. Ca kiểm thử có mã yêu cầu, dữ liệu, bước và kết quả mong đợi; 100% ca dự kiến chạy trong đợt đã được rà soát.
4. Kho GitHub, mẫu báo lỗi, nơi lưu minh chứng và quy tắc reset dữ liệu đã sẵn sàng; người phụ trách biết phần việc của mình.

## 6. Tiêu chí đầu ra

1. Đã thiết kế ít nhất 100 ca và thực thi 100% ca thuộc phạm vi đợt nghiệm thu. Mọi ca bị chặn/chưa chạy phải có lý do và đánh giá tác động.
2. 100% yêu cầu có liên kết tới ca kiểm thử. Toàn bộ rủi ro ưu tiên cao có ca kiểm thử và bằng chứng kết quả.
3. Mục tiêu tỷ lệ Pass ít nhất 95% trên số ca đã thực thi; không còn lỗi Critical/High chưa đánh giá. Vì nhóm không sửa được ứng dụng công khai, lỗi tồn tại phải có bằng chứng và được nêu rõ trong kết luận, không tự đổi thành Pass để đạt ngưỡng.
4. Có phân tích 3 hàm, ít nhất 25 unit test và 12 UI script. Unit test mã mô phỏng đạt, CI có kết quả được lưu; UI fail phải được phân biệt lỗi ứng dụng/môi trường/script.
5. Báo cáo tổng kết, bảng lỗi, RTM, phụ lục AI và bảng đóng góp hoàn tất, link minh chứng truy cập được. Nếu không đạt ngưỡng, nhóm vẫn báo cáo trung thực và kết luận hạn chế, không tuyên bố chất lượng đạt.

## 7. Rủi ro và ưu tiên

K là khả năng, A là ảnh hưởng, đều 1–5. Điểm = K × A; 15–25 cao, 8–14 trung bình, 1–7 thấp. Điểm dưới đây là ước lượng dự kiến của bản nháp, không phải tần suất sự cố đo được.

| Mã | Loại | Rủi ro | K | A | Điểm | Biện pháp và người phụ trách |
|---|---|---|---:|---:|---:|---|
| S01 | SP | Giỏ cập nhật sai sản phẩm hoặc tổng tiền sau thêm/xóa | 4 | 4 | 16 | Ngân: chuyển trạng thái, đối chiếu dữ liệu trước/sau |
| S02 | SP | Checkout tính sai subtotal/tax/total | 3 | 5 | 15 | Đại: kiểm tra phép tính, quy tắc làm tròn đã chốt |
| S03 | SP | Bỏ qua trường bắt buộc hoặc thông báo sai | 3 | 4 | 12 | Như: bảng quyết định, EP/BVA |
| S04 | SP | Tài khoản hợp lệ/bị khóa bị xử lý sai | 3 | 4 | 12 | Chương: EP tài khoản và kiểm tra trang đích |
| P01 | DA | Thiếu đặc tả rõ nên kết quả mong đợi không thống nhất | 4 | 3 | 12 | Đại: ghi giả định và chốt trước khi chạy |
| P02 | DA | Khác tài khoản/môi trường/dữ liệu giỏ làm khó tái hiện | 3 | 4 | 12 | Phong: checklist môi trường và reset dữ liệu |
| S05 | SP | Sắp xếp tên/giá sai thứ tự | 3 | 3 | 9 | Phong: đối chiếu toàn bộ thứ tự theo chế độ |
| P03 | DA | Thành viên bận thi hoặc trễ phần việc | 3 | 3 | 9 | Đại: chia việc độc lập, mốc nhỏ, dự phòng người |

Ma trận số rủi ro theo K/A:

| K \\ A | 1 | 2 | 3 | 4 | 5 |
|---|---:|---:|---:|---:|---:|
| 5 | 0 | 0 | 0 | 0 | 0 |
| 4 | 0 | 0 | 1 | 1 | 0 |
| 3 | 0 | 0 | 2 | 3 | 1 |
| 2 | 0 | 0 | 0 | 0 | 0 |
| 1 | 0 | 0 | 0 | 0 | 0 |

Ưu tiên S01, S02 trước; sau đó S03/S04 và xử lý P01/P02 từ giai đoạn chuẩn bị. Các điểm có thể khác bảng AI vì là lần đánh giá ưu tiên kế hoạch, không sao chép máy móc điểm AI. Cần chốt lại cùng nhóm trước khi thực thi.

## 8. Phân công

Phân công Buổi 3 giữ theo thống nhất của nhóm:

| Thành viên | MSSV | Công việc Buổi 3 | Phần tiểu luận dự kiến |
|---|---|---|---|
| Nguyễn Minh Đại | 49.01.104.027 | Bài nhóm 3.2: kế hoạch nháp, tổng hợp | Checkout/tổng tiền, 20 ca, 5 unit test, 2 UI script, quản lý tiến độ |
| Nguyễn Hoàng Chương | 49.01.104.015 | Bài nhóm 3.2: đăng ký, README, GitHub | Đăng nhập, 20 ca, 5 unit test, 3 UI script, CI |
| Nguyễn Thị Mỹ Ngân | 50.01.104.098 | Bài nhóm 3.1: rủi ro sản phẩm UniPay | Thêm/xóa giỏ, 20 ca, 5 unit test, 3 UI script |
| Nguyễn Quỳnh Như | 50.01.104.113 | Thực hành 3.2: phản biện AI, bổ sung rủi ro | Kiểm tra dữ liệu checkout, 20 ca, 5 unit test, 2 UI script |
| Lê Hoàng Phong | 50.01.104.117 | Bài nhóm 3.1: rủi ro dự án, xếp hạng, HeatMap | Danh sách/chi tiết/sắp xếp, 20 ca, 5 unit test, 2 UI script |

Mỗi người làm độc lập trên cùng đặc tả và mẫu đã chốt, không phải chờ người khác gửi bài mới bắt đầu. Rà soát và ghép kết quả ở mốc chung. Đại phụ trách hàm tổng tiền, Ngân hàm subtotal, Như hàm validation; Chương và Phong hỗ trợ ca đơn vị, CFG và CI. Phân công tiểu luận là đề xuất của kế hoạch nháp, nhóm điều chỉnh khi triển khai.

## 9. Lịch trình và ước lượng

Chưa có ngày học cụ thể của Buổi 10, nên dùng mốc học phần thay vì tự đặt ngày lịch.

| Mốc | Sản phẩm phải xong | Phụ trách |
|---|---|---|
| Trước Buổi 4 | Phiếu chính/dự phòng, kế hoạch nháp, README, bài nhóm Buổi 3 | Đại, Chương và từng người theo bảng |
| Buổi 4–6 | Đặc tả có phiên bản, bảng EP/BVA/quyết định/trạng thái, ca vòng 1, lỗi có bằng chứng nếu phát hiện | Cả nhóm theo chức năng |
| Buổi 7 | Kế hoạch cập nhật, đặc tả, ≥50/100 ca, RTM sơ bộ; nộp mốc tiến độ | Đại tổng hợp, từng người ≥10 ca |
| Buổi 7–8 | Hoàn thiện 100 ca và phân tích hộp trắng 3 hàm | Cả nhóm |
| Buổi 9 | ≥25 unit test, coverage, CI | Chương điều phối, mỗi người 5 test |
| Buổi 10 | ≥12 UI script, hồi quy, tổng kết, slide/video nháp | Cả nhóm |
| Ngày 1–5 sau Buổi 10 | Rà soát hồ sơ, hoàn thiện video 8–12 phút và minh chứng | Cả nhóm |
| Ngày 6 sau Buổi 10 | Kiểm tra link, gói nộp, dự phòng sửa lỗi tài liệu | Đại, Chương |
| 23:59 ngày thứ 7 sau Buổi 10 | Nộp toàn bộ hồ sơ cuối kỳ theo hướng dẫn | Đại đại diện nhóm |

Ước lượng công sức cả nhóm cho 3 nhóm việc chính, đơn vị giờ-người; đây là dự kiến cần cập nhật sau khảo sát.

| Công việc | a | m | b | E = (a+4m+b)/6 | SD = (b−a)/6 |
|---|---:|---:|---:|---:|---:|
| Khảo sát, đặc tả, kế hoạch và thiết kế ca | 18 | 26 | 40 | 27,00 | 3,67 |
| Thực thi thủ công, minh chứng, lỗi và hồi quy | 20 | 32 | 50 | 33,00 | 5,00 |
| Hộp trắng, tự động hóa, báo cáo, slide/video | 28 | 42 | 68 | 44,00 | 6,67 |
| Tổng | | | | 104,00 | 9,10 nếu độc lập |

Tổng khoảng 104 ± 9,10 giờ-người theo giả định độc lập, không phải khoảng đảm bảo hay số giờ lịch. Cần theo dõi thực tế và điều chỉnh khi công việc phụ thuộc nhau.

## 10. Quản lý kết quả và bàn giao

Ca kiểm thử dùng mã SW-TC-xxx, rủi ro dùng Sxx/Pxx. Báo lỗi ghi môi trường, tiền điều kiện, dữ liệu giả, bước tái hiện, mong đợi/thực tế, mức độ nghiêm trọng và minh chứng. Không dùng ảnh lỗi của tài khoản/biến thể khác làm kết quả của tài khoản chuẩn.

Commit tài liệu và mã theo phần việc. Lưu Excel ở `docs/`, mã mô phỏng ở `src/`, test ở `tests/`, ảnh/log ở `evidence/`. Các thư mục này là cấu trúc dự kiến, chỉ tạo khi có nội dung thực. README hiện liên kết tới kế hoạch ở gốc kho.

Phụ lục AI lưu công cụ, ngày, prompt/bối cảnh, nội dung dùng/sửa/bỏ và phần do người học đánh giá. Bản hỗ trợ AI cần được nhóm đọc lại và xác nhận, không ghi nhận như đã tự thực hiện. Báo cáo đóng góp chỉ ghi công việc thực tế.

Nguồn lập kế hoạch: `Huong-dan-tieu-luan-COMP1307.pdf`, mục 1.2, 2, 3.3, 3.6 và bước 3–4; phiếu bài tập Buổi 3, Bài nhóm 3.2; phiếu đăng ký đề tài nhóm 6 đã điền. Chưa có thực nghiệm mới được thực hiện để xác nhận các rủi ro trong bản kế hoạch này.
