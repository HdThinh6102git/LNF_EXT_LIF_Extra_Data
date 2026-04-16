# Hướng dẫn cài đặt thư viện ClosedXML trong UiPath Studio

Tài liệu này hướng dẫn bạn cách cài đặt thư viện Excel (**ClosedXML**) để xử lý các tệp Excel nâng cao trong UiPath.

## Bước 1: Mở trình quản lý gói (Manage Packages)
- Trên thanh công cụ của UiPath Studio, nhấn vào nút **Manage Packages** hoặc nhấn phím tắt `Ctrl + P`.

## Bước 2: Chọn nguồn gói NuGet
- Ở cột bên trái, hãy chọn mục **nuget.org**. 
- *Lưu ý: Nếu bạn chọn "All Packages", hãy đảm bảo rằng bộ lọc không giới hạn kết quả.*

## Bước 3: Tìm kiếm và Cài đặt
1. Nhập từ khóa `ClosedXML` vào ô tìm kiếm.
2. Nếu không thấy kết quả hiện ra (như hình bạn đã gặp), hãy kiểm tra biểu tượng **Filter** (hình cái phễu) ở bên phải ô tìm kiếm.
3. **Bỏ tích (Uncheck)** mục **UiPath Only**. Khi mục này được chọn, UiPath sẽ chỉ hiển thị các gói do chính họ phát hành.
4. Chọn gói `ClosedXML` từ danh sách kết quả (thường là bản có nhiều lượt tải nhất).
5. Nhấn nút **Install** ở bảng bên phải.
6. Nhấn nút **Save** ở góc dưới cùng bên phải cửa sổ.

## Bước 4: Chấp nhận các điều khoản
- Một cửa sổ xác nhận sẽ hiện ra, nhấn **I Accept** để hoàn tất việc tải và cài đặt thư viện vào dự án.

## Sau khi cài đặt thành công:
Đừng quên thêm **Namespace** để có thể sử dụng các hàm của thư viện trong code:
1. Mở tab **Imports** ở cạnh tab *Variables* và *Arguments*.
2. Nhập `ClosedXML.Excel` và nhấn Enter.

---
*Bây giờ bạn đã có thể sử dụng `ClosedXML.Excel.XLWorkbook` trong activity Invoke Code mà không gặp lỗi "Type not defined".*
