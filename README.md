<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>نظام إعداد التقارير التربوية</title>

<!-- jsPDF -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf-autotable/3.5.29/jspdf.plugin.autotable.min.js"></script>

<style>
body {
    font-family: Arial, sans-serif;
    background: #f2f2f2;
    padding: 20px;
    direction: rtl;
}
.container {
    max-width: 800px;
    background: #fff;
    margin: auto;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 0 0 20px rgba(0,0,0,.1);
}
h1 {
    text-align: center;
    color: #1a237e;
    margin-bottom: 30px;
}
label {
    font-weight: bold;
    margin-top: 15px;
    display: block;
}
input, textarea {
    width: 100%;
    padding: 10px;
    margin-top: 5px;
    border-radius: 5px;
    border: 1px solid #ccc;
}
textarea {
    height: 120px;
}
button {
    margin-top: 25px;
    padding: 15px;
    width: 100%;
    border: none;
    border-radius: 8px;
    background: #1a237e;
    color: #fff;
    font-size: 16px;
    cursor: pointer;
}
button:hover {
    background: #283593;
}
.preview {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
    margin-top: 10px;
}
.preview img {
    width: 120px;
    height: 80px;
    object-fit: cover;
    border: 1px solid #ccc;
}
.status {
    margin-top: 15px;
    text-align: center;
    font-weight: bold;
    color: green;
}
</style>
</head>

<body>

<div class="container">
    <h1>نظام إعداد التقارير التربوية</h1>

    <label>اسم المدرسة</label>
    <input id="school" value="مدرسة النموذجية الثانوية">

    <label>اسم المدير</label>
    <input id="principal" value="محمد أحمد السعيد">

    <label>اسم معد التقرير</label>
    <input id="reporter" value="خالد سعيد العتيبي">

    <label>عنوان التقرير</label>
    <input id="title" value="تقرير فعالية اليوم الوطني">

    <label>وصف التقرير</label>
    <textarea id="description">تم تنفيذ فعالية بمناسبة اليوم الوطني تضمنت أنشطة ثقافية وتربوية متنوعة.</textarea>

    <label>التاريخ</label>
    <input id="date" value="1445/06/12 هـ">

    <label>المكان</label>
    <input id="location" value="ساحة المدرسة">

    <label>الصور (حد أقصى 4)</label>
    <input type="file" id="images" multiple accept="image/*">
    <div class="preview" id="preview"></div>

    <button id="exportBtn">تصدير التقرير PDF</button>
    <div class="status" id="status"></div>
</div>

<script>
let uploadedImages = [];

document.getElementById('images').addEventListener('change', function (e) {
    uploadedImages = [];
    const preview = document.getElementById('preview');
    preview.innerHTML = '';

    Array.from(e.target.files).slice(0,4).forEach(file => {
        const reader = new FileReader();
        reader.onload = function(ev) {
            uploadedImages.push(ev.target.result);
            const img = document.createElement('img');
            img.src = ev.target.result;
            preview.appendChild(img);
        };
        reader.readAsDataURL(file);
    });
});

document.getElementById('exportBtn').addEventListener('click', function () {

    const schoolVal = document.getElementById('school').value.trim();
    const principalVal = document.getElementById('principal').value.trim();
    const reporterVal = document.getElementById('reporter').value.trim();
    const titleVal = document.getElementById('title').value.trim();
    const descriptionVal = document.getElementById('description').value.trim();
    const dateVal = document.getElementById('date').value.trim();
    const locationVal = document.getElementById('location').value.trim();

    if (!schoolVal || !principalVal || !reporterVal || !titleVal || !descriptionVal) {
        alert("يرجى تعبئة جميع الحقول الأساسية");
        return;
    }

    const { jsPDF } = window.jspdf;
    const doc = new jsPDF("p", "mm", "a4");

    doc.setFontSize(14);
    doc.text("وزارة التعليم", 105, 15, { align: "center" });
    doc.text("إدارة تعليم منطقة مكة المكرمة", 105, 25, { align: "center" });

    doc.setFontSize(18);
    doc.text(titleVal, 105, 40, { align: "center" });

    doc.autoTable({
        startY: 50,
        styles: { halign: 'right', fontSize: 12 },
        head: [['القيمة', 'البيان']],
        body: [
            [schoolVal, 'اسم المدرسة'],
            [principalVal, 'اسم المدير'],
            [reporterVal, 'معد التقرير'],
            [dateVal, 'التاريخ'],
            [locationVal, 'المكان']
        ],
        theme: 'grid'
    });

    let y = doc.lastAutoTable.finalY + 10;
    doc.setFontSize(14);
    doc.text("وصف التقرير:", 190, y, { align: "right" });
    y += 8;

    doc.setFontSize(12);
    doc.text(
        doc.splitTextToSize(descriptionVal, 170),
        190,
        y,
        { align: "right" }
    );

    if (uploadedImages.length > 0) {
        doc.addPage();
        let imgY = 20;

        uploadedImages.forEach((img, i) => {
            doc.addImage(img, 'JPEG', 20 + (i % 2) * 90, imgY, 80, 60);
            if (i % 2 === 1) imgY += 70;
        });
    }

    doc.save(titleVal + ".pdf");
    document.getElementById('status').textContent = "تم إنشاء التقرير بنجاح";
});
</script>

</body>
</html>