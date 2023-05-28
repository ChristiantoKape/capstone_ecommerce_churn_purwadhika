Capstone Project 3 - E-Commerce Customer Churn
-------------------------
Christianto Kurniawan P - JCDSOL-009-010

Business Problem Understanding
------------------------------------------------------------------------------------
**Context**
E-commerce customer churn, atau bisa disebut sebagai kehilangan pelanggan dalam bisnis e-commerce, merupakan sebuah fenomena dimana seorang pelangan menghentikan interaksinya dengan sebuah situs atau toko online setelah melakukan transaksi atau melakukan interaksi yang tidak diinginkan dengan situs tersebut. Fenomena ini merupakan masalah yang serius bagi banyak perusahaan e-commerce karena dapat mengurangi pendapatan dan keuntungan mereka. 

Oleh karena itu, sebuah perusahaan e-commerce ingin mengetahui pelanggan yang ingin melakukan pemberhentian (churn) dan mengurangi jumlah pelanggan yang churn. Dilakukan sebuah model prediksi yang tepat untuk menentukan pelanggan yang berhenti berlangganan (churn) atau tidak menggunakan machine learning. Dengan target yang ditentukan sebagai berikut:

- 0 : Customer tidak churn
- 1 : Customer churn

**Problem Statement**
Churn pelanggan dalam bisnis e-commerce merupakan masalah serius yang signifikan dalam jangka panjang, karena dapat berdampak negatif terhadap pertumbuhan dan profitabilitas bisnis. Menurut sumber yang dikutip, biaya yang dikeluarkan untuk mencari customer baru berkisar antara 45 - 50 USD, sedangkan biaya untuk mempertahankan customer sebesar 20 USD. Oleh karena itu, perusahaan e-commerce perlu memahami akar penyebab churn dan mengambil tindakan yang tepat untuk mencegahnya. Dengan demikian, permasalahan yang perlu dipecahkan adalah bagaimana mengurangi churn pelanggan secara efektif dalam bisnis e-commerce dan menjaga retensi pelanggan agar terjamin pertumbuhan dan profitabilitas jangka panjang.

**Goals**
Dalam rangka mengatasi permasalahan churn pelanggan. Perusahaan memiliki beberapa tujuan, yaitu meningkatkan kepuasan pelanggan, mengurangi penyebab churn, meningkatkan loyalitas pelanggan, meningkatkan retensi pelanggan, dan meningkatkan pertumbuhan bisnis jangka panjang

**Analytics Approach**
Jadi yang akan dilakukan adalah menganalisis faktor pembeda dari pelanggan yang mekalukan *Churn* atau tidak. Selanjutnya akan dibuat model klasifikasi yang akan membantu perusahaan untuk mempertahankan customer yang akan churn

**Metric Evaluation**
	        | N-Prediction |  P-Prediction |
--- | --- | --- |
N-Actual  | TN	         |  FP |
P-Actual  | FN	         |  TP |

False Positive (FP) : pelanggan dianggap sudah churn padahal tidak, Konsekuensinya: perusahaan akan kehilangan pelanggan yang masih aktif

Flase Negative (FN) : pelanggan dianggap tidak churn padahal churn, Konsekuensinya: perusahaan akan kehilangan pelanggan yang sebenarnya sudah churn

Berdasarkan konsekuensi tersebut akan dibuat model yang akan mengoptimalkan biaya promosi yang hanya di tujukan ke customer yang memiliki kecenderungan untuk churn dan memutuskan untuk tidak churn. Sehingga, metrics yang cocok digunakan pada model ini adalah **ROC_AUC**


Data Understanding
------------------------------------------------------------------------------------
**Attribute Information**
| Attribute | Data Type | Description |
| --- | --- | --- |
| Tenure | Float | Tenure of a customer in the company |
| WarehouseToHome | Float | Distance between the warehouse to the customer’s home |
| NumberOfDeviceRegistered | Int | Total number of deceives is registered on a particular customer |
| PreferedOrderCat | Object | Preferred order category of a customer in the last month |
| SatisfactionScore | Int | Satisfactory score of a customer on service |
| MaritalStatus | Object | Marital status of a customer |
| NumberOfAddress | Int | Total number of added on a particular customer |
| Complain | Int | Any complaint has been raised in the last month |
| DaySinceLastOrder | Float | Day since last order by customer |
| CashbackAmount | Float | Average cashback in last month |
| Churn | Int | Churn flag |


