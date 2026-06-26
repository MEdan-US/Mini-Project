# Bảng phân công công việc
|MSSV | Họ tên | Tasks | Mức độ đóng góp (%) |
| --- | --- | --- | --- |
|24280017| Trần Minh Nhật | Tiền xử lý dữ liệu và viết báo cáo | 16% |
|24280062| Nguyễn Lương Hoàng Hải | Thực hiện bài toán hồi quy và viết báo cáo | 14% |
|24280065| Ngô Văn Minh Hoàng | EDA phân tích tương quan và viết báo cáo | 14% |
|24280066| Nguyễn Thanh Hoàng | EDA biến định lượng và viết báo cáo | 14% |
|24280083| Kiên Tô Mon | EDA biến định tính và viết báo cáo | 14% |
|24280092| Bùi Hoàng Phát | Thực hiện bài toán phân loại và viết báo cáo | 14% |
|24280104| Lê Tấn Thành | Thực hiện bài toán phân cụm và viết báo cáo | 14% |


# 1. Giới thiệu bài toán
Phân tích tác động của việc sử dụng công cụ A.I tạo sinh đối với kết quả học tập, sức khỏe tinh thần và nguy cơ kiệt sức của 50.000 học sinh, sinh viên.


# 2. Mô tả dữ liệu:
## Dataset Overview
**Nguồn**: [Impact of AI on Students](https://www.kaggle.com/datasets/laveshjadon/ai-impact-on-students)

| Property | Details |
| :--- | :--- |
| **Rows** | 50.000 học sinh, sinh viên |
| **Columns** | 16 thuộc tính (features) |
| **Missing Values** | Không có (bộ dữ liệu hoàn toàn đầy đủ) |
| **File Format** | CSV |
| **Target Variables** | `Post_Semester_GPA`, `Skill_Retention_Score`, `Burnout_Risk_Level` |

---

## Column Descriptions

### Identifier
| Column | Type | Description |
| :--- | :--- | :--- |
| `Student_ID` | Integer | Mã định danh dạng số duy nhất cho mỗi học sinh/sinh viên (100001–150000) |

### Academic Profile
| Column | Type | Description |
| :--- | :--- | :--- |
| `Major_Category` | Categorical | Ngành học của sinh viên — STEM, Kinh doanh (Business), Nhân văn (Humanities), Y tế (Medical), Nghệ thuật (Arts) |
| `Year_of_Study` | Categorical | Năm học — Sinh viên năm nhất (Freshman), Năm hai (Sophomore), Năm ba (Junior), Năm tư (Senior), Học viên sau đại học (Graduate) |
| `Pre_Semester_GPA` | Float | Điểm GPA khi bắt đầu học kỳ (khoảng: ~1.18 – 4.00) |
| `Post_Semester_GPA`| Float | Điểm GPA vào cuối học kỳ (khoảng: ~1.00 – 4.00) — biến kết quả chính |

### AI Usage Behaviour
| Column | Type | Description |
| :--- | :--- | :--- |
| `Weekly_GenAI_Hours` | Float | Số giờ trung bình mỗi tuần dành cho việc sử dụng các công cụ AI tạo sinh (0 – 40 giờ) |
| `Primary_Use_Case` | Categorical | Mục đích chính mà sinh viên sử dụng AI — Soạn thảo/Viết lách (Copywriting/Drafting), Tóm tắt bài đọc (Summarizing_Reading), Sửa lỗi/Xử lý sự cố mã nguồn (Debugging/Troubleshooting), Lên ý tưởng (Ideation), Tạo câu trả lời trực tiếp (Direct_Answer_Generation) |
| `Prompt_Engineering_Skill` | Categorical | Mức độ thành thạo tự đánh giá trong việc đặt câu lệnh (prompt) hiệu quả — Sơ cấp (Beginner), Trung cấp (Intermediate), Cao cấp (Advanced) |
| `Tool_Diversity` | Integer | Số lượng các công cụ AI khác nhau được sử dụng (1–5) |
| `Paid_Subscription` | Boolean | Sinh viên có sử dụng tài khoản AI trả phí hay không (True / False) |

### Study Behaviour
| Column | Type | Description |
| :--- | :--- | :--- |
| `Traditional_Study_Hours` | Float | Số giờ hằng tuần dành cho các phương pháp học tập truyền thống (không dùng AI) (1 – ~36 giờ) |
| `Perceived_AI_Dependency` | Integer | Mức độ phụ thuộc vào các công cụ AI do sinh viên tự đánh giá, theo thang điểm từ 1 (thấp) đến 10 (cao) |

### Institutional Context
| Column | Type | Description |
| :--- | :--- | :--- |
| `Institutional_Policy` | Categorical | Quy định chính thức của nhà trường về việc sử dụng AI — Cho phép kèm trích dẫn (Allowed_With_Citation), Nghiêm cấm (Strictly_Ban), Tích cực khuyến khích (Actively_Encouraged) |

### Mental Health & Well-being
| Column | Type | Description |
| :--- | :--- | :--- |
| `Anxiety_Level_During_Exams` | Integer | Mức độ lo lắng trong kỳ thi do sinh viên tự báo cáo, từ 1 (tối thiểu) đến 10 (nghiêm trọng) |
| `Skill_Retention_Score` | Float | Điểm số (0–100) đo lường mức độ ghi nhớ và giữ vững các kỹ năng đã học của sinh viên sau học kỳ |
| `Burnout_Risk_Level` | Categorical | Mức độ rủi ro kiệt sức được đánh giá — Thấp (Low), Trung bình (Medium), Cao (High) |

---
# 3. Phân tích khám phá dữ liệu (EDA):
## Các biến định lượng (Numerical Features):
### 1. Cải thiện điểm nhờ A.I
* **Nội dung:** Cả `Post_Semester_GPA` và `Skill_Retention_Score` đều có xu hướng lệch trái (phần lớn đạt điểm cao). Tuy nhiên, tại các mốc tuyệt đối (GPA 4.0 và Skill Retention 100) lại ghi nhận **sự tăng vọt bất thường** so với thời điểm đầu kỳ (`Pre_Semester_GPA`). 
* **Ý nghĩa:** Điều này cho thấy việc ứng dụng GenAI có khả năng gia tăng điểm số và kết quả đánh giá kỹ năng của sinh viên lên mức tối đa một cách đột biến.

### 2. Khoảng cách học lực giữa các nhóm sinh viên
* **Nội dung:** Mặc dù phần lớn sinh viên có năng lực học tập khá giỏi, dữ liệu vẫn xuất hiện dải ngoại lai kéo dài hẳn về phía bên trái ở các biến `Pre_GPA`, `Post_GPA`, và `Skill_Retention_Score`. 
* **Ý nghĩa:** Phản ánh một nhóm nhỏ sinh viên đang bị tụt lại phía sau rất xa so với mặt bằng chung, tạo nên sự phân hóa rõ rệt về năng lực trong môi trường giáo dục.

### 3. Xu hướng lạm dụng AI cực đoan
* **Nội dung:** Biến `Weekly_GenAI_Hours` lệch phải nặng (phần lớn dùng `< 5h/tuần`) nhưng xuất hiện một nhóm ngoại lai lạm dụng AI cực đoan (từ 25 đến tận 40h/tuần). Đáng chú ý, ở biến `Traditional_Study_Hours`, đồ thị vọt lên bất thường ở mốc sát 0 (`< 3h/tuần`).
* **Ý nghĩa:** Có một bộ phận sinh viên đã gần như thay thế hoàn toàn thời gian tự học truyền thống bằng việc phụ thuộc hoàn toàn vào công cụ AI.

### 4. Lạm dụng A.I và dẫn đến áp lực thi cử
* **Nội dung:** Phân tích đa biến chỉ ra mối tương quan thuận rõ rệt: Thời gian dùng AI tương quan mạnh với mức độ lệ thuộc (0.67), và mức độ lệ thuộc lại tương quan dương với lo lắng thi cử (0.31).
* **Ý nghĩa:** Sinh viên càng dành nhiều thời gian cho GenAI thì càng bị phụ thuộc tâm lý. Sự lệ thuộc này trực tiếp chuyển hóa thành áp lực và sự lo lắng cực đoan khi bước vào phòng thi — nơi họ buộc phải tự lực và không được phép sử dụng công cụ trợ giúp.

### 5. Mối tương quan giữa thời lượng sử dụng AI và hiệu quả thực tế
* **Nội dung:** Hệ số tương quan giữa số giờ sử dụng AI (`Weekly_GenAI_Hours`) và điểm số cuối kỳ (`Post_Semester_GPA`) gần như bằng không (-0.02), thể hiện mối quan hệ phi tuyến tính rõ ràng.
* **Ý nghĩa:** Việc tăng vô tội vạ thời gian dùng AI không hề giúp sinh viên tăng GPA một cách tuyến tính. Hiệu quả học tập thực chất có thể phụ thuộc vào *cách thức sử dụng* (như kỹ năng prompt, mục đích sử dụng) chứ không nằm ở *thời lượng sử dụng*.

### 6. Hiện tượng đa cộng tuyến (Multicollinearity)
- Hai biến `Pre_Semester_GPA` và `Post_Semester_GPA` có mối tương quan tuyến tính thuận cực mạnh (lên tới 0.93), thể hiện rõ qua dải chấm dốc lên trên đồ thị phân tán.

## Các biến định tính (Categorical Features):
### 1. Áp lực đặc thù theo khối ngành học
* **Nội dung:** Khối ngành STEM ghi nhận tỷ lệ sinh viên rơi vào nhóm nguy cơ kiệt sức cao nhất (`Burnout_Risk_Level = High` chiếm 30.0%), ngược lại khối Nghệ thuật (Arts) có tỷ lệ sinh viên ở nhóm nguy cơ thấp cao nhất (33.9%).
* **Ý nghĩa:** Ngành học là một tác nhân trọng yếu ảnh hưởng đến mức độ stress của sinh viên. Các ngành kỹ thuật và khoa học tự nhiên vốn có khối lượng kiến thức nặng thường đẩy sinh viên vào trạng thái áp lực tâm lý.

### 2. Sự phân hóa hành vi sử dụng AI theo trình độ Prompt
* **Nội dung:** Trình độ đặt câu lệnh (`Prompt_Engineering_Skill`) trực tiếp quyết định mục đích sử dụng AI (`Primary_Use_Case`). Nhóm Advanced tập trung sâu vào các tác vụ chuyên biệt hóa như sửa lỗi mã nguồn (`Debugging`), trong khi nhóm Beginner có xu hướng dàn trải (generalist) trên mọi tác vụ.
* **Ý nghĩa:** Trình độ làm chủ công cụ càng cao, sinh viên càng biết cách tối ưu hóa AI vào các bài toán khó mang tính chuyên môn thay vì sử dụng một cách đại trà và hời hợt.

### 3. Sinh viên bị kiệt sức thường sử dụng AI trả phí
* **Nội dung:** Sinh viên sở hữu tài khoản AI trả phí (`Paid_Subscription = Yes`) có tỷ lệ kiệt sức cao vượt trội so với nhóm dùng bản miễn phí (30.2% so với 21.1%).
* **Ý nghĩa:** Điều này cho thấy một mối quan hệ ngược: Không phải việc mua tài khoản trả phí gây ra burnout, mà chính những sinh viên đang bị quá tải workload và stress nặng nề có động lực tài chính cao hơn để nâng cấp công cụ với hy vọng AI sẽ giải cứu họ khỏi áp lực học tập.

### 4. Áp lực từ các chính sách của nhà trường 
* **Nội dung:** Sinh viên ở các trường áp dụng chính sách "Cho phép nhưng phải trích dẫn" (`Allowed_With_Citation`) có tỷ lệ kiệt sức cao nhất, trong khi hai chính sách cực đoan hơn là Cấm triệt để (`Strictly_Ban`) và Khuyến khích hoàn toàn (`Actively_Encouraged`) lại có tỷ lệ kiệt sức tương đương nhau (khoảng 23.8%).
* **Ý nghĩa:** Quy chế lấp lửng, ràng buộc điều kiện (phải trích dẫn, kiểm soát học thuật) vô tình tạo ra một rào cản tâm lý và quy trình phức tạp, khiến sinh viên căng thẳng hơn cả việc cấm hẳn hoặc thả lỏng hoàn toàn.

### 5. Bản chất tác vụ phức tạp đẩy nhanh tiến trình kiệt sức
* **Nội dung:** Tần suất sử dụng AI tập trung mạnh vào các tác vụ đòi hỏi tư duy kéo dài như sửa lỗi lập trình (`Debugging`) và viết lách (`Copywriting`), đồng thời các tác vụ này chiếm tỷ trọng kiệt sức cao vượt trội so với nhóm chỉ dùng AI để lấy kết quả nhanh (`Direct_Answer_Generation`).
* **Ý nghĩa đối với mô hình:** Việc lạm dụng AI cho các tác vụ phức tạp không hề làm giảm tải đầu óc mà trái lại, sự kết hợp giữa tư duy nặng và sự phụ thuộc công cụ càng dễ đẩy sinh viên vào trạng thái quá tải. Đây là đặc trưng phân hóa cực kỳ đắt giá để các mô hình học máy gán trọng số khi dự báo rủi ro burnout.

## Phân tích tương quan

### 1. Biến ảnh hưởng đến điểm số
* **Nội dung:** `Pre_Semester_GPA` thể hiện lực tuyến tính cực mạnh và đạt điểm Mutual Information (MI) tuyệt đối (0.937) với `Post_Semester_GPA`. Bên cạnh đó, các yếu tố như khả năng giữ vững kỹ năng (`Skill_Retention_Score`) và thời gian tự học (`Traditional_Study_Hours`) đều có tương quan thuận với điểm số, bỏ xa các biến công nghệ.
* **Ý nghĩa:** Kết quả học tập cuối kỳ về bản chất vẫn được định đoạt bởi năng lực gốc và phong độ ổn định của sinh viên từ đầu kỳ. Các phương pháp học tập truyền thống và cách tiếp thu kiến thức có sức nặng hơn rất nhiều so với thời lượng tương tác với công nghệ.

### 2. Mối quan hệ của thời lượng sử dụng AI đối với kết quả học tập
* **Nội dung:** Đường hồi quy của `Weekly_GenAI_Hours` đi ngang hoàn toàn và có chỉ số MI nằm ở đáy bảng xếp hạng. 
* **Ý nghĩa:** Thời gian tương tác với AI nhiều hay ít không hề có mối liên hệ trực tiếp đến việc điểm số tăng hay giảm. GenAI ở bối cảnh này đóng vai trò thuần túy là một công cụ hỗ trợ bổ trợ, không phải là yếu tố cốt lõi để thay đổi điểm số của sinh viên.

### 3. Ảnh hưởng của việc lựa chọn phong cách học tập đến hiệu quả học tập
* **Nội dung:** Phân phối của điểm GPA cuối kỳ gần như đồng nhất tuyệt đối trên tất cả các phân loại của mọi biến định tính (như mục đích sử dụng `Primary_Use_Case`, chính sách trường, hay kỹ năng prompt). Điểm trung bình và trung vị của tất cả các nhóm này đều cố định ở mức 3.0 – 3.2.
* **Ý nghĩa:** Không có bất kỳ yếu tố hành vi AI hay bối cảnh môi trường nào tạo ra được sự bứt phá hay khác biệt rõ rệt về điểm số. Sinh viên dùng AI để viết nháp, sửa mã nguồn hay lên ý tưởng đều có phổ điểm tương đương nhau, tái khẳng định các biến công nghệ chỉ là nhiễu khi xét trên phương diện tác động tuyến tính đến kết quả học tập.
# 4. Xây dựng mô hình:
## Problem 1: Post-Semester GPA Prediction (Regression)
Mô hình sử dụng:
- `Linear Regression`
- `Decision Tree Regressor`
- `Random Forest Regressor`

## Problem 2: Burnout Risk Level Prediction (Classification)
Mô hình sử dụng:
- `Logistic Regression`
- `Random Forest Classifier`
- `Gradient Boosting Classifier`

## Problem 3: Behavior Clustering (Unsupervised)
Sử dụng thuật toán:
- `K-Means`
# 5. Đánh giá kết quả 

## Problem 1: Post-Semester GPA Prediction

### 1. Phương pháp thực hiện
- **Mục tiêu:** Dự báo điểm trung bình học kỳ sau (`Post_Semester_GPA`) của sinh viên dưới dạng giá trị liên tục (Bài toán Hồi quy - Regression).
- **Biến dự báo (Features):** Bao gồm số giờ dùng AI, số giờ học truyền thống, mức độ phụ thuộc, ngành học, mục đích sử dụng AI,...
- **Thuật toán:** Linear Regression, Decision Tree, Random Forest.

### 2. So sánh hiệu suất mô hình
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

### 3. Kết luận
- Khác với bài toán phân loại mức độ kiệt sức (Burn-Out Risk), các mô hình hồi quy đối với bài toán dự báo điểm số GPA này đạt độ chính xác rất cao, với khả năng giải thích và dự đoán đúng từ 88% đến gần 90% kết quả thực tế.
- Nhìn chung, các mô hình hoạt động ổn định và kiểm soát tốt hiện tượng biến động dữ liệu (ngoại trừ Decision Tree bị Overfitting nhẹ, hai mô hình còn lại không có dấu hiệu sai lệch cấu trúc hay Underfitting).
- Mô hình hoạt động hiệu quả nhất và được đề xuất lựa chọn là **Random Forest** nhờ đạt được chỉ số `Test_R²` cao nhất đồng thời tối thiểu hóa tối đa các lỗi sai số tuyệt đối (`MAE`) và sai số bình phương (`RMSE`).

## Problem 2: Burn-Out Risk Level Prediction
### 1. Phương pháp thực hiện
- **Mục tiêu:** Dự đoán mức độ kiệt sức (Low, Medium, High) của sinh viên.
- **Biến dự báo (Features):** Bao gồm số giờ dùng AI, số giờ học truyền thống, mức độ phụ thuộc, ngành học, mục đích sử dụng AI... (Loại bỏ `Post_Semester_GPA` để tránh rò rỉ dữ liệu).
- **Thuật toán:** Logistic Regression, Random Forest Classifier, Gradient Boosting Classifier.
- **Tối ưu hóa:** Sử dụng `GridSearchCV` với 5-fold Cross-Validation để tinh chỉnh siêu tham số và lựa chọn mô hình tốt nhất thông qua `f1_macro`.
### 2. So sánh hiệu suất mô hình
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
### 3. Kết luận
- Các mô hình không có sự chênh lệch quá nhiều đối với bộ dữ liệu này và chỉ dự đoán đúng được khoảng 52% so với thực tế
- Các mô hình không bị overfitting và có dấu hiệu underfitting
- Trong các mô hình thì mô hình hoạt động hiệu quả nhất là Gradient Boosting Classifier vì đạt được Test F1_score cao nhất

## Problem 3: Behavior Clustering (Unsupervised)
### 1. Nhận xét về việc lựa chọn số cụm
- Trong khi phương pháp Khuỷu tay (Elbow Method) gợi ý số cụm tối ưu là $k = 5$, thì cả hai chỉ số Silhouette Score và Calinski–Harabasz Score đều đồng loạt đạt giá trị cao nhất tại $k = 2$ (lần lượt là **0.2663** và **16,140.6857**).

- Lựa chọn **$k = 2$** là phương án tối ưu nhất cho mô hình K-Means cuối cùng. Lựa chọn này không chỉ đảm bảo cấu trúc phân cụm có độ tách biệt tốt nhất, mô hình đơn giản, dễ diễn giải, mà còn phản ánh đúng bản chất dữ liệu: sinh viên trong tập dữ liệu thực tế đang phân hóa rõ rệt thành hai nhóm hành vi lớn thay vì bị xé lẻ thành nhiều nhóm nhỏ.

### 2. Nhận xét từ heatmap tâm cụm

- Sự khác biệt giữa hai cụm sinh viên được định hình chủ yếu bởi bộ ba đặc trưng: Thời gian sử dụng GenAI (`Weekly_GenAI_Hours`), Mức độ phụ thuộc AI (`Perceived_AI_Dependency`), và Mức độ lo lắng trong kỳ thi (`Anxiety_Level_During_Exams`).

- Cụm 0 đại diện cho nhóm sinh viên lạm dụng và bị lệ thuộc nặng nề vào AI, đi kèm với tâm lý lo lắng thi cử lớn. Ngược lại, Cụm 1 đại diện cho nhóm sinh viên kiểm soát tốt giữa việc học tập truyền thống và sự hỗ trợ của A.I.

- Số lượng công cụ A.I sử dụng của cả hai cụm gần như trùng khớp tuyệt đối ở mức trung bình 2.81 và 2.80. Điều này cho thấy số lượng loại công cụ AI được sử dụng không có giá trị phân loại trong việc hình thành phân cụm. Bản chất của sự phân hóa sinh viên nằm ở **thời lượng sử dụng và mức độ phụ thuộc A.I**, chứ không phải số lượng công cụ nhiều hay ít.

### 3. Hành vi của từng cụm
- Bộ dữ liệu phân hóa thành hai phân khúc rõ rệt với quy mô chênh lệch lớn: Cụm 1 chiếm đại đa số với **73.90%** (36,948 sinh viên), trong khi Cụm 0 chiếm thiểu số với **26.10%** (13,052 sinh viên). Điểm trung bình `Post_Semester_GPA` của nhóm 0 là 3.33 thấp hơn điểm của cụm 1(3.36)
- Việc sử dụng AI ở mức độ kiểm soát cao vẫn là xu hướng chủ lưu trong môi trường giáo dục (Cụm 1). Tuy nhiên, Cụm 0 sở hữu quy mô lên tới hơn 13,000 sinh viên, chứng minh đây không phải là nhóm ngoại lệ.

- Cụm 0 – Nhóm "Lệ thuộc công nghệ và Áp lực tâm lý cao"
  - Sinh viên Cụm 0 dùng AI với cường độ cực cao (**18.64 giờ/tuần**), có mức phụ thuộc AI (**5.60**) và lo lắng phòng thi (**5.80**) vượt trội. Ngược lại, thời gian học truyền thống bị thu hẹp đáng kể (**9.54 giờ/tuần**).
  - Đây là  nhóm sinh viên thay vì dành thời gian tự học truyền thống thì lại dành thời lượng tương tác với AI. Sự xuất hiện đồng thời của ba yếu tố "dùng nhiều – phụ thuộc cao – lo lắng" là dấu hiệu đáng lo ngại về rủi ro tâm lý và burnout trong kỷ nguyên AI.

- Cụm 1 – Nhóm "Làm chủ công cụ và Học tập cân bằng"
  - Chiếm gần 3/4 dữ liệu, sinh viên Cụm 1 chỉ sử dụng GenAI ở mức bổ trợ (**4.82 giờ/tuần**), giữ mức phụ thuộc AI rất thấp (**2.77**) và tâm lý phòng thi khá ổn định (**3.73**). Đồng thời, họ duy trì thời gian học truyền thống tốt hơn (**11.80 giờ/tuần**).
  - Nhóm này đại diện cho mô hình học tập lành mạnh: coi AI là công cụ hỗ trợ thứ yếu thay vì giải pháp thay thế. Khoảng cách chênh lệch lên tới **13.82 giờ AI/tuần** và **2.26 giờ tự học/tuần** so với Cụm 0.

### 4. Tổng hợp kết quả

Kết quả K-Means cho thấy sinh viên trong bộ dữ liệu có thể được chia thành hai xu hướng hành vi chính. Nhóm thứ nhất sử dụng GenAI với cường độ cao, phụ thuộc AI nhiều hơn, học truyền thống ít hơn và có mức lo lắng khi thi cao hơn. Nhóm thứ hai sử dụng AI ít hơn, ít phụ thuộc hơn, có thời gian học truyền thống cao hơn và chiếm phần lớn số sinh viên.

Các đặc trưng phân biệt hai nhóm mạnh nhất là thời gian sử dụng GenAI, mức phụ thuộc AI và mức lo lắng trong kỳ thi. Ngược lại, mức đa dạng công cụ AI gần như không tạo ra khác biệt giữa hai cụm.

Mô hình với (k=2) tạo ra cách phân chia đơn giản, có ý nghĩa và dễ diễn giải. Tuy vậy, do Silhouette Score chưa cao và biểu đồ PCA vẫn có một phần chồng lấn, các cụm nên được xem là những nhóm hành vi tương đối, không phải các nhãn cố định hoặc đánh giá sinh viên theo hướng tốt và xấu.

# 6. Kết luận và hướng phát triển
## Kết luận:

### 1. Công cụ A.I không tác động đến điểm số

* **Nội dung:** Kết quả từ mô hình hồi quy dự báo GPA (`R²` đạt gần 90%) khẳng định phong độ đầu kỳ (`Pre_Semester_GPA`) cùng các yếu tố nội tại như năng lực giữ vững kiến thức (`Skill_Retention_Score`) và thời gian tự học (`Traditional_Study_Hours`) mới là những biến quyết định điểm số cuối kỳ. Trái lại, thời lượng hay số lượng công cụ AI sử dụng hoàn toàn không có mối tương quan đối với việc tăng hay giảm GPA.
* **Ý nghĩa:** Trí tuệ nhân tạo tạo sinh (GenAI) trong bối cảnh giáo dục hiện nay chỉ đóng vai trò là một công cụ bổ trợ, không phải là một giải pháp thay thế cho năng lực tư duy độc lập và nỗ lực học tập tự thân của sinh viên

### 2. Sự phân hóa hành vi rõ rệt 

* **Nội dung:** Mô hình phân cụm K-Means ($k=2$) đã phác họa thành công hai hành vi hoàn toàn đối lập trong môi trường học đường. Nhóm 1 (chiếm **73.90%**) thể hiện mô hình học tập cân bằng khi làm chủ công cụ và chỉ dùng AI ở mức bổ trợ (4.82 giờ/tuần). Tuy nhiên, một bộ phận không nhỏ (Nhóm 0 - chiếm **26.10%**, tương đương hơn 13,000 sinh viên) đang lạm dụng AI cực đoan (18.64 giờ/tuần) và đánh đổi thời gian tự học truyền thống. Bên cạnh đó, điểm trung bình của nhóm 1 cũng cao hơn nhóm 0 `0.03`.
* **Ý nghĩa:** Quy mô của Cụm 0 chứng minh hiện tượng lạm dụng công nghệ đã mang tính hệ thống, đặt ra yêu cầu cấp bách cho các nhà quản lý giáo dục trong việc định hướng và đào tạo kỹ năng sử dụng AI một cách thông minh cho sinh viên.

### 3. Ảnh hưởng của việc lạm dụng công nghệ đối với sức khỏe tinh thần
* **Nội dung:** Dữ liệu chỉ ra một mối liên kết chặt chẽ mang tính hệ quả: việc tăng thời lượng dùng AI tỷ lệ thuận với mức độ lệ thuộc tâm lý (tương quan 0.67), và sự lệ thuộc này chuyển hóa trực tiếp thành áp lực lo lắng cực đoan khi bước vào phòng thi (nơi sinh viên buộc phải tự lực). Sự kết hợp giữa việc dùng AI cho các tác vụ tư duy nặng (như `Debugging`, `Copywriting`) và sự buông bỏ học tập truyền thống chính là tác nhân đẩy sinh viên vào trạng thái quá tải, kiệt sức.
* **Ý nghĩa:** Đây là phát hiện đắt giá nhất về mặt tâm lý học đường, cảnh báo rằng việc lạm dụng AI không những không làm giảm tải áp lực học tập mà trái lại, đang tạo ra những tổn hại vô hình đối với sức khỏe tinh thần của người học.

## 6. Hướng cải thiện
### 1. Feature Engineering từ kết quả phân cụm
* Tận dụng kết quả từ mô hình K-Means bằng cách đưa nhãn cụm (`Cluster_ID`) làm một biến đầu vào (Feature) cho các mô hình phân loại Burnout. Ngoài ra, cần tạo ra các biến tương tác phi tuyến tính phản ánh đúng hành vi của sinh viên nhằm giúp các mô hình phân loại (đặc biệt là Gradient Boosting) có thêm các đặc trưng mạnh để phân loại mức độ kiệt sức, khắc phục hiện tượng Underfitting hiện tại.

### 2. Xử lý đa cộng tuyến và lựa chọn đặc trưng (Feature Selection)
- Phân tích tương quan đã chỉ ra hiện tượng đa cộng tuyến cực kỳ nghiêm trọng giữa `Pre_Semester_GPA` và `Post_Semester_GPA` (0.93). Trong các bước tiếp theo, đối với bài toán Hồi quy, cần:
- Áp dụng các phương pháp giảm chiều dữ liệu như PCA (Principal Component Analysis) hoặc các mô hình hồi quy có phạt như Ridge/Lasso Regression để tự động triệt tiêu các biến nhiễu công nghệ có điểm Mutual Information thấp.
- Tối ưu hóa trọng số của mô hình Linear Regression, giúp mô hình ổn định hơn và giải thích tường minh hơn đóng góp của các biến còn lại.

### 3. Thu thập thêm dữ liệu định tính và áp dụng các thuật toán nâng cao cho bài toán Burnout
- Vì bài toán dự báo mức độ kiệt sức (`Burnout_Risk_Level`) rất phức tạp và liên quan đến tâm lý, việc chỉ sử dụng các biến số lượng (giờ giấc, điểm số) là chưa đủ.
- Thu thập thêm các biến định tính sâu hơn như: Áp lực từ gia đình, số lượng tín chỉ đăng ký trong học kỳ, hoặc thời gian ngủ trung bình của sinh viên.
- Thử nghiệm các thuật toán mạnh mẽ hơn trong việc học các mối quan hệ phi tuyến phức tạp như **LightGBM**, **XGBoost**, hoặc mạng thần kinh nhân tạo (**Multi-Layer Perceptron - MLP**), kết hợp với việc xử lý mất cân bằng dữ liệu (nếu có).

