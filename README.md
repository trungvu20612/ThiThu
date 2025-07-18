# ThiThu
Thực Hành Biến Đổi & Tiền Xử Lý Ảnh Nâng Cao
Sinh viên thực hiện: Vũ Minh Trung
MSSV: 2274802010945
Môn học: Nhập môn Xử lý ảnh số
Giảng viên: Đỗ Hữu Quân
BÀI 1)
Biến Đổi & Lọc Ảnh Grayscale + Màu HSV
* Giới thiệu
Bài lab này nhằm thực hành các kỹ thuật tiền xử lý ảnh cơ bản bao gồm:

Lọc trung bình làm mượt ảnh

Phát hiện biên qua Laplacian

Biến đổi màu ngẫu nhiên trong ảnh RGB

Chuyển ảnh sang không gian màu HSV và tách riêng từng kênh

Các thao tác này giúp sinh viên:

Làm quen với các phép biến đổi không gian ảnh

Hiểu cơ bản về phân tích kênh màu

Ứng dụng trong tiền xử lý ảnh, trích xuất đặc trưng

* Công nghệ sử dụng
Công cụ	Mục đích
Python	Ngôn ngữ lập trình chính
OpenCV (cv2)	Xử lý ảnh nhanh, hỗ trợ nhiều bộ lọc
NumPy	Biểu diễn và thao tác ảnh dạng mảng

* Các thao tác xử lý ảnh
1. Lọc trung bình (Mean Filter)
Mục đích: Làm mượt ảnh, giảm nhiễu

Kích thước kernel: 5×5

Kết quả lưu: a_mean.jpg

python
Copy
Edit
mean_filtered = cv2.blur(image, (5, 5))
2. Phát hiện biên (Edge Detection - Laplacian)
Mục đích: Tìm các cạnh, đường viền rõ ràng

Không gian màu: Ảnh xám

Kết quả lưu: a_edge.jpg

python
Copy
Edit
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
edges = cv2.Laplacian(gray_image, cv2.CV_64F)
edges = cv2.convertScaleAbs(edges)
3. Đổi màu ngẫu nhiên (Random RGB Shuffle)
Mục đích: Trộn kênh màu RGB để tạo hiệu ứng ngẫu nhiên

Ứng dụng: Phân tích độ ảnh hưởng từng kênh

Kết quả lưu: a_random_color.jpg

python
Copy
Edit
random_indices = list(np.random.permutation(3))
random_colored = image[:, :, random_indices]
4. Chuyển đổi HSV & Tách kênh
Mục đích: Phân tích từng thành phần Hue (màu), Saturation (độ bão hòa), Value (độ sáng)

Kết quả lưu:

a_hue.jpg

a_saturation.jpg

a_value.jpg

python
Copy
Edit
hsv_image = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)
h, s, v = cv2.split(hsv_image)
 Cấu trúc thư mục
bash
Copy
Edit
├── main.py              # Mã nguồn chính
├── a.jpg                # Ảnh gốc đầu vào
├── a_mean.jpg           # Ảnh sau lọc trung bình
├── a_edge.jpg           # Ảnh sau Laplacian
├── a_random_color.jpg   # Ảnh sau trộn màu ngẫu nhiên
├── a_hue.jpg            # Kênh Hue
├── a_saturation.jpg     # Kênh Saturation
├── a_value.jpg          # Kênh Value
├── README.md            # File mô tả này
 Hướng dẫn sử dụng
1. Cài đặt thư viện
bash
Copy
Edit
pip install opencv-python numpy
2. Chạy chương trình
Đảm bảo có file a.jpg trong cùng thư mục.

Chạy lệnh:

bash
Copy
Edit
python main.py
Kết quả sẽ được lưu ra file như mô tả ở trên.

 Ghi chú
Bạn có thể thử thay đổi kích thước kernel trong mean filter để thấy hiệu ứng rõ hơn.

Thử các ảnh khác với độ tương phản/độ sáng khác nhau để đánh giá hiệu quả lọc và phát hiện biên.

Các phép biến đổi HSV hữu ích trong việc nhận diện vật thể theo màu sắc.

 Giới thiệu
Tài liệu này mô tả chi tiết các bước thực hiện xử lý ảnh nâng cao bao gồm:

Các phép biến đổi cường độ (gamma, log, histogram, contrast…)

Biến đổi hình học: xoay, lật, resize

Lọc mờ ảnh và điều chỉnh độ sáng/tương phản

Tăng cường chất lượng ảnh theo nhiều hướng tiếp cận

Việc thực hành các thao tác này giúp sinh viên:

