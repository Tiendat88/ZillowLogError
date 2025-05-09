Dự án Dự đoán Sai số Log Giá Nhà Zillow
Tổng quan
Dự án này xây dựng mô hình dự đoán sai số log (logerror) giữa giá ước lượng của Zillow (Zestimate) và giá bán thực tế (SalePrice) của các căn nhà, được định nghĩa là:

logerror = log(Zestimate) - log(SalePrice).

Mục tiêu là hỗ trợ cải thiện độ chính xác của các ước lượng giá nhà bằng cách phân tích dữ liệu bất động sản từ Zillow. Dự án sử dụng PySpark để xử lý dữ liệu lớn, mô hình hồi quy tuyến tính để dự đoán, và giao diện Tkinter để tra cứu kết quả dự đoán.

Tính năng
Tiền xử lý dữ liệu:
Kết hợp dữ liệu giao dịch (train_2016_v2.csv, train_2017.csv) và thuộc tính bất động sản (properties_2016.csv, properties_2017.csv).
Xử lý giá trị ngoại lệ trong logerror bằng Z-score (thay thế giá trị vượt ±3 độ lệch chuẩn bằng giá trị trung bình).
Mã hóa các cột định tính (propertycountylandusecode, propertyzoningdesc) bằng StringIndexer.
Trích xuất đặc trưng thời gian (năm, tháng, ngày) từ transactiondate.
Xây dựng mô hình:
Sử dụng hồi quy tuyến tính (LinearRegression) để dự đoán logerror.
Tối ưu hóa siêu tham số bằng CrossValidator với ParamGridBuilder.
Đánh giá mô hình:
Tính Sai số Tuyệt đối Trung bình (MAE) và Sai số Bình phương Trung bình Căn (RMSE).
Kết quả: MAE ~0.0545, RMSE ~0.0887 (sau tối ưu hóa).
Giao diện tra cứu: Giao diện Tkinter cho phép nhập năm và tháng để dự đoán trung bình logerror.
Bộ dữ liệu
Files:
properties_2016.csv, properties_2017.csv: Chứa 58 cột thuộc tính bất động sản (diện tích, số phòng, năm xây, giá trị thuế, v.v.), ~2.98M dòng mỗi file.
train_2016_v2.csv, train_2017.csv: Chứa parcelid, logerror, và transactiondate, lần lượt 90,275 và 77,613 dòng.
Cột chính:
parcelid: Mã định danh bất động sản.
logerror: Sai số log giữa giá ước lượng và giá thực tế.
transactiondate: Ngày giao dịch.
Các cột thuộc tính như bathroomcnt, bedroomcnt, yearbuilt, taxvaluedollarcnt, v.v.
Yêu cầu
Để chạy dự án, cài đặt các gói Python sau:

bash

Sao chép
pip install pyspark pandas numpy matplotlib seaborn tkinter
Lưu ý: Cần cài đặt Apache Spark để sử dụng PySpark. Hướng dẫn cài đặt Spark: Apache Spark Documentation.

Cài đặt
Tải repository hoặc các file dự án.
Đặt các file dữ liệu (properties_2016.csv, properties_2017.csv, train_2016_v2.csv, train_2017.csv) vào thư mục dự án (hoặc cập nhật đường dẫn trong mã).
Cài đặt các gói phụ thuộc được liệt kê ở phần Yêu cầu.
Đảm bảo môi trường Spark được cấu hình đúng.
Hướng dẫn sử dụng
Mở file Jupyter Notebook zillow_home_Apolo_ver2.ipynb.
Chạy lần lượt các ô mã để:
Tải và tiền xử lý dữ liệu.
Xử lý giá trị ngoại lệ và mã hóa dữ liệu.
Huấn luyện mô hình hồi quy tuyến tính với tối ưu hóa siêu tham số.
Đánh giá mô hình bằng MAE và RMSE.
Khởi chạy giao diện Tkinter để tra cứu dự đoán logerror theo tháng và năm.
Kết quả:
File model_results.txt và model_results_cross.txt lưu MAE và RMSE.
Giao diện Tkinter cho phép nhập năm/tháng để xem trung bình logerror dự đoán.
Kết quả đầu ra
Đánh giá mô hình:
MAE ban đầu: ~0.0547.
RMSE ban đầu: ~0.0891.
MAE sau tối ưu hóa: ~0.0545.
RMSE sau tối ưu hóa: ~0.0887.
Giao diện tra cứu: Hiển thị trung bình logerror dự đoán cho tháng và năm được nhập.
File kết quả:
model_results.txt: Lưu MAE và RMSE của mô hình ban đầu.
model_results_cross.txt: Lưu MAE và RMSE của mô hình sau tối ưu hóa.
Hạn chế và Cải tiến
Hạn chế:
Mô hình hồi quy tuyến tính có thể không nắm bắt được các mối quan hệ phi tuyến trong dữ liệu.
Dữ liệu có nhiều giá trị thiếu, ảnh hưởng đến hiệu suất mô hình.
Cải tiến:
Thử các mô hình phức tạp hơn như Random Forest, Gradient Boosting, hoặc XGBoost.
Xử lý giá trị thiếu bằng cách điền giá trị trung bình, trung vị, hoặc sử dụng mô hình dự đoán.
Thêm các đặc trưng mới như tỷ lệ giữa taxvaluedollarcnt và lotsizesquarefeet.