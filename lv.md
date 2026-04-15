Để viết Chương 2 đạt chuẩn luận văn Thạc sĩ (khoảng 20-30 trang cho toàn chương) và bám sát bài báo gốc của bạn làm xương sống, tôi sẽ triển khai chi tiết phần 2.1. 

Trong bài báo gốc của bạn, mô hình được xây dựng trên kiến trúc **ResNet-18** làm backbone, được khởi tạo bằng trọng số **ImageNet-1K** và thực hiện nhiệm vụ **phân loại đa nhãn** (Atelectasis, Cardiomegaly, Consolidation, Edema, Pleural Effusion). Chúng ta sẽ lấy đúng các chi tiết này làm "xương sống" để phóng tác và mở rộng lý thuyết.

Dưới đây là nội dung chi tiết cho **Mục 2.1**:

---

### **CHƯƠNG 2: CƠ SỞ LÝ THUYẾT VÀ TỔNG QUAN NGHIÊN CỨU**

#### **2.1. Phân loại bệnh lý X-quang ngực bằng Deep Learning**
Trong lĩnh vực chẩn đoán hình ảnh y tế, ảnh X-quang ngực (Chest X-ray - CXR) là một trong những công cụ phổ biến và quan trọng nhất để phát hiện các bệnh lý về lồng ngực. Tuy nhiên, việc đọc và phân tích ảnh đòi hỏi kiến thức chuyên môn sâu và tốn nhiều thời gian của các bác sĩ. Sự ra đời của Học sâu (Deep Learning) đã mở ra một kỷ nguyên mới, cho phép tự động hóa quá trình trích xuất đặc trưng và phân loại các tổn thương bệnh lý trên ảnh CXR với độ chính xác cao.

##### **2.1.1. Kiến trúc Convolutional Neural Networks (CNNs)**
Mạng thần kinh tích chập (CNN) là kiến trúc cốt lõi đứng sau hầu hết các hệ thống thị giác máy tính hiện đại, đặc biệt hiệu quả trong xử lý dữ liệu dạng lưới như hình ảnh y tế. Thay vì sử dụng các đặc trưng thủ công (hand-crafted features) dễ bị sai số và phụ thuộc vào người thiết kế, CNN tự động học cách trích xuất các đặc trưng từ mức độ thấp (như cạnh, góc) đến mức độ cao (như hình dạng của khối u hay vùng đông đặc phổi) thông qua các lớp tích chập.

Một mạng CNN tiêu chuẩn bao gồm các thành phần chính:
*   **Lớp tích chập (Convolutional Layer):** Sử dụng các bộ lọc (filters/kernels) trượt trên ảnh để tạo ra các bản đồ đặc trưng (feature maps). Phép toán này giúp giữ lại tính chất không gian cục bộ của các điểm ảnh.
*   **Lớp kích hoạt (Activation Layer):** Thường sử dụng hàm ReLU $f(x) = \max(0, x)$ để đưa tính phi tuyến vào mô hình, giúp mạng học được các cấu trúc phức tạp.
*   **Lớp gộp (Pooling Layer):** (Ví dụ: Max Pooling, Average Pooling) giúp giảm kích thước chiều không gian của bản đồ đặc trưng, từ đó giảm số lượng tham số tính toán và hạn chế hiện tượng quá khớp (overfitting).

Trong bài toán phân tích ảnh X-quang ngực, các mạng CNN đã chứng minh được khả năng vượt trội so với các phương pháp truyền thống nhờ khả năng xử lý các biến đổi phức tạp về cường độ sáng và cấu trúc giải phẫu học của cơ thể người.

##### **2.1.2. Kiến trúc ResNet-18 và các biến thể backbone**
Trong bài báo gốc phục vụ nghiên cứu này, kiến trúc **ResNet-18** được lựa chọn làm mạng xương sống (backbone) để trích xuất đặc trưng từ ảnh X-quang ngực. 

**Mạng ResNet (Residual Network):**
Trước khi ResNet ra đời, việc tăng độ sâu của mạng (thêm nhiều lớp) thường dẫn đến hiện tượng tiêu biến đạo hàm (vanishing gradient), làm cho hiệu năng của mạng bị giảm sút. ResNet giải quyết vấn đề này bằng cách giới thiệu cấu trúc "kết nối tắt" (skip connection) hay khối phần dư (Residual Block). Thay vì cố gắng học trực tiếp một ánh xạ $H(x)$, khối phần dư cố gắng học hàm $F(x) = H(x) - x$, từ đó ánh xạ gốc trở thành $H(x) = F(x) + x$. Điều này giúp dòng đạo hàm có thể truyền ngược trực tiếp về các lớp phía trước mà không bị tiêu biến.

