# Báo cáo kết quả benchmark LightGBM trên CPU

**Học viên:** Trần Hoàng Mai Anh - 2A202601324

Bài lab được thực hiện trên máy CPU `t3.micro` với bộ dữ liệu 284.807 giao dịch và 30 đặc trưng.
Thời gian nạp dữ liệu là 2,62 giây, còn thời gian huấn luyện LightGBM là 5,58 giây.
Kết quả này cho thấy mô hình có thể huấn luyện khá nhanh trên cấu hình tài nguyên hạn chế.
AUC-ROC đạt 0,7551, cho thấy khả năng phân biệt giao dịch gian lận ở mức khá.
Accuracy đạt 0,9975 nhưng F1-Score chỉ 0,4496, Precision 0,3625 và Recall 0,5918. Kết quả trên phản ánh đúng thực tế performance trên bộ dữ liệu mất cân bằng nhãn. Với bộ dữ liệu này, Accuracy không phải một metric đáng tin, muốn tiếp tục cải thiện model, cần tập trung tối ưu F1-score, Precision và Recall.
Độ trễ dự đoán một dòng là khoảng 1,70 ms; với 1.000 dòng, thời gian là 0,00571 giây, tương đương khoảng 175.119 dòng/giây.
Nhìn chung, mô hình Light GBM đáp ứng tốt yêu cầu inference nhanh trên CPU, AUC và Recall vẫn có thể cải thiện bằng tinh chỉnh tham số và xử lý mất cân bằng dữ liệu. Một số kỹ thuật nên thử trước tiên là dùng scale_pos_weight để điều chỉnh trọng số, dùng focal loss để ưu tiên mẫu khó, tuning decision threshold thay vì mặc định 0.5,...
