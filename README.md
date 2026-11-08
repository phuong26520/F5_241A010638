Lab F5 - Danh sách và lưới trong Flutter - Danh sách sản phẩm và Album ảnh

Thông tin sinh viên: Nguyễn Hoài Phương - MSSV 241A010638 - Lớp LTTTBDD - Môn INT4211.

Mô tả ngắn gọn

App có 2 tab chuyển qua lại bằng NavigationBar: tab Danh sách dùng ListView.builder để hiển thị sản phẩm bằng Card và ListTile, có thêm sản phẩm và vuốt sang trái bằng Dismissible để xóa; tab Lưới dùng GridView.builder hiển thị album ảnh 2 cột.

Cấu trúc chính

lib/main.dart: mã nguồn chính của ứng dụng.
assets/images/: 6 ảnh sản phẩm từ p1.jpg đến p6.jpg.
test/widget_test.dart: kiểm tra hiển thị danh sách, thêm mới, tìm kiếm và chuyển sang lưới.
pubspec.yaml: thông tin project và khai báo thư mục assets/images/.

Các chức năng đã làm

- Hiển thị danh sách sản phẩm bằng ListView.builder.
- Tách model SanPham riêng và định dạng giá tiền.
- Hiển thị mỗi dòng bằng Card và ListTile, cắt chữ dài bằng dấu ba chấm.
- Thêm sản phẩm mới lên đầu danh sách bằng nút +.
- Vuốt xóa sản phẩm bằng Dismissible và hiện thông báo khi danh sách trống.
- Hiển thị lưới ảnh 2 cột bằng GridView.builder và nạp ảnh từ assets.

Bài nâng cao đã làm

NC1 - Tìm kiếm sản phẩm theo tên

Bài yêu cầu thêm thanh tìm kiếm để lọc danh sách ngay khi đang gõ. Mình thêm biến _tuKhoa trong _ProductListTabState và đặt một TextField ở phía trên ListView.builder. Vì TextField và ListView.builder nằm chung trong một Column nên ListView.builder được bọc trong Expanded để không bị lỗi chiều cao.

Khi người dùng nhập từ khóa, hàm onChanged gọi setState cập nhật _tuKhoa. Danh sách hiển thị dsHienThi được lọc từ danh sách gốc _ds bằng where((sp) => sp.ten.toLowerCase().contains(_tuKhoa.trim().toLowerCase())).toList() rồi đưa vào ListView.builder. Nhờ giữ riêng _ds nên khi xóa từ khóa thì toàn bộ sản phẩm hiện lại.

NC3 - Hoàn tác sau khi xóa

Bài yêu cầu hiện SnackBar có nút Hoàn tác sau khi vuốt xóa để chèn lại sản phẩm về đúng chỗ cũ. Trong onDismissed của Dismissible, trước khi xóa khỏi _ds, chương trình lưu lại sản phẩm sp và vị trí viTriGoc = _ds.indexOf(sp), rồi mới gọi setState(() => _ds.removeAt(viTriGoc)).

Sau đó chương trình hiện SnackBar kèm SnackBarAction có nhãn Hoàn tác. Khi bấm Hoàn tác, callback gọi setState(() => _ds.insert(viTriGoc, sp)) để đưa sản phẩm vừa xóa trở lại đúng vị trí ban đầu.

Cách chạy

Chạy flutter pub get, sau đó chạy flutter run. Có thể dùng flutter analyze để kiểm tra lỗi.
