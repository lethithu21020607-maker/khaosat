KHAO SAT

<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Khảo sát trực tuyến</title>

<style>
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg, #dbeafe, #eff6ff);
    min-height: 100vh;
    padding: 30px 15px;
    color: #1e293b;
}

.container {
    max-width: 700px;
    margin: auto;
    background: white;
    padding: 35px;
    border-radius: 18px;
    box-shadow: 0 8px 30px rgba(0,0,0,0.08);
}

.header {
    text-align: center;
    margin-bottom: 30px;
}

.header h1 {
    color: #2563eb;
    margin-bottom: 12px;
}

.header p {
    color: #64748b;
}

.section {
    margin-bottom: 25px;
    padding-bottom: 20px;
    border-bottom: 1px solid #e2e8f0;
}

.section h3 {
    margin-bottom: 15px;
    font-size: 17px;
}

input[type="text"],
input[type="email"],
textarea,
select {
    width: 100%;
    padding: 12px;
    border: 1px solid #cbd5e1;
    border-radius: 8px;
    font-size: 15px;
    margin-top: 8px;
}

textarea {
    min-height: 100px;
    resize: vertical;
}

.option {
    display: block;
    margin: 12px 0;
    cursor: pointer;
}

.option input {
    margin-right: 8px;
}

button {
    width: 100%;
    padding: 15px;
    background: #2563eb;
    color: white;
    border: none;
    border-radius: 9px;
    font-size: 16px;
    font-weight: bold;
    cursor: pointer;
}

button:hover {
    background: #1d4ed8;
}

#message {
    text-align: center;
    margin-top: 18px;
    color: #15803d;
    font-weight: bold;
}

@media(max-width: 500px) {
    .container {
        padding: 22px;
    }
}
</style>
</head>

<body>

<div class="container">

<div class="header">
    <h1>PHIẾU KHẢO SÁT</h1>
    <p>Khảo sát ý kiến và mức độ hài lòng</p>
    <p>Rất mong nhận được ý kiến đóng góp của bạn!</p>
</div>

<form id="surveyForm">

<div class="section">
    <h3>Thông tin người tham gia</h3>

    <input type="text" name="name"
    placeholder="Họ và tên">

    <input type="email" name="email"
    placeholder="Địa chỉ email">
</div>

<div class="section">
    <h3>1. Bạn đánh giá trải nghiệm tổng thể như thế nào? *</h3>

    <label class="option">
        <input type="radio" name="rating"
        value="Rất hài lòng" required>
        Rất hài lòng
    </label>

    <label class="option">
        <input type="radio" name="rating"
        value="Hài lòng">
        Hài lòng
    </label>

    <label class="option">
        <input type="radio" name="rating"
        value="Bình thường">
        Bình thường
    </label>

    <label class="option">
        <input type="radio" name="rating"
        value="Chưa hài lòng">
        Chưa hài lòng
    </label>
</div>

<div class="section">
    <h3>2. Bạn quan tâm đến yếu tố nào nhất?</h3>

    <label class="option">
        <input type="checkbox" name="interest"
        value="Chất lượng">
        Chất lượng
    </label>

    <label class="option">
        <input type="checkbox" name="interest"
        value="Giá cả">
        Giá cả
    </label>

    <label class="option">
        <input type="checkbox" name="interest"
        value="Dịch vụ">
        Dịch vụ
    </label>

    <label class="option">
        <input type="checkbox" name="interest"
        value="Trải nghiệm">
        Trải nghiệm
    </label>
</div>

<div class="section">
    <h3>3. Bạn có muốn giới thiệu cho người khác không? *</h3>

    <label class="option">
        <input type="radio" name="recommend"
        value="Có" required>
        Có
    </label>

    <label class="option">
        <input type="radio" name="recommend"
        value="Không">
        Không
    </label>

    <label class="option">
        <input type="radio" name="recommend"
        value="Chưa chắc">
        Chưa chắc
    </label>
</div>

<div class="section">
    <h3>4. Bạn có đề xuất hoặc góp ý gì không?</h3>

    <textarea name="comments"
    placeholder="Nhập ý kiến của bạn..."></textarea>
</div>

<button type="submit">GỬI KHẢO SÁT</button>

<p id="message"></p>

</form>
</div>

<script>
document.getElementById("surveyForm")
.addEventListener("submit", function(event) {

    event.preventDefault();

    const form = new FormData(this);

    const answers = {
        name: form.get("name"),
        email: form.get("email"),
        rating: form.get("rating"),
        interests: form.getAll("interest"),
        recommend: form.get("recommend"),
        comments: form.get("comments"),
        submittedAt: new Date().toISOString()
    };

    const blob = new Blob(
        [JSON.stringify(answers, null, 2)],
        {type: "application/json"}
    );

    const url = URL.createObjectURL(blob);

    const link = document.createElement("a");
    link.href = url;
    link.download = "cau-tra-loi-khao-sat.json";
    link.click();

    URL.revokeObjectURL(url);

    document.getElementById("message")
    .textContent = "Cảm ơn bạn đã tham gia khảo sát!";

    this.reset();
});
</script>

</body>
</html>
