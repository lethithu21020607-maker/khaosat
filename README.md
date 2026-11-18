# khaosat
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Phiếu khảo sát ý kiến</title>
  <style>
    :root { --primary: #2563eb; --bg: #f3f6fb; --text: #172033; }
    * { box-sizing: border-box; }
    body {
      margin: 0; padding: 32px 16px; background: var(--bg);
      color: var(--text); font: 16px/1.6 system-ui, sans-serif;
    }
    main {
      max-width: 720px; margin: auto; padding: 32px;
      background: white; border-radius: 18px;
      box-shadow: 0 12px 36px rgba(20, 40, 80, .09);
    }
    h1 { margin: 0 0 8px; font-size: clamp(1.6rem, 4vw, 2.2rem); }
    .intro { color: #64748b; margin: 0 0 28px; }
    fieldset { border: 0; border-top: 1px solid #e5eaf2; padding: 22px 0 8px; margin: 0; }
    legend { padding: 0 0 12px; font-weight: 700; }
    label.option { display: flex; gap: 10px; align-items: flex-start; margin: 10px 0; cursor: pointer; }
    input[type="text"], input[type="email"], select, textarea {
      width: 100%; padding: 12px 14px; border: 1px solid #cbd5e1;
      border-radius: 10px; font: inherit; background: white;
    }
    textarea { min-height: 110px; resize: vertical; }
    .field-label { display: block; font-weight: 600; margin: 14px 0 7px; }
    button {
      width: 100%; border: 0; border-radius: 10px; padding: 14px 18px;
      margin-top: 22px; background: var(--primary); color: white;
      font: inherit; font-weight: 700; cursor: pointer;
    }
    button:hover { background: #1d4ed8; }
    #notice { margin-top: 14px; color: #166534; font-weight: 600; }
    .hint { font-size: .9rem; color: #64748b; }
    @media (max-width: 520px) { main { padding: 22px 18px; } }
  </style>
</head>
<body>
  <main>
    <h1>Phiếu khảo sát ý kiến</h1>
    <p class="intro">Cảm ơn bạn đã dành thời gian tham gia khảo sát. Vui lòng trả lời các câu hỏi dưới đây.</p>

    <form id="surveyForm">
      <label class="field-label" for="name">Họ và tên (không bắt buộc)</label>
      <input id="name" name="name" type="text" placeholder="Nhập họ và tên">

      <label class="field-label" for="email">Email (không bắt buộc)</label>
      <input id="email" name="email" type="email" placeholder="name@example.com">

      <fieldset>
        <legend>1. Bạn đánh giá trải nghiệm tổng thể như thế nào? *</legend>
        <label class="option"><input type="radio" name="rating" value="Rất hài lòng" required> Rất hài lòng</label>
        <label class="option"><input type="radio" name="rating" value="Hài lòng"> Hài lòng</label>
        <label class="option"><input type="radio" name="rating" value="Bình thường"> Bình thường</label>
        <label class="option"><input type="radio" name="rating" value="Chưa hài lòng"> Chưa hài lòng</label>
      </fieldset>

      <fieldset>
        <legend>2. Điều gì bạn quan tâm nhất? (Có thể chọn nhiều đáp án)</legend>
        <label class="option"><input type="checkbox" name="interest" value="Chất lượng"> Chất lượng</label>
        <label class="option"><input type="checkbox" name="interest" value="Giá cả"> Giá cả</label>
        <label class="option"><input type="checkbox" name="interest" value="Tốc độ phục vụ"> Tốc độ phục vụ</label>
        <label class="option"><input type="checkbox" name="interest" value="Trải nghiệm sử dụng"> Trải nghiệm sử dụng</label>
      </fieldset>

      <fieldset>
        <legend>3. Bạn có muốn giới thiệu cho người khác không? *</legend>
        <label class="option"><input type="radio" name="recommend" value="Có" required> Có</label>
        <label class="option"><input type="radio" name="recommend" value="Không"> Không</label>
        <label class="option"><input type="radio" name="recommend" value="Chưa chắc"> Chưa chắc</label>
      </fieldset>

      <fieldset>
        <legend>4. Ý kiến hoặc đề xuất thêm</legend>
        <textarea name="comments" placeholder="Chia sẻ ý kiến của bạn..."></textarea>
      </fieldset>

      <button type="submit">Gửi khảo sát</button>
      <p id="notice" role="status" aria-live="polite"></p>
      <p class="hint">Bản mẫu này chưa gửi dữ liệu lên máy chủ. Hãy kết nối Google Forms hoặc dịch vụ backend để nhận câu trả lời.</p>
    </form>
  </main>
  <script>
    document.getElementById('surveyForm').addEventListener('submit', function (event) {
      event.preventDefault();
      const data = new FormData(this);
      const result = {
        name: data.get('name'),
        email: data.get('email'),
        rating: data.get('rating'),
        interests: data.getAll('interest'),
        recommend: data.get('recommend'),
        comments: data.get('comments')
      };
      const blob = new Blob([JSON.stringify(result, null, 2)], { type: 'application/json' });
      const url = URL.createObjectURL(blob);
      const link = document.createElement('a');
      link.href = url;
      link.download = 'phan-hoi-khao-sat.json';
      link.click();
      URL.revokeObjectURL(url);
      document.getElementById('notice').textContent =
        'Đã tải câu trả lời về thiết bị này dưới dạng JSON. Dữ liệu chưa được gửi cho người tạo khảo sát.';
      this.reset();
    });
  </script>
</body>
</html>