Nắm vững các khái niệm tiền xử lý ảnh

Phân biệt và lựa chọn kỹ thuật phù hợp với từng bài toán

Áp dụng linh hoạt các hàm trong OpenCV và NumPy

 Công nghệ sử dụng
Công cụ	Mục đích
Python	Ngôn ngữ lập trình chính
OpenCV	Xử lý ảnh (đọc, lọc, biến đổi hình học)
NumPy	Tính toán ma trận ảnh, tạo bảng tra cứu
Random	Sinh số ngẫu nhiên để thử nghiệm thông số

 *BÀI 2 – Biến Đổi Cường Độ Ảnh
Danh sách ảnh đầu vào:
diff
Copy
Edit
- image1.jpg
- image2.jpg
- image3.jpg
Tùy chọn biến đổi (menu):
Phím	Phép biến đổi	Mô tả
I	Inverse Transformation	Đảo ngược ảnh (âm bản)
G	Gamma Correction	Làm sáng/tối ảnh theo gamma
L	Logarithmic Transformation	Tăng cường chi tiết vùng tối
H	Histogram Equalization	Cân bằng histogram ảnh
C	Contrast Stretching	Kéo giãn độ tương phản tự động (ngẫu nhiên ngưỡng min/max)
A	Adaptive Histogram Equalization (CLAHE)	Cải thiện chi tiết ảnh bằng CLAHE

Ví dụ thông số sinh ngẫu nhiên:
Gamma: 0.5 – 2.0

Contrast α: 0.5 – 2.0

Brightness β: -50 – +50

Log c: 1.0 – 5.0

 Bài 3 – Biến Đổi Hình Học & Tăng Cường Ảnh
1. Resize + Thêm biên
Ảnh: colorful-ripe-tropical-fruits.jpg

Thao tác: Tăng kích thước thêm 30 pixel mỗi chiều

python
Copy
Edit
resized = cv2.resize(image, (width + 30, height + 30))
 Output: output_colorful_resized.jpg

2. Xoay 45 độ + Lật ngang
Ảnh: quang-ninh.jpg

Thao tác: Xoay theo chiều kim đồng hồ, rồi lật ngang

python
Copy
Edit
matrix = cv2.getRotationMatrix2D(center, -45, 1.0)
flipped = cv2.flip(rotated, 1)
 Output: output_quangninh_rotated_flipped.jpg

3. Phóng to 5 lần + Làm mờ Gaussian
Ảnh: pagoda.jpg

Thao tác: Resize lên gấp 5 lần, sau đó làm mờ kernel 7×7

python
Copy
Edit
resized = cv2.resize(image, (width * 5, height * 5))
blurred = cv2.GaussianBlur(resized, (7, 7), 0)
📁 Output: output_pagoda_upscaled_blurred.jpg

4. Điều chỉnh độ sáng và tương phản
Ảnh: pagoda.jpg

Thao tác: Áp dụng công thức I_out = α * I_in + β

python
Copy
Edit
adjusted = cv2.convertScaleAbs(image, alpha=alpha, beta=beta)
📁 Output: output_pagoda_brightness_contrast.jpg
📝 Thông số in ra console: alpha = 1.47, beta = 32

📁 Cấu trúc thư mục
bash
Copy
Edit
├── bai2_bien_doi_cuong_do.py         # Mã chính xử lý bài 2
├── bai3_bien_doi_hinh_hoc.py         # Mã chính xử lý bài 3
├── image1.jpg
├── image2.jpg
├── image3.jpg
├── colorful-ripe-tropical-fruits.jpg
├── quang-ninh.jpg
├── pagoda.jpg
├── output_inverse_1.jpg              # Kết quả bài 2
├── output_gamma_1.jpg                # ...
├── output_log_1.jpg                  # ...
├── output_histogram_1.jpg           # ...
├── output_contrast_1.jpg            # ...
├── output_adaptive_1.jpg            # ...
├── output_colorful_resized.jpg
├── output_quangninh_rotated_flipped.jpg
├── output_pagoda_upscaled_blurred.jpg
├── output_pagoda_brightness_contrast.jpg
├── README.md                         # File mô tả này
▶️ Hướng dẫn sử dụng
Cài đặt thư viện:
bash
Copy
Edit
pip install opencv-python numpy
Chạy bài 2:
bash
Copy
Edit
python bai2_bien_doi_cuong_do.py
Chọn phím tương ứng trong menu để áp dụng phép biến đổi.

Chạy bài 3:
bash
Copy
Edit
python bai3_bien_doi_hinh_hoc.py
Tự động thực hiện toàn bộ thao tác và lưu kết quả.
