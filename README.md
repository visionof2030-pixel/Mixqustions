<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>نظام إعداد التقارير التربوية</title>

<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap" rel="stylesheet">

<style>
/* ===== عام ===== */
body {
    font-family: 'Cairo', sans-serif;
    margin: 0;
    background: #f2f2f2;
    direction: rtl;
}

/* ===== واجهة ===== */
.wrapper {
    max-width: 900px;
    margin: auto;
    padding: 15px;
}

.form {
    background: white;
    padding: 20px;
    border-radius: 10px;
}

.form label {
    display: block;
    margin-top: 15px;
    font-weight: bold;
}

.form input,
.form textarea {
    width: 100%;
    padding: 12px;
    font-size: 16px;
}

textarea { min-height: 120px; }

button {
    margin-top: 20px;
    width: 100%;
    padding: 14px;
    font-size: 18px;
    background: #1a237e;
    color: white;
    border: none;
    border-radius: 8px;
}

/* ===== التقرير ===== */
.report {
    background: white;
    margin-top: 20px;
    padding: 20px;
    border-radius: 10px;
}

.report h1,
.report h2 { text-align: center; }

table {
    width: 100%;
    border-collapse: collapse;
    page-break-inside: avoid;
}

td {
    border: 1px solid #000;
    padding: 8px;
}

.label {
    font-weight: bold;
    background: #f5f5f5;
}

/* ===== الصور ===== */
.images {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
}

.images img {
    width: 100%;
    border: 1px solid #000;
    border-radius: 6px;
    page-break-inside: avoid;
}

@media (min-width: 768px) {
    .images img { width: 48%; }
}

/* ===== الطباعة ===== */
@page {
    size: A4;
    margin: 20mm;
}

@media print {
    body { background: white; }

    .wrapper { padding: 0; }

    .form { display: none; }

    .report {
        width: 210mm;
        min-height: 297mm;
        margin: 0;
        padding: 25mm;
        border-radius: 0;
    }

    img { max-width: 100%; }
}
</style>
</head>

<body>

<div class="wrapper">

<div class="form">
<label>اسم المدرسة</label>
<input oninput="school.textContent=this.value" value="مدرسة النموذجية الثانوية">

<label>اسم المدير</label>
<input oninput="principal.textContent=this.value" value="محمد أحمد السعيد">

<label>معد التقرير</label>
<input oninput="reporter.textContent=this.value" value="خالد سعيد العتيبي">

<label>عنوان التقرير</label>
<input oninput="titleH.textContent=this.value" value="تقرير فعالية اليوم الوطني">

<label>وصف التقرير</label>
<textarea oninput="description.textContent=this.value">
تم تنفيذ فعالية بمناسبة اليوم الوطني تضمنت أنشطة ثقافية وتربوية متنوعة.
</textarea>

<label>التاريخ</label>
<input oninput="date.textContent=this.value" value="1445/06/12 هـ">

<label>المكان</label>
<input oninput="location.textContent=this.value" value="ساحة المدرسة">

<label>إدراج الصور</label>
<input type="file" multiple accept="image/*" onchange="loadImages(this.files)">

<button onclick="window.print()">تصدير PDF</button>
</div>

<div class="report">
<h1>وزارة التعليم</h1>
<h2>إدارة تعليم منطقة مكة المكرمة</h2>
<h2 id="titleH">تقرير فعالية اليوم الوطني</h2>

<table>
<tr><td class="label">اسم المدرسة</td><td id="school">مدرسة النموذجية الثانوية</td></tr>
<tr><td class="label">اسم المدير</td><td id="principal">محمد أحمد السعيد</td></tr>
<tr><td class="label">معد التقرير</td><td id="reporter">خالد سعيد العتيبي</td></tr>
<tr><td class="label">التاريخ</td><td id="date">1445/06/12 هـ</td></tr>
<tr><td class="label">المكان</td><td id="location">ساحة المدرسة</td></tr>
</table>

<h3>وصف التقرير</h3>
<p id="description">
تم تنفيذ فعالية بمناسبة اليوم الوطني تضمنت أنشطة ثقافية وتربوية متنوعة.
</p>

<h3>الصور التوثيقية</h3>
<div class="images" id="imagesContainer"></div>
</div>

</div>

<script>
function loadImages(files) {
    const container = document.getElementById("imagesContainer");
    container.innerHTML = "";

    Array.from(files).forEach(file => {
        if (!file.type.startsWith("image/")) return;
        const reader = new FileReader();
        reader.onload = e => {
            const img = document.createElement("img");
            img.src = e.target.result;
            container.appendChild(img);
        };
        reader.readAsDataURL(file);
    });
}
</script>

</body>
</html>