<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>أداة إعداد التقارير</title>

<style>
@font-face {
  font-family: 'KufamLocal';
  src: url('static/Kufam-Regular.ttf') format('truetype');
}
@font-face {
  font-family: 'KufamLocal';
  src: url('static/Kufam-Bold.ttf') format('truetype');
  font-weight: 700;
}

body {
  font-family: 'KufamLocal', sans-serif;
  background: #f2f2f2;
  margin: 0;
}

/* ================= الأداة ================= */
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

.report { display: none; }

/* ================= الطباعة ================= */
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

  .school-name {
    background: #0a3b40;
    color: white;
    width: fit-content;
    margin: 10px auto 18px;
    padding: 8px 28px;
    border-radius: 14px;
  }

  /* ===== شبكة المحتوى ===== */
  .grid-desc {
    display: grid;
    grid-template-columns: 1fr 90px 1fr;
    gap: 12px;
    margin-top: 18px;
    align-items: stretch;
  }

  /* ===== مربعات النص (موحدة – 12 سطر) ===== */
  .desc-box {
    border: 2px solid #cfd8dc;
    border-radius: 16px;
    padding: 14px;
    height: 260px;
    overflow: hidden;
  }

  .desc-box strong {
    display: block;
    margin-bottom: 8px;
  }

  .desc-box p {
    line-height: 1.6;
    max-height: calc(1.6em * 12);
    overflow: hidden;
    margin: 0;
  }

  /* ===== المربع الأوسط المصحح ===== */
  .vertical-split {
    background: #e0e0e0;
    border-radius: 16px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    padding: 14px 6px;
    font-weight: 700;
    text-align: center;
  }

  .vertical-split span {
    writing-mode: vertical-rl;
    font-size: 14px;
  }

  .vertical-divider {
    width: 60%;
    height: 2px;
    background: #9e9e9e;
    margin: 10px 0;
  }

  /* ===== التوقيعات ===== */
  .signatures {
    margin-top: 40px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 40px;
    text-align: center;
  }

  .signature-box {
    border-top: 2px solid #000;
    padding-top: 8px;
  }
}
</style>
</head>

<body>

<!-- ================= الأداة ================= -->
<div class="tool">

<label>اسم المدرسة</label>
<input oninput="school.textContent=this.value">

<label>الوصف المختصر</label>
<textarea oninput="desc1.textContent=this.value"></textarea>

<label>تفاصيل التنفيذ</label>
<textarea oninput="desc2.textContent=this.value"></textarea>

<label>النتائج</label>
<textarea oninput="desc3.textContent=this.value"></textarea>

<label>التوصيات</label>
<textarea oninput="desc4.textContent=this.value"></textarea>

<label>اسم المعلم</label>
<input oninput="teacher.textContent=this.value">

<label>اسم مدير المدرسة</label>
<input oninput="principal.textContent=this.value">

<button onclick="window.print()">تصدير PDF</button>
</div>

<!-- ================= التقرير ================= -->
<div class="report">

<!-- الصفحة الأولى -->
<div class="page">
  <div class="header-full">
    <img src="https://i.ibb.co/2037zjqy/IMG-2102.jpg">
    <div>وزارة التعليم</div>
  </div>

  <div class="school-name" id="school"></div>

  <div class="grid-desc">
    <div class="desc-box">
      <strong>وصف مختصر لما تم تنفيذه</strong>
      <p id="desc1"></p>
    </div>

    <div class="vertical-split">
      <span>وصف مختصر</span>
      <div class="vertical-divider"></div>
      <span>إجراءات التنفيذ</span>
    </div>

    <div class="desc-box">
      <strong>تفاصيل التنفيذ</strong>
      <p id="desc2"></p>
    </div>
  </div>
</div>

<!-- الصفحة الثانية -->
<div class="page">
  <div class="grid-desc">
    <div class="desc-box">
      <strong>النتائج</strong>
      <p id="desc3"></p>
    </div>

    <div class="vertical-split">
      <span>النتائج</span>
      <div class="vertical-divider"></div>
      <span>التوصيات</span>
    </div>

    <div class="desc-box">
      <strong>التوصيات</strong>
      <p id="desc4"></p>
    </div>
  </div>
</div>

<!-- الصفحة الثالثة -->
<div class="page">
  <div class="signatures">
    <div class="signature-box">
      اسم المعلم<br>
      <strong id="teacher"></strong>
    </div>
    <div class="signature-box">
      اسم مدير المدرسة<br>
      <strong id="principal"></strong>
    </div>
  </div>
</div>

</div>

</body>
</html>