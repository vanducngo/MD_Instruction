Tuyệt vời! Dưới đây là hướng dẫn chi tiết cách cài đặt và chạy inference (testing) cho project LLaMP dựa trên thông tin từ repository GitHub bạn cung cấp.

**Tổng quan các bước:**

1.  **Cài đặt môi trường:** Tạo môi trường Conda và cài đặt các thư viện cần thiết.
2.  **Chuẩn bị dữ liệu:** Tải và sắp xếp dữ liệu cho dataset bạn muốn test (ví dụ: Caltech101, ImageNet).
3.  **Tải mô hình đã huấn luyện (Pretrained Models):** Tải checkpoint của LLaMP.
4.  **Chạy Inference/Testing:** Sử dụng các script được cung cấp để đánh giá mô hình.

---

**Bước 1: Cài đặt môi trường**

1.  **Clone repository:**
    ```bash
    git clone https://github.com/zhaohengz/LLaMP.git
    cd LLaMP
    ```

2.  **Tạo và kích hoạt môi trường Conda:**
    Repository cung cấp file `environment.yml`.
    ```bash
    conda env create -f environment.yml
    conda activate llamp
    ```
    *Lưu ý:* File `environment.yml` chỉ định `pytorch=1.12.1`, `torchvision=0.13.1` và `cudatoolkit=11.3`. Hãy đảm bảo driver NVIDIA của bạn tương thích. Nếu bạn có phiên bản CUDA khác, bạn có thể cần điều chỉnh file `environment.yml` hoặc cài đặt PyTorch riêng biệt phù hợp với CUDA của bạn.

3.  **Cài đặt các gói phụ thuộc khác:**
    Repository yêu cầu cài đặt thêm `clip` và `open_clip_torch`.
    ```bash
    pip install git+https://github.com/openai/CLIP.git
    pip install open_clip_torch
    ```
    (Có thể bạn cần `pip install open-clip-torch` tùy thuộc vào phiên bản pip và cách package được publish). Kiểm tra kỹ tên package nếu có lỗi.

---

**Bước 2: Chuẩn bị dữ liệu**

1.  **Tạo thư mục dữ liệu:**
    Bạn cần một thư mục gốc để chứa tất cả các dataset. Ví dụ, tạo thư mục `data` bên ngoài thư mục `LLaMP`:
    ```bash
    cd .. # Ra ngoài thư mục LLaMP
    mkdir data
    export DATA_ROOT=$(pwd)/data # Hoặc đặt DATA_ROOT là đường dẫn tuyệt đối đến thư mục data của bạn
    cd LLaMP # Quay lại thư mục LLaMP
    ```
    *Quan trọng:* Đường dẫn `DATA_ROOT` này sẽ được sử dụng trong các script chạy.

