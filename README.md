<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>أداة إعداد التقارير</title>

<style>
/* ===== الخط ===== */
@font-face {
  font-family: 'KufamLocal';
  src: url('static/Kufam-Regular.ttf') format('truetype');
}
@font-face {
  font-family: 'KufamLocal';
  src: url('static/Kufam-Bold.ttf') format('truetype');
  font-weight: 700;
}

/* ===== عام ===== */
body {
  font-family: 'KufamLocal', sans-serif;
  background: #f2f2f2;
  margin: 0;
}

/* ===== الأداة ===== */
.tool {
  max-width: 900px;
  margin: auto;
  padding: 20px;
  background: white;
}

.tool label {
  display: block;
  margin-top: 12px;
  font-weight: 700;
}

.tool input,
.tool textarea {
  width: 100%;
  padding: 10px;
  margin-top: 5px;
}

.tool textarea { min-height: 90px; }

button {
  margin-top: 20px;
  width: 100%;
  padding: 14px;
  font-size: 18px;
  background: #0a3b40;
  color: white;
  border: none;
  border-radius: 8px;
}

/* ===== معاينة الصور ===== */
.preview {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
  gap: 10px;
  margin-top: 10px;
}
.preview img {
  width: 100%;
  border-radius: 8px;
  border: 1px solid #ccc;
}

/* ===== قالب التقرير ===== */
.report { display: none; }

/* =================== الطباعة =================== */
@page {
  size: A4;
  margin: 14mm;
}

@media print {

  body { background: white; }
  .tool { display: none; }
  .report { display: block; }

  .page { page-break-after: always; }
  .page:last-child { page-break-after: auto; }

  /* ===== الهيدر ===== */
  .header-full {
    background: #0a3b40;
    color: white;
    border-radius: 18px;
    padding: 20px;
    text-align: center;
  }

  .header-full img {
    width: 110px;
    margin-bottom: 10px;
  }

  .header-full h1 {
    margin: 0;
    font-size: 18px;
    font-weight: 700;
  }

  .header-full h2 {
    margin: 6px 0 0;
    font-size: 14px;
    font-weight: 400;
  }

  .school-name {
    background: #0a3b40;
    color: white;
    width: fit-content;
    margin: 10px auto 18px;
    padding: 8px 28px;
    border-radius: 14px;
    font-size: 15px;
  }

  /* ===== شبكة المعلومات ===== */
  .info-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
    margin-bottom: 18px;
  }

  .info-box {
    border: 2px solid #cfd8dc;
    border-radius: 14px;
    padding: 10px;
    font-size: 14px;
  }

  .info-box span {
    display: block;
    background: #e0e0e0;
    border-radius: 10px;
    padding: 4px;
    text-align: center;
    font-weight: 700;
    margin-bottom: 6px;
  }

  /* ===== محتوى ===== */
  .grid-desc {
    display: grid;
    grid-template-columns: 1fr 90px 1fr;
    gap: 10px;
    margin-top: 18px;
  }

  .desc-box {
    border: 2px solid #cfd8dc;
    border-radius: 16px;
    padding: 12px;
  }

  /* ===== المربع النصفي المعدل ===== */
  .vertical {
    background: #eef3f1;
    border-radius: 16px;
    display: grid;
    grid-template-columns: 1fr 1px 1fr;
    align-items: center;
    padding: 10px 6px;
    font-weight: 600;
  }

  .vertical .right {
    writing-mode: vertical-rl;
    font-size: 12px;
    color: #1b5e52;
    text-align: center;
  }

  .vertical .left {
    writing-mode: vertical-lr;
    transform: rotate(180deg);
    font-size: 12px;
    color: #4f6f68;
    text-align: center;
  }

  .vertical .divider {
    width: 1px;
    height: 80%;
    background: #8fbfb3;
    margin: auto;
  }

  /* ===== الصور ===== */
  .images {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    margin-top: 18px;
  }

  .images img {
    width: 100%;
    border-radius: 12px;
    border: 1px solid #999;
  }
}
</style>
</head>

<body>

<!-- ========= الأداة ========= -->
<div class="tool">

<label>اسم المدرسة</label>
<input oninput="school.textContent=this.value">

<label>عنوان التقرير</label>
<input oninput="title.textContent=this.value">

<label>تاريخ التنفيذ</label>
<input oninput="date.textContent=this.value">

<label>المستهدفون</label>
<input oninput="target.textContent=this.value">

<label>عدد المستفيدين</label>
<input oninput="count.textContent=this.value">

<label>الوصف المختصر</label>
<textarea oninput="desc1.textContent=this.value"></textarea>

<label>إجراءات التنفيذ</label>
<textarea oninput="desc2.textContent=this.value"></textarea>

<label>النتائج</label>
<textarea oninput="desc3.textContent=this.value"></textarea>

<label>التوصيات</label>
<textarea oninput="desc4.textContent=this.value"></textarea>

<label>إرفاق الصور</label>
<input type="file" multiple accept="image/*" onchange="loadImages(this.files)">
<div class="preview" id="preview"></div>

<button onclick="window.print()">تصدير PDF</button>
</div>

<!-- ========= التقرير ========= -->
<div class="report">

<!-- الصفحة الأولى -->
<div class="page">

<div class="header-full">
  <img src="https://i.ibb.co/2037zjqy/IMG-2102.jpg">
  <h1>الإدارة العامة للتعليم</h1>
  <h2>وزارة التعليم</h2>
</div>

<div class="school-name" id="school"></div>

<div class="info-grid">
  <div class="info-box"><span>عنوان التقرير</span><div id="title"></div></div>
  <div class="info-box"><span>تاريخ التنفيذ</span><div id="date"></div></div>
  <div class="info-box"><span>المستهدفون</span><div id="target"></div></div>
  <div class="info-box"><span>عدد المستفيدين</span><div id="count"></div></div>
</div>

<div class="grid-desc">
  <div class="desc-box"><strong>وصف مختصر</strong><p id="desc1"></p></div>

  <div class="vertical">
    <div class="right">وصف مختصر</div>
    <div class="divider"></div>
    <div class="left">إجراءات التنفيذ</div>
  </div>

  <div class="desc-box"><p id="desc2"></p></div>
</div>

</div>

<!-- الصفحة الثانية -->
<div class="page">
  <div class="grid-desc">
    <div class="desc-box"><strong>النتائج</strong><p id="desc3"></p></div>

    <div class="vertical">
      <div class="right">النتائج</div>
      <div class="divider"></div>
      <div class="left">التوصيات</div>
    </div>

    <div class="desc-box"><p id="desc4"></p></div>
  </div>
</div>

<!-- الصفحة الثالثة -->
<div class="page">
  <h3 style="text-align:center">شواهد الصور</h3>
  <div class="images" id="imagesContainer"></div>
</div>

</div>

<script>
function loadImages(files) {
  const preview = document.getElementById("preview");
  const container = document.getElementById("imagesContainer");

  preview.innerHTML = "";
  container.innerHTML = "";

  Array.from(files).forEach(file => {
    if (!file.type.startsWith("image/")) return;
    const reader = new FileReader();
    reader.onload = e => {
      const img1 = document.createElement("img");
      const img2 = document.createElement("img");
      img1.src = img2.src = e.target.result;
      preview.appendChild(img1);
      container.appendChild(img2);
    };
    reader.readAsDataURL(file);
  });
}
</script>

</body>
</html>