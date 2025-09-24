Đây là một bài tập nhỏ để ứng dụng khả năng dự đoán của mô hình linear regression. 

Kết quả khi sử dụng mô hình linear regression cũng khá ổn ( thực tế rằng bộ dữ liệu này được thiết kế để làm theo thuật toán linear regression). Và dataset này toàn bộ đều là dữ liệu đã được làm sạch cho nên ta không phải xử lí các missing data. 

Đây là kết quả của chúng sau khi train model 

<div style="text-align: center;">
  <img width="333" height="204" alt="image" 
       src="https://github.com/user-attachments/assets/9ed7c3d6-f38b-4456-834a-bf1b2eeed283" />
</div>

I. Bước chuẩn bị 
+ Việc chọn feature để training model : chọn các feature không được lan man ( không liên quan đế label ta cần dự đoán ), để làm được việc đó thì ta có ma trận tương quan, tìm hiểu xem những feature nào ảnh hưởng nhiều nhất đến label dự đoán khi thay đổi các feature đó ( hay còn gọi là sự phụ thuộc của label vào các feature). Từ đó ta kết luận được những feature nào ảnh hướng nhiều đến mô hình và loại bỏ những feature không ảnh hưởng nhiều, nhằm tối ưu hóa tài nguyên.

<img width="856" height="663" alt="image" src="https://github.com/user-attachments/assets/a0b43f07-678b-45b5-824c-1e7652d9ad4e" />

+ Sau cùng là một vài kĩ thuật đơn giản để xử lí dữ liệu sau đó tiến hành training model ( encoding , ....)

II. Hiểu biết về mô hình 
1. Khái niệm

Hồi quy tuyến tính là một thuật toán thống kê và Machine Learning dùng để dự đoán một biến liên tục (biến mục tiêu 
𝑦
y) dựa trên một hoặc nhiều biến đầu vào (features 
𝑥
x).
Ý tưởng: mô hình hóa mối quan hệ tuyến tính giữa đầu vào và đầu ra.

Ví dụ: dự đoán giá nhà dựa trên diện tích, số phòng, vị trí…

<!doctype html>
<html lang="vi">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Công thức Linear Regression</title>

  <!-- MathJax để render công thức LaTeX -->
  <script>
    window.MathJax = {
      tex: { inlineMath: [['$', '$'], ['\\(', '\\)']] },
      svg: { fontCache: 'global' }
    };
  </script>
  <script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js" defer></script>

  <style>
    :root{
      --bg:#0f1113;
      --muted:#bfc7cc;
      --accent:#ffffff;
      --maxw:900px;
    }
    html,body{
      height:100%;
      margin:0;
      background:linear-gradient(180deg,#0b0c0d 0%, #101214 100%);
      color:var(--accent);
      font-family: "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
    }
    .container{
      max-width:var(--maxw);
      margin:48px auto;
      padding:32px;
    }
    h2{
      margin:0 0 18px 0;
      font-size:28px;
    }
    .section{
      background:rgba(255,255,255,0.03);
      padding:22px;
      border-radius:10px;
      box-shadow: 0 6px 18px rgba(0,0,0,0.6);
      margin-bottom:32px;
    }
    .bullet-list{
      margin:18px 0 0 0;
      padding-left:24px;
      color:var(--muted);
      font-size:16px;
      line-height:1.6;
    }
    .formula {
      text-align:center;
      margin:20px 0;
    }
    .formula .line {
      display:inline-block;
      background:rgba(255,255,255,0.02);
      padding:12px 18px;
      border-radius:8px;
      font-size:22px;
    }
    .sub-bullets{
      margin-top:12px;
      padding-left:18px;
      color:var(--muted);
      font-size:15px;
    }
    .small{
      color:var(--muted);
      font-size:14px;
    }
    hr{
      border: none;
      border-top:1px solid rgba(255,255,255,0.1);
      margin:24px 0;
    }
  </style>
</head>
<body>
  <main class="container">
    <!-- Phần 2 -->
    <div class="section">
      <h2>2. Công thức cơ bản</h2>
      <ul class="bullet-list">
        <li>
          <strong>Hồi quy tuyến tính đơn (1 biến đầu vào):</strong>
          <div class="formula">
            <div class="line">
              \( y = \beta_0 + \beta_1 x + \varepsilon \)
            </div>
          </div>
          <ul class="sub-bullets">
            <li><em>y</em>: giá trị dự đoán (output)</li>
            <li><em>x</em>: biến đầu vào (input)</li>
            <li><em>β₀</em>: hệ số chặn (intercept)</li>
            <li><em>β₁</em>: hệ số góc (slope)</li>
            <li><em>ε</em>: sai số</li>
          </ul>
        </li>

        <li style="margin-top:16px;">
          <strong>Hồi quy tuyến tính đa biến (nhiều biến đầu vào):</strong>
          <div class="formula">
            <div class="line">
              \( y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \cdots + \beta_p x_p + \varepsilon \)
            </div>
          </div>
          <p class="small">(Trong đó \(p\) là số biến đầu vào)</p>
        </li>
      </ul>
    </div>

    <!-- Phần 3 + 4 -->
    <div class="section">
      <h2>3. Mục tiêu mô hình</h2>
      <p>Tìm các hệ số \( \beta_0, \beta_1, \ldots \) sao cho <strong>tổng bình phương sai số nhỏ nhất</strong> (Least Squares):</p>
      <div class="formula">
        <div class="line">
          Minimize \( \sum (y_i - \hat{y}_i)^2 \)
        </div>
      </div>

      <hr>

      <h2>4. Các giả định của Linear Regression</h2>
      <ul class="bullet-list">
        <li>Quan hệ tuyến tính giữa \(x\) và \(y\).</li>
        <li>Sai số độc lập và phân phối chuẩn.</li>
        <li>Độ phân tán sai số không đổi (homoscedasticity).</li>
        <li>Không có đa cộng tuyến nghiêm trọng giữa các biến độc lập.</li>
      </ul>
    </div>

    <!-- Phần 5 -->
    <div class="section">
      <h2>5. Đánh giá mô hình</h2>
      <ul class="bullet-list">
        <li>\(R^2\) (coefficient of determination) – mức độ giải thích của mô hình.</li>
        <li><strong>MSE / RMSE</strong> – trung bình bình phương sai số.</li>
      </ul>
    </div>
  </main>
</body>
</html>