**Tại sao lại là ResNet-18 trong nghiên cứu này?**
*   **Tính cân bằng giữa hiệu năng và tài nguyên:** So với các mạng sâu hơn như ResNet-50 hay ResNet-101, ResNet-18 có số lượng tham số nhỏ hơn nhiều (khoảng 11 triệu tham số), giúp quá trình thích nghi tại thời điểm kiểm thử (Test-Time Adaptation) diễn ra nhanh chóng, phù hợp với dòng dữ liệu y tế trực tuyến.
*   **Khai thác trọng số tiền huấn luyện (Transfer Learning):** Như đã đề cập trong phương pháp của bài báo, mô hình backbone được khởi tạo bằng bộ trọng số được huấn luyện trước trên tập dữ liệu **ImageNet-1K** [Deng et al., 2009]. Việc này giúp mô hình thừa hưởng khả năng nhận diện các đặc trưng thị giác cơ bản (cạnh, khối) từ hàng triệu ảnh tự nhiên trước khi được tinh chỉnh (fine-tune) trên tập dữ liệu chuyên biệt CheXpert.

Ngoài ResNet, các biến thể backbone khác cũng thường được sử dụng trong bài toán này bao gồm **DenseNet-121** (kiến trúc được sử dụng trong bài báo kinh điển CheXNet [Rajpurkar et al., 2017]). DenseNet kết nối mỗi lớp với tất cả các lớp phía sau nó, giúp tối ưu hóa luồng thông tin tốt hơn nhưng đòi hỏi bộ nhớ GPU lớn hơn khi xử lý TTA.

##### **2.1.3. Bài toán phân loại đa nhãn (Multi-label classification) trong y tế**
Khác biệt lớn nhất giữa bài toán phân loại ảnh thông thường và phân tích ảnh X-quang ngực nằm ở bản chất của nhãn dữ liệu. Trong ảnh tự nhiên (như ImageNet), một bức ảnh thường chỉ chứa một đối tượng chính (đơn nhãn - single-label). Tuy nhiên, trên một tấm phim X-quang ngực, một bệnh nhân có thể cùng lúc mắc nhiều bệnh lý khác nhau (đồng xuất hiện - co-occurring pathologies).

Như được định nghĩa trong bài báo gốc, mô hình cần dự đoán đồng thời sự hiện diện của 5 bệnh lý: **Atelectasis (Xẹp phổi), Cardiomegaly (Tim to), Consolidation (Đông đặc), Edema (Phù phổi), và Pleural Effusion (Tràn dịch màng phổi)**. 

Những thách thức kỹ thuật và giải pháp trong bài toán đa nhãn y tế bao gồm:
*   **Từ Softmax sang độc lập Sigmoid:** Trong bài toán đơn nhãn, hàm Softmax được dùng ở lớp cuối cùng để tạo ra một phân phối xác suất có tổng bằng 1. Đối với bài toán đa nhãn của nghiên cứu này, lớp Softmax được thay thế bằng hàm **Sigmoid** độc lập cho từng đầu ra của mảng 5 bệnh lý. Xác suất của mỗi bệnh lý $c$ được tính độc lập bằng công thức: $p_c = \sigma(z_c) = \frac{1}{1 + e^{-z_c}}$.
*   **Hàm mất mát Binary Cross-Entropy (BCE):** Để tối ưu hóa độc lập cho từng bệnh lý, hàm mất mát BCE được áp dụng thay cho Cross-Entropy thông thường, cho phép mô hình học cách nhận biết một hoặc nhiều bệnh lý cùng xuất hiện trên một bệnh nhân một cách chính xác.

---

### **Đánh giá mức độ bám sát bài báo gốc:**
*   Phần **2.1.2** đã trích dẫn đúng việc dùng ResNet-18 và ImageNet-1K weights từ phần *3.2 Source Model* của bài báo.
*   Phần **2.1.3** đã trích dẫn đúng 5 loại bệnh lý bạn dùng và việc chuyển từ hàm mục tiêu softmax (mặc định của các phương pháp TTA gốc) sang sigmoid và BCE loss (từ phần *3.3 Test-Time Adaptation Methods* của bài báo).

**Bước tiếp theo:**
Chúng ta sẽ triển khai tiếp mục **2.2: Vấn đề Domain Shift trong chẩn đoán hình ảnh**. Phần này sẽ phân tích sâu về lý do tại sao mô hình bị rớt đỉnh khi chuyển từ CheXpert sang NIH-14 (dẫn chứng từ bảng 2 trong bài báo của bạn).

Bạn có muốn tôi tiến hành viết tiếp mục 2.2 luôn không?
