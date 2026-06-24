# Problem 1: Post-Semester GPA Prediction

## 1. Phương pháp thực hiện
- **Mục tiêu:** Dự báo điểm trung bình học kỳ sau (`Post_Semester_GPA`) của sinh viên dưới dạng giá trị liên tục (Bài toán Hồi quy - Regression).
- **Biến dự báo (Features):** Bao gồm số giờ dùng AI, số giờ học truyền thống, mức độ phụ thuộc, ngành học, mục đích sử dụng AI,...
- **Thuật toán:** Linear Regression, Decision Tree, Random Forest.

## 2. So sánh hiệu suất mô hình
Dựa trên kết quả thực nghiệm với tập dữ liệu Train và Test, hiệu suất của các thuật toán được tóm tắt như sau:

| Model | Train MAE | Test MAE | Train RMSE | Test RMSE | Train R² | Test R² |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Linear Regression** | 0.1318 | 0.1306 | 0.1683 | 0.1663 | 0.8853 | 0.8854 |
| **Decision Tree** | 0.1142 | 0.1301 | 0.1474 | 0.1697 | 0.9120 | 0.8807 |
| **Random Forest** | 0.1091 | 0.1213 | 0.1387 | 0.1556 | 0.9220 | 0.8997 |

**Nhận xét chi tiết về hiệu suất:**
- **Random Forest**
  - Mô hình cho hiệu suất tối ưu nhất trên tập dữ liệu này khi đạt hệ số tương quan cao nhất với `Test_R²` = 0.8997, nghĩa là giải thích được gần 90% sự biến động của điểm GPA thực tế.
  - Mô hình cũng ghi nhận các mức sai số thấp nhất (`Test_MAE` = 0.1213, `Test_RMSE` = 0.1556).
  - Độ chênh lệch hiệu suất giữa tập Train và tập Test rất nhỏ (khoảng 0.02 đối với R²), chứng tỏ mô hình có khả năng tổng quát hóa tốt và không bị Overfitting đáng kể nhờ cơ chế Ensemble (học máy kết hợp từ nhiều cây quyết định).
- **Linear Regression**
  - Các chỉ số hiệu suất trên cả hai tập vô cùng sát nhau (`Train_R²` = 0.8853 và `Test_R²` = 0.8854), thậm chí sai số trên tập Test (`Test_MAE` = 0.1306) còn thấp hơn nhẹ so với tập Train. Điều này chứng tỏ mô hình cực kỳ ổn định, có tính tổng quát cao và hoàn toàn không bị Overfitting.
  - Vì Linear Regression là mô hình tuyến tính, việc nó đạt kết quả cao (giải thích được 88.54% biến động) chứng tỏ mối quan hệ giữa các biến dự báo và điểm GPA mang tính tuyến tính rất mạnh mẽ trong bộ dữ liệu này.
- **Decision Tree**
  - Mô hình bộc lộ xu hướng quá khớp (Overfitting) rõ rệt nhất trong 3 thuật toán. Cụ thể, trên tập huấn luyện mô hình học rất tốt (`Train_R²` lên tới 0.9120), nhưng khi áp dụng vào tập Test độc lập, hiệu suất giảm xuống rõ rệt (`Test_R²` = 0.8807, thấp nhất trong 3 mô hình) và sai số bình phương tăng lên (`Test_RMSE` = 0.1697).
  - Điều này phản ánh nhược điểm cố hữu của một cây quyết định đơn lẻ khi dễ dàng "học thuộc lòng" cả các nhiễu trong tập dữ liệu huấn luyện.

## 4. Kết luận
- Khác với bài toán phân loại mức độ kiệt sức (Burn-Out Risk), các mô hình hồi quy đối với bài toán dự báo điểm số GPA này đạt độ chính xác rất cao, với khả năng giải thích và dự đoán đúng từ 88% đến gần 90% kết quả thực tế.
- Nhìn chung, các mô hình hoạt động ổn định và kiểm soát tốt hiện tượng biến động dữ liệu (ngoại trừ Decision Tree bị Overfitting nhẹ, hai mô hình còn lại không có dấu hiệu sai lệch cấu trúc hay Underfitting).
- Mô hình hoạt động hiệu quả nhất và được đề xuất lựa chọn là **Random Forest** nhờ đạt được chỉ số `Test_R²` cao nhất đồng thời tối thiểu hóa tối đa các lỗi sai số tuyệt đối (`MAE`) và sai số bình phương (`RMSE`).
# Problem 2: Burn-Out Risk Level Prediction
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

# Problem 3: Behavior Clustering (Unsupervised)
## 1. Nhận xét về việc lựa chọn số cụm

Theo biểu đồ Elbow, giá trị Inertia giảm liên tục khi số cụm (k) tăng từ 2 đến 10. Điểm gãy được ước lượng tại (k=5), cho thấy từ sau 5 cụm, mức giảm Inertia bắt đầu chậm hơn và việc tăng thêm số cụm không còn đem lại cải thiện lớn như ở giai đoạn trước.

Tuy nhiên, kết quả Silhouette Score lại cho thấy (k=2) là phương án tốt nhất. Tại (k=2), Silhouette Score đạt **0,2663**, cao hơn rõ rệt so với (k=3) là **0,1779** và các giá trị (k) còn lại, vốn chỉ dao động trong khoảng từ khoảng **0,1555 đến 0,1780**. Điều này cho thấy khi chia dữ liệu thành hai cụm, mức độ gần nhau giữa các sinh viên trong cùng cụm và mức độ phân biệt giữa hai cụm tốt hơn so với khi chia thành nhiều nhóm nhỏ hơn.

