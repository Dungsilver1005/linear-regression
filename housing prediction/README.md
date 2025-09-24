Đây là một bài tập nhỏ để ứng dụng khả năng dự đoán của mô hình linear regression. 

Kết quả khi sử dụng mô hình linear regression cũng khá ổn ( thực tế rằng bộ dữ liệu này được thiết kế để làm theo thuật toán linear regression). Và dataset này toàn bộ đều là dữ liệu đã được làm sạch cho nên ta không phải xử lí các missing data. 

Đây là kết quả của chúng sau khi train model 

<img width="333" height="204" alt="image" src="https://github.com/user-attachments/assets/9ed7c3d6-f38b-4456-834a-bf1b2eeed283" />

+ Việc chọn feature để training model : chọn các feature không được lan man ( không liên quan đế label ta cần dự đoán ), để làm được việc đó thì ta có ma trận tương quan, tìm hiểu xem những feature nào ảnh hưởng nhiều nhất đến label dự đoán khi thay đổi các feature đó ( hay còn gọi là sự phụ thuộc của label vào các feature). Từ đó ta kết luận được những feature nào ảnh hướng nhiều đến mô hình và loại bỏ những feature không ảnh hưởng nhiều, nhằm tối ưu hóa tài nguyên.

<img width="856" height="663" alt="image" src="https://github.com/user-attachments/assets/a0b43f07-678b-45b5-824c-1e7652d9ad4e" />

+ Sau cùng là một vài kĩ thuật đơn giản để xử lí dữ liệu sau đó tiến hành training model ( encoding , ....)
