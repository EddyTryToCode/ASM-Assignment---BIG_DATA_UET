# ASM Assignment - Big Data UET

# 📊 Stock Price BigData (Vietnam Stock Market Analysis)

## 📘 Giới thiệu
Dự án này mô phỏng hệ thống **phân tích và xử lý dữ liệu lớn** cho bài toán chứng khoán Việt Nam.  
Hệ thống được triển khai dựa trên **Hadoop**, **Spark**, và **Jupyter (PySpark)** trong môi trường **Docker**.

Mục tiêu:
- Xây dựng pipeline Big Data để xử lý dữ liệu chứng khoán Việt Nam.  
- Phân tích, trực quan hoá biến động giá cổ phiếu.  
- Huấn luyện mô hình **LSTM** để dự báo xu hướng giá.

---

## ⚙️ Kiến trúc hệ thống
Hệ thống mô phỏng cụm Big Data bao gồm:
- **1 Namenode + 4 Datanode** (HDFS)
- **1 Spark Master + 4 Spark Worker**
- **1 Jupyter Notebook container** để thực hiện phân tích bằng PySpark.

Docker images sử dụng:  
`bde2020/hadoop`, `bde2020/spark`, `jupyter/pyspark-notebook`.

---

## 📂 Dữ liệu
Nguồn dữ liệu: **API `vnstock`** (PyPI)  
Bao gồm hơn **1600 mã cổ phiếu** từ các sàn HOSE và HNX, ví dụ:
`VIC`, `VNM`, `VCB`, `HPG`, `SSI`, `CII`.

Định dạng: `.csv`  
Các cột chính: `Time`, `Open`, `High`, `Low`, `Close`, `Volume`

Lệnh tải dữ liệu lên HDFS:
```bash
hdfs dfs -mkdir -p /user/root/vn_stock/
hdfs dfs -put stock_data_VIC.csv /user/root/vn_stock/
```

## 📊 Phân tích dữ liệu

Thực hiện trong file **`Stock_price_demo-Copy2.ipynb`**

1. **Đọc dữ liệu từ HDFS bằng PySpark.**  
2. **Tiền xử lý:**
   - Tạo cột `Mean = (High + Low)/2`
   - Tính biến động ngày `Change = (Close/Close.shift(1)) - 1`
3. **Chuyển sang Pandas để trực quan hóa:**
   - Biểu đồ giá trung bình (Mean)
   - Biểu đồ phân phối lợi suất (Histogram, KDE)
4. **So sánh biến động giữa 5 mã lớn:** `VIC`, `VNM`, `VCB`, `HPG`, `SSI`

---

## 🤖 Mô hình dự báo LSTM

Huấn luyện mô hình LSTM dự báo giá cổ phiếu **CII** (Hạ tầng Kỹ thuật TP.HCM).

**Thông tin huấn luyện:**
- Framework: TensorFlow/Keras  
- 4 lớp LSTM + Dropout  
- Epochs: 100  
- Batch size: 32  
- Dữ liệu: 2012–2025 (Train 2012–2023, Test 2024–2025)

**Kết quả:**
- Mô hình bám sát xu hướng giá thực tế.  
- Nhận diện được các giai đoạn tăng mạnh.  
- Có độ trễ nhỏ (lag) đặc trưng của chuỗi thời gian.

---

## 📈 Kết luận

- Hệ thống Big Data chạy ổn định trong Docker.  
- Pipeline xử lý dữ liệu và dự báo giá hoạt động hoàn chỉnh.  
- Mô hình LSTM thể hiện tiềm năng ứng dụng thực tế cho thị trường chứng khoán Việt Nam.  

---

## 📚 Tài liệu tham khảo

1. [Big Data Europe – Docker Hadoop & Spark](https://github.com/big-data-europe/docker-hadoop)  
2. [Stock Price BigData – Thviet79](https://github.com/thviet79/Stock-Price)  
3. [VN Stock PyPI](https://pypi.org/project/vnstock/)  
4. [Apache Spark Docs](https://spark.apache.org/docs/latest/)  
5. [Jason Brownlee – LSTM Time Series Forecasting](https://machinelearningmastery.com/time-series-prediction-lstm-recurrent-neural-networks-python-keras/)

---

## 💻 Repository

📍 **GitHub:** [https://github.com/EddyTryToCode/ASM-Assignment---BIG_DATA_UET](https://github.com/EddyTryToCode/ASM-Assignment---BIG_DATA_UET)

---

## 👤 Tác giả

**Hoàng Minh Quyền**  
📘 MSSV: 23020421  
🎓 Lớp: K68A-AI1  
🏫 Trường Đại học Công nghệ – Đại học Quốc gia Hà Nội (UET)

