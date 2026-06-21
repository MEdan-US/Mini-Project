# Report - Problem 2: Burn-Out Risk Level Prediction
## 1. Phương pháp thực hiện
- **Mục tiêu:** Dự đoán mức độ kiệt sức (Low, Medium, High) của sinh viên.
- **Biến dự báo (Features):** Bao gồm số giờ dùng AI, số giờ học truyền thống, mức độ phụ thuộc, ngành học, mục đích sử dụng AI... (Loại bỏ `Post_Semester_GPA` để tránh rò rỉ dữ liệu).
- **Thuật toán:** Logistic Regression, Random Forest Classifier, Gradient Boosting Classifier.
- **Tối ưu hóa:** Sử dụng `GridSearchCV` với 5-fold Cross-Validation để tinh chỉnh siêu tham số và lựa chọn mô hình tốt nhất thông qua `f1_macro`.
## 2. So sánh hiệu suất mô hình
Dựa trên kết quả thực nghiệm với tập dữ liệu Test, hiệu suất của các thuật toán được tóm tắt như sau:
| Model | Train Accuracy | Test Accuracy | Train Precision | Test Precision | Train Recall | Test Recall | Train F1-Score | Test F1-Score |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Logistic Regression** | 0.5207 | 0.5200 | 0.5532 | 0.5487 | 0.5073 | 0.5055 | 0.5205 | 0.5179 |
| **Random Forest Classifier** | 0.5597 | 0.5265 | 0.6029 | 0.5659 | 0.5390 | 0.5060 | 0.5536 | 0.5192 |
| **Gradient Boosting Classifier** | 0.5431 | 0.5330 | 0.5754 | 0.5633 | 0.5304 | 0.5198 | 0.5438 | 0.5326 |

**Nhận xét chung về hiệu suất:**
- **Gradient Boosting Classifier**
  -Mô hình cho chỉ số Test_f1-score cao nhất với 0.5326 và các chỉ số còn lại trừ Test_Precision đều cao nhất. Bên cạnh đó, độ chênh lệch giữa tập train và tập test thấp khoảng 0.01 -> 0.02 => mô hình không bị 
- **Random Forest**
  - Các chỉ số test đều cao khoảng 0.->0.52, riêng chỉ số Test_Presion cao nhất với 0.566 cho thấy mô hình có tỉ lệ số dự đoán đúng mức độ kiệt sức trên tổng số dự đoán của mức độ đó cao
  - Giữa tập train và test có chênh lệch nhẹ khoảng 0.3 -> 0.4 => không bị overfitting đáng kể
- **Logistic Regression**:
  - Logistic Regression có kết quả thấp nhất trong ba mô hình, nhưng vẫn là một baseline tốt.
  - Train F1 là 0.5205 và Test F1 là 0.5179, hai giá trị rất gần nhau. Điều này cho thấy mô hình ít bị overfitting.
  - Mô hình có Test_Recall thấp hơn Test_Precision, nghĩa là mô hình có xu hướng tìm được số người có mức độ kiệt sức đúng trên tổng số người mà mô hình dự đoán là mức độ kiệt sức đó
  - Vì Logistic Regression là mô hình tuyến tính, nó có thể chưa mô tả tốt các quan hệ phi tuyến trong dữ liệu khoản vay.
## 4. Kết luận
- Các mô hình không có sự chênh lệch quá nhiều đối với bộ dữ liệu này và chỉ dự đoán đúng được khoảng 52% so với thực tế
- Các mô hình không bị overfitting và có dấu hiệu underfitting
- Trong các mô hình thì mô hình hoạt động hiệu quả nhất là Gradient Boosting Classifier vì đạt được Test F1_score cao nhất