2.  **Tải và tổ chức dataset:**
    *   Thông tin chi tiết về cách tổ chức dữ liệu cho từng dataset có trong file `DATA.md` của repository.
    *   **Ví dụ với Caltech101 (một dataset nhỏ, dễ test):**
        *   Tải `101_ObjectCategories.tar.gz` từ [trang web Caltech101](http://www.vision.caltech.edu/Image_Datasets/Caltech101/).
        *   Giải nén và đặt vào thư mục `DATA_ROOT` theo cấu trúc:
            ```
            $DATA_ROOT/
                caltech-101/
                    101_ObjectCategories/
                        accordion/
                        airplanes/
                        ...
                    BACKGROUND_Google/
            ```
        *   Bạn có thể cần tạo symlink hoặc di chuyển thư mục cho đúng tên:
            ```bash
            mkdir -p $DATA_ROOT/caltech-101
            # Giả sử bạn đã tải và giải nén 101_ObjectCategories.tar.gz vào $DATA_ROOT/caltech-101/
            # cd $DATA_ROOT/caltech-101
            # tar -zxvf 101_ObjectCategories.tar.gz
            # mv 101_ObjectCategories/* .
            # rm -rf 101_ObjectCategories
            # (Cần kiểm tra lại cấu trúc sau giải nén và điều chỉnh cho khớp)
            ```
            Theo `DATA.md`, cấu trúc cho Caltech101 nên là:
            ```
            $DATA_ROOT/caltech-101/
                images/ # Thư mục này chứa các thư mục con là tên class (ví dụ: accordion, airplanes)
                    accordion/
                        image_0001.jpg
                        ...
                    airplanes/
                        image_0001.jpg
                        ...
                split_zhou_Caltech101.json # File này cần được tạo hoặc tải về nếu có sẵn từ CoOp/CLIP_adapter
            ```
            File `split_zhou_Caltech101.json` rất quan trọng. Repository LLaMP không cung cấp trực tiếp các file split này. Bạn cần tìm chúng từ các repository khác như CoOp hoặc CLIP-Adapter, hoặc tự tạo nếu biết cách. Thông thường, các file này định nghĩa tập train/val/test.
            Link tham khảo cho split files: [https://github.com/KaiyangZhou/CoOp/tree/main/data/caltech-101](https://github.com/KaiyangZhou/CoOp/tree/main/data/caltech-101) (tải `split_zhou_Caltech101.json`) và đặt vào `$DATA_ROOT/caltech-101/`.

    *   **Đối với ImageNet:** Quá trình tương tự nhưng phức tạp hơn do kích thước lớn. Xem `DATA.md` để biết chi tiết.

---

**Bước 3: Tải mô hình đã huấn luyện (Pretrained Models)**

1.  **Tạo thư mục `pretrained`:**
    Bên trong thư mục `LLaMP`:
    ```bash
    mkdir pretrained
    ```

2.  **Tải checkpoints:**
    *   Link tải được cung cấp trong README: [Google Drive](https://drive.google.com/drive/folders/1o7OKxRncxI2otl0p2ZkSOq1Jz8ZTa6Ad?usp=sharing)
    *   Có hai loại: "LLaMP Base models" và "LLaMP Large models".
    *   Để test, bạn có thể bắt đầu với "LLaMP Base models". Ví dụ, tải `llamp_base_caption_retrieval.pth`.
    *   Đặt file `.pth` đã tải vào thư mục `LLaMP/pretrained/`.

---

**Bước 4: Chạy Inference/Testing**

Repository cung cấp các script bash trong thư mục `scripts/`.

1.  **Chỉnh sửa script (RẤT QUAN TRỌNG):**
    *   Mở script bạn muốn chạy, ví dụ: `scripts/llamp_base/zeroshot.sh`.
    *   Tìm dòng `DATA_ROOT="/path/to/your/data"` và **thay đổi nó thành đường dẫn tuyệt đối** đến thư mục `DATA_ROOT` mà bạn đã tạo ở Bước 2 (ví dụ: `/home/user/projects/data` hoặc giá trị của biến `$DATA_ROOT` bạn đã export).
    *   Kiểm tra `CKPT_PATH` trong script. Nó nên trỏ đúng đến file checkpoint bạn đã tải, ví dụ `pretrained/llamp_base_caption_retrieval.pth`. Mặc định có vẻ đã đúng nếu bạn đặt file vào thư mục `pretrained`.

2.  **Ví dụ chạy Zero-shot evaluation trên Caltech101 với LLaMP-Base:**
    *   Giả sử bạn muốn chạy trên GPU 0 và dataset là `caltech101`.
    *   Sau khi đã chỉnh sửa `DATA_ROOT` trong `scripts/llamp_base/zeroshot.sh`:
        ```bash
        bash scripts/llamp_base/zeroshot.sh 0 caltech101
        ```
        Trong đó:
        *   `0`: là ID của GPU.
        *   `caltech101`: là tên dataset (phải khớp với tên thư mục trong `DATA_ROOT` và cách dataset được định nghĩa trong code).

3.  **Ví dụ chạy Few-shot evaluation trên ImageNet với LLaMP-Base (16-shot):**
    *   Chỉnh sửa `DATA_ROOT` trong `scripts/llamp_base/fewshot.sh`.
    *   Đảm bảo bạn đã chuẩn bị ImageNet đúng cách.
    *   ```bash
        bash scripts/llamp_base/fewshot.sh 0 imagenet 16
        ```
        Trong đó:
        *   `0`: ID GPU.
        *   `imagenet`: Tên dataset.
        *   `16`: Số lượng shot (ví dụ).

**Các tham số trong script `zeroshot.sh` (ví dụ):**
```bash
# scripts/llamp_base/zeroshot.sh
#!/bin/bash
cd ../.. # Chuyển về thư mục gốc LLaMP

GPU_ID=$1
DATASET=$2 # Ví dụ: caltech101,imagenet,oxford_pets,... (có thể là danh sách các dataset)

DATA_ROOT="/path/to/your/data" # <<< BẠN PHẢI THAY ĐỔI DÒNG NÀY
CFG="llamp_base_zeroshot" # Config của mô hình
CKPT_PATH="pretrained/llamp_base_caption_retrieval.pth" # Đường dẫn checkpoint

python main.py \
--gpu_id ${GPU_ID} \
--cfg ${CFG} \
--ckpt_path ${CKPT_PATH} \
--dataset ${DATASET} \
--data_root ${DATA_ROOT} \
--eval_only
```
Script này sẽ gọi `main.py` với các tham số tương ứng.

---

**Lưu ý quan trọng và Gỡ lỗi:**

*   **Đường dẫn:** Sai lầm phổ biến nhất là đường dẫn sai tới `DATA_ROOT` hoặc `CKPT_PATH`. Hãy kiểm tra kỹ và sử dụng đường dẫn tuyệt đối nếu không chắc.
*   **File split (`.json`):** Đảm bảo các file split (ví dụ `split_zhou_Caltech101.json`) tồn tại trong thư mục dataset tương ứng trong `DATA_ROOT`. Nếu không có, bạn sẽ gặp lỗi khi load dữ liệu.
*   **GPU:** Đảm bảo bạn có GPU NVIDIA, driver tương thích và PyTorch được cài đặt với CUDA support. Nếu không có GPU, code có thể không chạy hoặc rất chậm (nếu có hỗ trợ CPU fallback, nhưng thường không tối ưu).
*   **Thiếu thư viện:** Nếu gặp lỗi `ModuleNotFoundError`, hãy `conda activate llamp` và `pip install <tên_thư_viện_thiếu>`.
*   **Phiên bản CUDA:** Nếu `environment.yml` không tương thích với CUDA của bạn, bạn có thể tạo môi trường thủ công:
    ```bash
    conda create -n llamp python=3.8 # Hoặc 3.9
    conda activate llamp
    # Cài PyTorch phù hợp với CUDA của bạn từ https://pytorch.org/get-started/previous-versions/
    # Ví dụ cho CUDA 11.7:
    # pip install torch==1.13.1+cu117 torchvision==0.14.1+cu117 torchaudio==0.13.1 --extra-index-url https://download.pytorch.org/whl/cu117
    # Sau đó cài các gói còn lại từ requirements.txt (nếu có) hoặc thủ công
    pip install -r requirements.txt # (Kiểm tra xem có file này không, nếu không thì cài các gói như tqdm, yacs, etc.)
    pip install git+https://github.com/openai/CLIP.git
    pip install open_clip_torch
    ```
*   **Đọc log lỗi:** Luôn kiểm tra kỹ output và log lỗi để xác định vấn đề.

Chúc bạn thành công với việc chạy LLaMP! Nếu có lỗi cụ thể, bạn có thể cung cấp thêm thông tin để được hỗ trợ tốt hơn.
