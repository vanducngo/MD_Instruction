**Bài 4**, chúng ta bắt đầu làm việc với **cấu trúc dữ liệu**. Thay vì chỉ lưu trữ một giá trị đơn lẻ (như số tiền lương, số giờ làm), bây giờ chúng ta cần quản lý một **danh sách** các phần tử. Đây là bước ngoặt để hiểu về **Bộ nhớ (Memory)** và **Chỉ số (Index)**.

---

# BÀI TẬP 4: THỐNG KÊ ĐIỂM SỐ (ARRAY)

### 1. Đề bài
Nhập vào danh sách điểm số của `N` học sinh (số `N` do người dùng nhập từ bàn phím). 
*   **Yêu cầu:** 
    1.  Cho người dùng nhập `N`, sau đó nhập lần lượt điểm của `N` học sinh đó vào mảng.
    2.  Tìm và in ra: **Điểm cao nhất**, **Điểm thấp nhất**, và **Điểm trung bình cộng** của cả lớp.
    3.  Vẽ Pseudocode trước khi viết code Java.

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

### 2. Gợi ý
*   **Tư duy:** 
    *   Mảng trong Java bắt đầu từ chỉ số 0.
    *   Để tìm Max/Min, hãy **giả định** phần tử đầu tiên (`arr[0]`) là Max/Min, sau đó so sánh với các phần tử còn lại. Nếu thấy phần tử nào lớn hơn Max thì gán nó vào Max.
    *   Để tính trung bình, ta cần một biến `tong` để cộng dồn tất cả các điểm, sau đó chia cho `N`.

---

### 3. Pseudocode (Bản thiết kế logic)

```text
BẮT ĐẦU
    NHẬP N
    KHỞI TẠO Mảng diem với kích thước N
    
    CHO i TỪ 0 ĐẾN N-1:
        NHẬP diem[i]
        
    // Tìm Max, Min và Tổng
    max = diem[0], min = diem[0], tong = 0
    CHO i TỪ 0 ĐẾN N-1:
        NẾU diem[i] > max: max = diem[i]
        NẾU diem[i] < min: min = diem[i]
        tong = tong + diem[i]
        
    XUẤT "Max: " + max
    XUẤT "Min: " + min
    XUẤT "Trung bình: " + (tong / N)
KẾT THÚC
```

---

### 4. Map từ Pseudocode sang Code Java

```java
import java.util.Scanner;

public class ThongKeDiem {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Nhập số lượng học sinh: ");
        int n = sc.nextInt();
        
        double[] diem = new double[n]; // Khởi tạo mảng
        
        // Nhập liệu vào mảng
        for (int i = 0; i < n; i++) {
            System.out.print("Nhập điểm học sinh thứ " + (i + 1) + ": ");
            diem[i] = sc.nextDouble();
        }
        
        // Xử lý dữ liệu
        double max = diem[0];
        double min = diem[0];
        double tong = 0;
        
        for (int i = 0; i < n; i++) {
            if (diem[i] > max) max = diem[i];
            if (diem[i] < min) min = diem[i];
            tong += diem[i];
        }
        
        System.out.println("Điểm cao nhất: " + max);
        System.out.println("Điểm thấp nhất: " + min);
        System.out.println("Điểm trung bình: " + (tong / n));
    }
}
```

---

### 5. Câu hỏi phát triển tư duy
1.  **Câu hỏi về Chỉ số (Index):** "Điều gì xảy ra nếu em cố tình truy cập `diem[n]` trong khi mảng chỉ có `n` phần tử (từ 0 đến n-1)?" (Gợi ý: Đây là lỗi kinh điển `ArrayIndexOutOfBoundsException`).
2.  **Câu hỏi về Logic:** "Nếu thầy muốn đếm xem có bao nhiêu học sinh **đạt loại giỏi** (điểm >= 8.0) trong danh sách vừa nhập, em sẽ thêm vòng lặp nào?" (Giúp họ làm quen với việc **"duyệt và đếm"**).
3.  **Câu hỏi về Cấu trúc:** "Tại sao chúng ta phải dùng Mảng thay vì tạo ra N biến `diem1, diem2, ..., diemN`?" (Câu hỏi này giúp sinh viên thấy được sức mạnh của việc quản lý dữ liệu số lượng lớn).
