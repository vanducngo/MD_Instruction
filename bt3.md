**Bài 3**, chúng ta sẽ chuyển sang tư duy về **sự lặp lại (Iteration)**.

---

# BÀI TẬP 3: TÍNH GIAI THỪA CỦA N (N!)

### 1. Đề bài
Nhập vào một số nguyên dương `N` từ bàn phím. Hãy tính giá trị của `N!` (N giai thừa).
*   **Định nghĩa:** `N! = 1 * 2 * 3 * ... * N`.
*   **Yêu cầu:** 
    *   Phải sử dụng cấu trúc vòng lặp (`for` hoặc `while`).
    *   Xử lý trường hợp nếu người dùng nhập `N < 0` (giai thừa không xác định với số âm).
    *   Vẽ Pseudocode trước khi viết code.

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
    *   Để tính tích của các số, ta cần một "biến tích lũy" (accumulator).
    *   **Biến cần có:** `N` (số đầu vào), `ketQua` (kết quả), `i` (biến đếm của vòng lặp).
*   **Lưu ý:** `ketQua` phải khởi tạo bằng `1`, không được là `0` (vì bất cứ số nào nhân với 0 cũng bằng 0).

---

### 3. Pseudocode (Bản thiết kế logic)

```text
BẮT ĐẦU
    NHẬP N
    
    NẾU N < 0:
        XUẤT "Không tính được giai thừa số âm"
    KHÁC:
        ketQua = 1
        CHO i TỪ 1 ĐẾN N:
            ketQua = ketQua * i
        XUẤT "Kết quả của N! là: " + ketQua
KẾT THÚC
```

---

### 4. Map từ Pseudocode sang Code Java

```java
import java.util.Scanner;

public class TinhGiaiThua {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        System.out.print("Nhập N: ");
        int n = sc.nextInt();
        
        if (n < 0) {
            System.out.println("Không tính được giai thừa số âm.");
        } else {
            long ketQua = 1; // Dùng long để tránh tràn số khi N lớn
            for (int i = 1; i <= n; i++) {
                ketQua = ketQua * i;
            }
            System.out.println(n + "! = " + ketQua);
        }
    }
}
```

---

### 5. Câu hỏi phát triển tư duy

1.  **Câu hỏi về kiểu dữ liệu:** "Tại sao thầy đổi từ `int ketQua` sang `long ketQua`?" (Gợi ý: `int` có giới hạn tối đa khoảng 2 tỷ. Giai thừa tăng rất nhanh, thử tính 13! xem kết quả là bao nhiêu?).
2.  **Câu hỏi về tối ưu:** "Nếu anh nhập `N = 0`, chương trình chạy thế nào?" (Giai thừa của 0 là 1. Code của em có xử lý được không? Đây là **Boundary Testing** - kiểm tra các giá trị biên).
3.  **Câu hỏi về vòng lặp:** "Em có thể dùng vòng lặp `while` thay cho `for` không?" (Gợi ý: Cho sinh viên tự viết lại code bằng `while` để hiểu sự tương đồng của hai cấu trúc).
4.  **Tư duy thuật toán:** "Nếu đề bài yêu cầu tính tổng `1 + 2 + 3 + ... + N` thay vì tích, em chỉ cần thay đổi dòng code nào?"

---
