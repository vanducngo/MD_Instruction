**Bài 2** sẽ nâng cấp tư duy từ "tính toán thẳng" sang **"quản lý nhiều trường hợp (Multiple Branches)"**.

---

# BÀI TẬP 2: GIẢI PHƯƠNG TRÌNH BẬC NHẤT (ax + b = 0)

### 1. Đề bài
Viết chương trình nhập vào hai số thực `a` và `b`. Tìm nghiệm của phương trình bậc nhất `ax + b = 0`.
*   **Yêu cầu:** 
    *   Xét tất cả các trường hợp có thể xảy ra của `a` và `b` (Vô nghiệm, Vô số nghiệm, Một nghiệm duy nhất).
    *   Luôn vẽ Pseudocode trước khi viết code Java.

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

### 2. Gợi y
*   **Bước 1: Xác định biến:** `a`, `b` (kiểu `double`).
*   **Bước 2: Phân tích các tình huống (Case analysis):**
    *   Nếu `a = 0`:
        *   Nếu `b = 0`: Phương trình trở thành `0 = 0` (Luôn đúng với mọi x) -> Vô số nghiệm.
        *   Nếu `b != 0`: Phương trình trở thành `0 = -b` (Vô lý) -> Vô nghiệm.
    *   Nếu `a != 0`:
        *   Nghiệm của phương trình là `x = -b / a`.

---

### 3. Pseudocode (Bản thiết kế logic)

```text
BẮT ĐẦU
    NHẬP a, b
    
    NẾU a BẰNG 0:
        NẾU b BẰNG 0:
            XUẤT "Phương trình vô số nghiệm"
        KHÁC (tức b khác 0):
            XUẤT "Phương trình vô nghiệm"
    KHÁC (tức a khác 0):
        x = -b / a
        XUẤT "Nghiệm của phương trình là: " + x
KẾT THÚC
```

---

### 4. Map từ Pseudocode sang Code Java

```java
import java.util.Scanner;

public class GiaiPhuongTrinh {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        System.out.print("Nhập a: ");
        double a = sc.nextDouble();
        System.out.print("Nhập b: ");
        double b = sc.nextDouble();
        
        // Map trực tiếp từ pseudocode
        if (a == 0) {
            if (b == 0) {
                System.out.println("Phương trình vô số nghiệm.");
            } else {
                System.out.println("Phương trình vô nghiệm.");
            }
        } else {
            double x = -b / a;
            System.out.println("Nghiệm là x = " + x);
        }
    }
}
```

---

### 5. Câu hỏi phát triển tư duy

1.  **Câu hỏi về làm tròn:** "Nếu kết quả là 1/3, màn hình in ra `0.33333333333`. Làm thế nào để chỉ lấy 2 chữ số thập phân?" (Gợi ý: Tìm hiểu `System.out.printf("%.2f", x)`).
2.  **Câu hỏi về Logic:** "Có bao nhiêu cách để viết lại đoạn `if-else` này mà vẫn cho ra kết quả đúng?" (Gợi ý: Cho họ thử dùng `switch-case` hoặc cấu trúc `if` khác thứ tự để thấy sự linh hoạt).
3.  **Câu hỏi thực tế:** "Nếu bài toán thay đổi thành `ax^2 + bx + c = 0` (Phương trình bậc 2), em sẽ vẽ Pseudocode như thế nào?" (Đây là cách để họ làm quen với tư duy **mở rộng vấn đề** - bài tập quan trọng nhất để trở thành lập trình viên giỏi).

---