Chỉ số Calinski–Harabasz cũng đạt giá trị cao nhất tại (k=2), bằng **16.140,6857**, sau đó giảm dần khi số cụm tăng. Kết quả này tiếp tục củng cố cho phương án hai cụm, vì độ phân tán giữa các cụm tại (k=2) là lớn nhất so với độ phân tán bên trong từng cụm.

Đối với Davies–Bouldin Score, giá trị tại (k=2) là **1,5290**. Đây không phải giá trị thấp nhất trong toàn bộ các phương án, các giá trị (k=5), (k=8) và (k=10) có Davies–Bouldin thấp hơn một chút. Tuy nhiên, khi tăng số cụm, Silhouette Score và Calinski–Harabasz Score đều giảm đáng kể, trong khi mô hình trở nên phức tạp và khó diễn giải hơn. Vì vậy, mức cải thiện điểm nhỏ của Davies–Bouldin không đủ để bù lại sự suy giảm của hai chỉ số còn lại.

Như vậy, mặc dù Elbow Method gợi ý (k=5), việc lựa chọn **(k=2)** cho mô hình K-Means cuối cùng là hợp lý vì phương án này đạt Silhouette Score và Calinski–Harabasz Score tốt nhất, đồng thời tạo ra cấu trúc phân cụm đơn giản và dễ diễn giải. Kết quả cũng cho thấy dữ liệu phù hợp hơn với hai nhóm hành vi lớn thay vì nhiều nhóm hành vi nhỏ.

## 2. Nhận xét từ heatmap tâm cụm

Heatmap tâm cụm chuẩn hóa cho thấy sự khác biệt giữa hai nhóm chủ yếu đến từ ba đặc trưng:

1. Thời gian sử dụng GenAI
2. Mức phụ thuộc AI
3. Mức lo lắng trong kỳ thi

Trong đó, thời gian sử dụng GenAI và mức phụ thuộc AI là hai đặc trưng tạo ra sự khác biệt lớn nhất. Cụm 0 có giá trị dương cao ở hai biến này, trong khi Cụm 1 có giá trị âm.

Thời gian học truyền thống cũng góp phần phân biệt hai cụm, nhưng mức chênh lệch không mạnh bằng các biến liên quan đến việc sử dụng và phụ thuộc AI.

Đáng chú ý, mức đa dạng công cụ AI của hai nhóm gần như giống nhau, với giá trị trung bình lần lượt là 2,81 và 2,80, còn giá trị chuẩn hóa đều xấp xỉ 0. Điều này cho thấy số lượng loại công cụ AI được sử dụng không phải là yếu tố quan trọng trong việc hình thành hai cụm. Điểm khác biệt chính nằm ở **thời lượng sử dụng và mức độ phụ thuộc**, chứ không phải số loại công cụ mà sinh viên sử dụng.

## 3. Nhận xét từ biểu đồ PCA

Hai thành phần chính của PCA giải thích được **58,0% tổng phương sai** của năm đặc trưng ban đầu. Trên biểu đồ PCA, hai cụm được phân chia tương đối rõ theo trục PC1:

* Cụm 1 tập trung chủ yếu ở phía bên trái
* Cụm 0 tập trung chủ yếu ở phía bên phải

Kết quả này cho thấy sự khác biệt về hành vi giữa hai nhóm được thể hiện khá rõ trên thành phần chính thứ nhất. Các đặc trưng như thời gian sử dụng GenAI và mức phụ thuộc AI nhiều khả năng đóng góp đáng kể vào hướng phân tách này, phù hợp với kết quả thể hiện trên heatmap tâm cụm.

Tuy nhiên, tại khu vực ranh giới giữa hai cụm vẫn xuất hiện một số điểm chồng lấn. Điều này phù hợp với Silhouette Score đạt 0,2663, cho thấy hai nhóm có sự khác biệt nhưng chưa hoàn toàn tách biệt.

Ngoài ra, PCA hai chiều mới chỉ giữ lại 58,0% thông tin biến thiên của dữ liệu, còn khoảng 42,0% phương sai nằm trong các chiều chưa được biểu diễn. Vì vậy, biểu đồ PCA chỉ được sử dụng để minh họa trực quan, chất lượng mô hình vẫn phải được đánh giá dựa trên dữ liệu năm chiều và các chỉ số phân cụm.

## 4. Tổng hợp kết quả

Kết quả K-Means cho thấy sinh viên trong bộ dữ liệu có thể được chia thành hai xu hướng hành vi chính. Nhóm thứ nhất sử dụng GenAI với cường độ cao, phụ thuộc AI nhiều hơn, học truyền thống ít hơn và có mức lo lắng khi thi cao hơn. Nhóm thứ hai sử dụng AI ít hơn, ít phụ thuộc hơn, có thời gian học truyền thống cao hơn và chiếm phần lớn số sinh viên.

Các đặc trưng phân biệt hai nhóm mạnh nhất là thời gian sử dụng GenAI, mức phụ thuộc AI và mức lo lắng trong kỳ thi. Ngược lại, mức đa dạng công cụ AI gần như không tạo ra khác biệt giữa hai cụm.

Mô hình với (k=2) tạo ra cách phân chia đơn giản, có ý nghĩa và dễ diễn giải. Tuy vậy, do Silhouette Score chưa cao và biểu đồ PCA vẫn có một phần chồng lấn, các cụm nên được xem là những nhóm hành vi tương đối, không phải các nhãn cố định hoặc đánh giá sinh viên theo hướng tốt và xấu.
