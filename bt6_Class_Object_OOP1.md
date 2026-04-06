
# 🚀 BÀI TẬP LỚN: HỆ THỐNG QUẢN LÝ SINH VIÊN & PHƯƠNG TIỆN (OOP ADVANCED)

### 🎯 Mục tiêu bài học
Thông qua bài tập này, bạn sẽ làm chủ các kiến thức trọng tâm của Lập trình hướng đối tượng (OOP):
*   **Encapsulation (Đóng gói):** Bảo vệ dữ liệu bằng `private` và `getter/setter`.
*   **Constructor Overloading:** Đa dạng hóa cách khởi tạo đối tượng.
*   **Static Keyword:** Quản lý dữ liệu chung của toàn bộ lớp (bộ đếm).
*   **Object Relationship:** Cách các đối tượng liên kết và chứa nhau (`Xe` nằm trong `SinhVien`, `SinhVien` nằm trong `TruongHoc`).
*   **Variable Scope:** Phân biệt biến cục bộ (local) và biến thuộc tính (instance).

---

### 🏗 CẤU TRÚC HỆ THỐNG
Hệ thống gồm 4 lớp chính:
1.  **Xe:** Quản lý thông tin phương tiện.
2.  **SinhVien:** Quản lý thông tin cá nhân và xe của sinh viên.
3.  **TruongHoc:** Quản lý danh sách sinh viên.
4.  **Main:** Điều hành luồng hoạt động của chương trình.

---

### 1️⃣ Lớp Xe (Quản lý tài sản)
Lớp này giúp bạn luyện tập về **static** và **encapsulation**.

*   **Thuộc tính:**
    *   `private String hangXe`, `private String mauSac`
    *   `private static int soLuongXe`: Biến dùng để đếm tổng số xe đã được tạo ra trong hệ thống.
*   **Yêu cầu:**
    *   **Constructor:** Mỗi khi một đối tượng `Xe` được tạo ra, hãy tăng biến `soLuongXe` lên 1.
    *   **Getter/Setter:** Đầy đủ cho các thuộc tính private.
    *   **Method:** `public static void hienThiSoLuongXe()` để in ra tổng số xe hiện có.

### 2️⃣ Lớp SinhVien (Thành phần cốt lõi)
Lớp này giúp bạn luyện tập về **Constructor Overloading** và **this keyword**.

*   **Thuộc tính:**
    *   `private String maSV`, `String ten`, `int tuoi`
    *   `private Xe xe`: (Đây là mối quan hệ Has-A: Sinh viên sở hữu một chiếc xe).
*   **Yêu cầu:**
    *   **Constructor 1:** Không tham số (gán giá trị mặc định).
    *   **Constructor 2:** Đầy đủ tham số (Sử dụng `this` để phân biệt biến tham số và biến thuộc tính).
    *   **Getter/Setter:** Đầy đủ cho tất cả thuộc tính.
    *   **Method:** `public void hienThiThongTin()`
        *   In ra thông tin cá nhân.
        *   Nếu sinh viên có xe, in thông tin xe. Nếu không, in "Chưa có xe".

### 3️⃣ Lớp TruongHoc (Quản lý tổng thể)
Lớp này giúp bạn luyện tập về **Array Object**, **Variable Scope** và **Method Overloading**.

*   **Thuộc tính:**
    *   `private String tenTruong`
    *   `private SinhVien[] danhSach`: Mảng chứa các đối tượng sinh viên.
    *   `private int soLuongSVHienTai`: Biến dùng để quản lý chỉ số mảng.
*   **Yêu cầu:**
    *   **Constructor:** Nhận vào tên trường và khởi tạo mảng `danhSach` có kích thước 10.
    *   **Method Overloading (Nâng cao):**
        *   `public void themSinhVien(SinhVien sv)`: Nhận vào một đối tượng SV đã có sẵn.
        *   `public void themSinhVien(String ma, String ten, int tuoi)`: Tự tạo một đối tượng SV mới bên trong method rồi thêm vào mảng.
    *   **Logic bổ sung:** Trong method `themSinhVien`, hãy khai báo một biến cục bộ `int index` để xác định vị trí cần thêm (để luyện tập về **Variable Scope**).
    *   **Method:** `public void hienThiDanhSach()`: Duyệt mảng và gọi hàm hiển thị của từng sinh viên.

### 4️⃣ Lớp Main (Chạy chương trình)
Bạn hãy viết code trong hàm `main` theo kịch bản sau:

1.  **Khởi tạo xe:** Tạo 2 đối tượng `Xe` (ví dụ: Honda - Đen, Yamaha - Trắng).
2.  **Khởi tạo sinh viên:** 
    *   SV1: Tạo bằng constructor đầy đủ tham số, gán xe thứ nhất.
    *   SV2: Tạo bằng constructor không tham số, sau đó dùng `setter` để gán giá trị và gán xe thứ hai.
3.  **Khởi tạo trường học:** Đặt tên là "Đại học Bách Khoa".
4.  **Thực thi:**
    *   Thêm SV1 và SV2 vào trường học bằng 2 phương thức `themSinhVien` khác nhau.
    *   Gọi hàm `hienThiDanhSach()` của trường học.
    *   Gọi hàm `Xe.hienThiSoLuongXe()` để kiểm tra biến static.

---

### 🚩 CÁC QUY TẮC BẮT BUỘC
1.  **Tính đóng gói:** Tất cả thuộc tính phải là `private`. Không được truy cập trực tiếp kiểu `sv.ten = "An"`.
2.  **Từ khóa this:** Bắt buộc dùng trong Constructor và Setter.
3.  **Variable Scope:** Giải thích được sự khác nhau giữa biến `danhSach` (instance) và biến `index` (local) trong lớp `TruongHoc`.
4.  **Static:** Biến `soLuongXe` phải được gọi thông qua tên lớp `Xe.hienThiSoLuongXe()`, không gọi qua đối tượng.

---

### 🎁 OUTPUT MONG ĐỢI
```text
Trường: Đại học Bách Khoa
------------------------------
Mã SV: SV001 | Tên: Nguyễn Văn An | Tuổi: 20
Xe: Honda (Màu: Đen)

Mã SV: SV002 | Tên: Trần Thị Bình | Tuổi: 21
Xe: Yamaha (Màu: Trắng)
------------------------------
=> Tổng số xe đang quản lý trong hệ thống: 2
```

---
