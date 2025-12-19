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
    margin-top: 20px;
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

    <label>معد التقرير</label>
    <input id="reporter" value="خالد سعيد العتيبي">

    <label>عنوان التقرير</label>
    <input id="title" value="تقرير فعالية اليوم الوطني">

    <label>وصف التقرير</label>
    <textarea id="description">تم تنفيذ فعالية بمناسبة اليوم الوطني تضمنت أنشطة ثقافية وتربوية متنوعة هدفت إلى تعزيز الانتماء الوطني.</textarea>

    <label>التاريخ</label>
    <input id="date" value="1445/06/12 هـ">

    <label>المكان</label>
    <input id="location" value="ساحة المدرسة">

    <label>الصور (حتى 4)</label>
    <input type="file" id="images" multiple accept="image/*">
    <div class="preview" id="preview"></div>

    <button id="export">تصدير التقرير PDF</button>
    <div class="status" id="status"></div>
</div>

<script>
let uploadedImages = [];

document.getElementById('images').addEventListener('change', e => {
    uploadedImages = [];
    const preview = document.getElementById('preview');
    preview.innerHTML = '';

    [...e.target.files].slice(0,4).forEach(file => {
        const reader = new FileReader();
        reader.onload = ev => {
            uploadedImages.push(ev.target.result);
            const img = document.createElement('img');
            img.src = ev.target.result;
            preview.appendChild(img);
        };
        reader.readAsDataURL(file);
    });
});

document.getElementById('export').addEventListener('click', () => {
    const { jsPDF } = window.jspdf;
    const doc = new jsPDF();

    const school = school.value;
    const principal = principal.value;
    const reporter = reporter.value;
    const title = document.getElementById('title').value;
    const description = description.value;
    const date = date.value;
    const location = location.value;

    doc.setFontSize(14);
    doc.text("وزارة التعليم", 105, 15, { align: "center" });
    doc.text("إدارة تعليم منطقة مكة المكرمة", 105, 25, { align: "center" });
    doc.setFontSize(18);
    doc.text(title, 105, 40, { align: "center" });

    doc.autoTable({
        startY: 50,
        styles: { halign: 'right' },
        head: [['القيمة', 'البيان']],
        body: [
            [school, 'اسم المدرسة'],
            [principal, 'اسم المدير'],
            [reporter, 'معد التقرير'],
            [date, 'التاريخ'],
            [location, 'المكان']
        ]
    });

    let y = doc.lastAutoTable.finalY + 10;
    doc.text("وصف التقرير:", 190, y, { align: "right" });
    y += 7;
    doc.setFontSize(12);
    doc.text(doc.splitTextToSize(description, 170), 190, y, { align: "right" });

    if (uploadedImages.length) {
        doc.addPage();
        y = 20;
        uploadedImages.forEach((img, i) => {
            doc.addImage(img, 'JPEG', 20 + (i % 2) * 90, y, 80, 60);
            if (i % 2 === 1) y += 70;
        });
    }

    doc.save(title + ".pdf");
    document.getElementById('status').textContent = "تم إنشاء الملف بنجاح";
});
</script>

</body>
</html>