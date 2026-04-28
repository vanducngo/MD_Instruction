Tôi đã chuyển đổi mã LaTeX của bạn thành dạng bảng (Markdown) tương thích để bạn có thể copy và paste trực tiếp vào file Word một cách dễ dàng. 

Khi paste vào Word, bạn chỉ cần bôi đen bảng $\rightarrow$ chọn Insert $\rightarrow$ Table $\rightarrow$ **Convert Text to Table** (nếu cần), hoặc Word sẽ tự động nhận diện định dạng lưới này.

---

**Bảng 3.1: Phân tích thống kê cấp độ điểm ảnh (Mean và Standard Deviation) của tập NIH-14 và CIFAR dưới tác động của nhiễu ở mức độ nghiêm trọng 5.0.**

| Nhóm nhiễu (Group Type) | Loại nhiễu (Corruption Type) | NIH-14 (CXR) - Mean | NIH-14 (CXR) - Std | CIFAR-10 - Mean | CIFAR-10 - Std | CIFAR-100 - Mean | CIFAR-100 - Std |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Ảnh gốc (Clean Baseline)** | | *0.4885* | *0.2473* | *0.4766* | *0.2504* | *0.4794* | *0.2676* |
| **Độ sáng & Tương phản (Brightness & Contrast)** | Brightness | 0.8922 | 0.1562 | 0.6962 | 0.2333 | 0.6851 | 0.2498 |
| | Contrast | 0.4885 | 0.0950 | 0.4746 | 0.1391 | 0.4774 | 0.1654 |
| | Fog | 0.4949 | 0.1339 | 0.4712 | 0.1530 | 0.4733 | 0.1583 |
| **Nhiễu cộng gộp (Additive Noise)** | Shot Noise | 0.4883 | 0.5366 | 0.4717 | 0.2615 | 0.4732 | 0.2753 |
| | Impulse Noise | 0.4888 | 0.2655 | 0.4782 | 0.2755 | 0.4808 | 0.2901 |
| | Gaussian Noise | 0.4909 | 0.2594 | 0.4744 | 0.2628 | 0.4767 | 0.2766 |
| **Mờ ảnh (Blur Group)** | Zoom Blur | 0.3496 | 0.2738 | 0.4714 | 0.2318 | 0.4726 | 0.2470 |
| | Frost | 0.4207 | 0.1782 | 0.6372 | 0.2000 | 0.6410 | 0.2099 |
| | Defocus Blur | 0.4828 | 0.2421 | 0.4746 | 0.2339 | 0.4773 | 0.2524 |
| | Glass Blur | 0.4847 | 0.2392 | 0.4742 | 0.2450 | 0.4770 | 0.2620 |
| | Motion Blur | 0.4814 | 0.2385 | 0.4766 | 0.2328 | 0.4796 | 0.2511 |
| **Kỹ thuật số, Thời tiết & Hình thái (Digital, Weather & Morphological)** | Snow | 0.5249 | 0.2348 | 0.6797 | 0.2433 | 0.6770 | 0.2507 |
| | Elastic Transform | 0.4885 | 0.2468 | 0.4741 | 0.2402 | 0.4770 | 0.2580 |
| | Pixelate | 0.4874 | 0.2472 | 0.4780 | 0.2438 | 0.4808 | 0.2615 |
| | JPEG Compression | 0.4855 | 0.2695 | 0.4765 | 0.2485 | 0.4791 | 0.2647 |

---

*(Mẹo cho Word: Sau khi paste vào Word, bạn bôi đen toàn bộ bảng, vào thẻ **Table Design** $\rightarrow$ chọn một mẫu bảng có đường kẻ ngang mờ (như mẫu Light Shading) để bảng trông giống hệt như chuẩn trình bày của các bài báo khoa học quốc tế nhé).*
