# Hướng dẫn sửa lỗi trong UiPath Studio

Dưới đây là các bước để bạn tự sửa lỗi trực tiếp trên giao diện UiPath:

### 1. Cài đặt Package ClosedXML
Lỗi `Type 'ClosedXML.Excel.XLWorkbook' is not defined` xảy ra do thiếu thư viện.
- Mở **Manage Packages** (Ctrl + P).
- Chọn tab **All Packages**.
- Tìm kiếm `ClosedXML` và cài đặt bản mới nhất.
- Nhấn **Save**.

### 2. Thêm Namespace (Imports)
- Ở bảng bên dưới, chọn tab **Imports**.
- Nhập `ClosedXML.Excel` và nhấn Enter để thêm vào.

### 3. Cấu hình Arguments cho Invoke Code
Lỗi `'LNF_EXT_LIF_download_file' is not declared` là do biến chưa được truyền vào code.
- Chọn activity **Invoke Code**.
- Trong bảng **Properties**, nhấn vào nút **Edit Arguments**.
- Thêm 2 dòng sau:
    - Name: `LNF_EXT_LIF_download_file` | Direction: `In` | Type: `String` | Value: `LNF_EXT_LIF_download_file`
    - Name: `LNF_EXT_LIF_data_table` | Direction: `Out` | Type: `DataTable` | Value: `LNF_EXT_LIF_data_table`

### 4. Sửa code để tránh lỗi Late Binding
Thay thế code cũ trong **Invoke Code** bằng đoạn code dưới đây:

```vbnet
Dim dt As New DataTable()
dt.Columns.Add("Rule", GetType(String))
dt.Columns.Add("Search Data", GetType(String))
dt.Columns.Add("Change Column Name", GetType(String))
dt.Columns.Add("Before Column Data", GetType(String))
dt.Columns.Add("After Column Data", GetType(String))
dt.Columns.Add("Required Action", GetType(String))

Using workbook As New ClosedXML.Excel.XLWorkbook(LNF_EXT_LIF_download_file)
    Dim worksheet As ClosedXML.Excel.IXLWorksheet = workbook.Worksheet(1)
    Dim rows = worksheet.RowsUsed()
    
    For Each row As ClosedXML.Excel.IXLRow In rows.Skip(1)
        Dim valYuJi As String = row.Cell(40).Value.ToString().Trim() ' Column AN
        If valYuJi = "000" Then
            Dim valKeYak As String = row.Cell(14).Value.ToString().Trim() ' Column N
            dt.Rows.Add("2", valKeYak, "", "", "", "NOA")
        End If
    Next
End Using

LNF_EXT_LIF_data_table = dt
```
