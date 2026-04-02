**Bài 5**, chúng ta bước vào tư duy **"Chia để trị" (Divide and Conquer)**. Đây là kỹ năng quan trọng nhất để trở thành một lập trình viên chuyên nghiệp: **không bao giờ viết một chương trình quá dài trong hàm `main()`**. Chúng ta sẽ chia chương trình thành các phần nhỏ (Methods) để dễ quản lý, dễ kiểm thử và có thể tái sử dụng.

---

# BÀI TẬP 5: MÁY TÍNH BỎ TÚI (METHOD & CHIA ĐỂ TRỊ)

### 1. Đề bài
Viết chương trình máy tính thực hiện các phép tính cơ bản: Cộng, Trừ, Nhân, Chia.
*   **Yêu cầu:** 
    1.  Tạo 4 hàm riêng biệt: `cong(a, b)`, `tru(a, b)`, `nhan(a, b)`, `chia(a, b)`.
    2.  Hàm `chia(a, b)` phải kiểm tra mẫu số `b` có bằng 0 hay không.
    3.  Chương trình chính (`main`) sẽ gọi các hàm này để thực hiện tính toán.
    4.  Vẽ Pseudocode trước khi viết code Java.

---
<br />
<br />
<br />
<br />

<br />
<br />
<br />
<br />

<br />
<br />
<br />
<br />

### 2. Gợi ý hướng dẫn (Phân tích Logic)
*   **Tư duy:** 
    *   Hàm là một "cỗ máy" nhỏ: có Input (tham số đầu vào) và Output (giá trị trả về).
    *   Thay vì viết `c = a + b` ở trong `main`, ta hãy giao việc đó cho hàm `cong`. Nếu sau này muốn đổi công thức cộng, ta chỉ cần sửa đúng 1 chỗ trong hàm.

---

### 3. Pseudocode (Bản thiết kế logic)

```text
HÀM cong(a, b): TRẢ VỀ a + b
HÀM tru(a, b): TRẢ VỀ a - b
HÀM nhan(a, b): TRẢ VỀ a * b
HÀM chia(a, b):
    NẾU b == 0: TRẢ VỀ thông báo lỗi
    KHÁC: TRẢ VỀ a / b

CHƯƠNG TRÌNH CHÍNH (main):
    NHẬP a, b, phép tính (1: Cộng, 2: Trừ...)
    NẾU lựa chọn là 1: KẾT QUẢ = cong(a, b)
    ... (tương tự cho các phép tính khác)
    XUẤT KẾT QUẢ
```

---

### 4. Map từ Pseudocode sang Code Java

```java
import java.util.Scanner;

public class MayTinh {
    // Các hàm xử lý (Methods)
    public static double cong(double a, double b) { return a + b; }
    public static double tru(double a, double b) { return a - b; }
    public static double nhan(double a, double b) { return a * b; }
    public static double chia(double a, double b) {
        if (b == 0) {
            System.out.println("Lỗi: Không thể chia cho 0");
            return 0; // Giá trị mặc định
        }
        return a / b;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Nhập liệu và gọi hàm tương ứng
        System.out.print("Nhập a: "); double a = sc.nextDouble();
        System.out.print("Nhập b: "); double b = sc.nextDouble();
        
        System.out.println("Kết quả cộng: " + cong(a, b));
        System.out.println("Kết quả chia: " + chia(a, b));
    }
}
```

---

### 5. Câu hỏi triển tư duy
1.  **Câu hỏi về Phạm vi (Scope):** "Nếu thầy khai báo biến `int a` bên trong hàm `cong`, liệu trong hàm `main` thầy có thể dùng biến `a` đó không?" (Đây là bài học về phạm vi của biến - Variable Scope).
2.  **Câu hỏi về Tái sử dụng:** "Tại sao chúng ta nên tách code ra thành hàm thay vì viết hết trong `main`?" (Gợi ý: Dễ đọc, dễ test lỗi, và nếu cần làm máy tính khoa học phức tạp hơn, ta chỉ cần thêm hàm mới).
3.  **Câu hỏi về Lập trình phòng thủ (Defensive Programming):** "Trong hàm `chia`, thay vì trả về `0`, làm thế nào để thông báo cho người dùng biết là họ đã nhập sai?" (Gợi ý: Giới thiệu khái niệm `throw exception` ở mức độ cơ bản).

---