Data Cleanng
------------------------------------------------------------------------------------
Kita memiliki missing value pada 194 baris pada kolom Tenure, 169 missing value pada kolom WarehouseToHome, 213 missing value pada kolom DaySinceLastOrder
  1. Menggabungkan Phone dan Mobile Phone menjadi Mobile Phone
  2. Boxplot Missing
  3. Heatmap Data Correlation
  4. Drop Data Duplikat
  5. Handling Missing Value
      Pada pengisian missing values ini menggunakan metode SimpleImputer(Median)


Data Analysis
------------------------------------------------------------------------------------
  1. **Categorical Features**
      Kolom yang termasuk dalam Categorical Features yaitu 'PreferedOrderCat' dan 'MaritalStatus'
  2. **Numerical Features**
      Kolom yang termasuk dalam Numerical Features yaitu 'Tenure', 'WarehouseToHome', 'NumberOfDeviceRegistered', 'SatisfactionScore', 'NumberOfAddress', 'Complain', 'DaySinceLastOrder', 'CashbackAmount'.


Data Preparation
------------------------------------------------------------------------------------
  1. **Data Splitting**
      Pada splitting, kita menggunakan 20% test size dan stratify=y. fungsi stratify digunakan untuk memastikan bahwa distribusi kelas dalam variabel target tetap seimbang antara set pelatihan dan pengujian.
  2. **Modeling**
      Pada modeling, kita menggunakan LogisticRegression, DecisionTreeClassifier, KNeighborsClassifier, XGBClassifier, RandomForestClassifier.
  3. **Model Benchmarking: K-Fold**
      Model Benchmarking dengan nilai ROC_AUC yang tertinggi adalah XGBoost Classifier dan Random Forest Classifier
  4. **Model Benchmarking: Data Testing**
      Model Benchmarking dengan nilai ROC_AUC yang tertinggi adalah XGBoost Classifier
  5. **Oversampling Test**
      Pada oversampling, kita menggunakan metode SMOTE(Synthetic Minority Over-sampling Technique). Merupakan suatu metode yang umum digunakan dalam pemrosesan data tidak seimbang (imbalanced data).
  6. **Hyperparameter Tuning**
      Hyperparameter Tuning kali ini menggunakan teknik GridSearchCV. Teknik ini digunakan untuk mencari nilai parameter yang optimal dari dataset yang diberikan dalam bentuk grid.
  7. **Feature Importance**
      Pada teknik ini, digunakan untuk mencari feature importance pada dataset.


Conclusion dan Recommendation
------------------------------------------------------------------------------------
**Conclusion**
Berdasarkan hasil classification report dengan metode Machine Learning, XGBoost Classifier. Dapat disimpulkan bahwa model dapat mengetahui 92% customer yang tidak churn dan 77% customer yang churn berdasarkan recall. Dan berdasarkan nilai prediksi, model memiliki kemungkinan customer churn sebesar 64%, sehingga masih ada customer tidak churn dan diprediksi sebagai churn (False Positive Rate) sebesar 7%
Berdasarkan sumber, biaya yang dikeluarkan jika harus mendapatkan 1 customer berkisar antara 50 USD, sedangkan biaya yang digunakan untuk mempertahankan 1 customer berkisar antara 20 USD

**Recommendation**
For Bussiness: 
1. Perusahaan dapat memberikan vocer gratis ongkos kirim pada customer yang berpotensi churn
2. Perusahaan dapat membuat marketing campaign yang lebih segmented seperti kategori pesanan yang disukai, berapa lama langganan customer.
3. Mengembangkan fitur pada aplikasi e-commerce seperti permainan atau live dari toko yang disukai. Dan memberikan poin untuk setiap pembelian yang bisa digunakan kembali untuk belanja

For Model:
1. Menambahkan fitur lain terkait faktor churn, sehigga dapat dilihat faktor-faktor yang mempengaruhi customer churn.
2. Menghilangkan outlier, agar bisa dilihat apakah outlier mempengaruhi hasil secara signifikan atau tidak
3. Melakukan uji pada model Machine Learning dan Hypertuning kembali.
