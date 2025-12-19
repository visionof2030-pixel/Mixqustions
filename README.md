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
  font-weight: 400;
}
@font-face {
  font-family: 'KufamLocal';
  src: url('static/Kufam-Bold.ttf') format('truetype');
  font-weight: 700;
}

/* ===== عام ===== */
body {
  font-family: 'KufamLocal', sans-serif;
  background: linear-gradient(135deg, #f2f7f6 0%, #e8eff0 100%);
  margin: 0;
  padding: 20px;
  color: #333;
}

/* ===== الأداة ===== */
.tool {
  max-width: 900px;
  margin: 30px auto;
  padding: 30px;
  background: white;
  border-radius: 20px;
  box-shadow: 0 10px 30px rgba(10, 59, 64, 0.08);
  border: 1px solid #e0e6e5;
}

.tool-header {
  text-align: center;
  margin-bottom: 30px;
  padding-bottom: 20px;
  border-bottom: 2px solid #0a3b40;
}

.tool-header h1 {
  color: #0a3b40;
  margin: 0;
  font-size: 26px;
  font-weight: 700;
}

.tool-header p {
  color: #4f6f68;
  margin-top: 8px;
  font-size: 16px;
}

/* ===== حقول الإدخال ===== */
.input-group {
  margin-bottom: 25px;
  position: relative;
}

.tool label {
  display: block;
  margin-bottom: 8px;
  font-weight: 700;
  color: #1b5e52;
  font-size: 15px;
}

.tool input,
.tool textarea,
.tool select {
  width: 100%;
  padding: 14px;
  border: 2px solid #cfd8dc;
  border-radius: 12px;
  font-family: 'KufamLocal', sans-serif;
  font-size: 15px;
  transition: all 0.3s ease;
  box-sizing: border-box;
  background: #f9fbfb;
}

.tool input:focus,
.tool textarea:focus,
.tool select:focus {
  outline: none;
  border-color: #0a3b40;
  background: white;
  box-shadow: 0 0 0 3px rgba(10, 59, 64, 0.1);
}

.tool textarea {
  min-height: 100px;
  resize: vertical;
  line-height: 1.6;
}

.tool select {
  cursor: pointer;
  appearance: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='16' height='16' viewBox='0 0 24 24' fill='none' stroke='%230a3b40' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpolyline points='6 9 12 15 18 9'%3E%3C/polyline%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: left 15px center;
  padding-right: 15px;
}

/* ===== نص افتراضي ===== */
.default-text-note {
  font-size: 13px;
  color: #4f6f68;
  margin-top: 5px;
  font-style: italic;
  padding-right: 5px;
}

.clear-default-btn {
  position: absolute;
  left: 10px;
  top: 38px;
  background: #f0f4f3;
  border: 1px solid #cfd8dc;
  border-radius: 8px;
  padding: 6px 12px;
  font-size: 13px;
  cursor: pointer;
  color: #4f6f68;
  transition: all 0.3s ease;
}

.clear-default-btn:hover {
  background: #e8eff0;
  color: #0a3b40;
  border-color: #0a3b40;
}

/* ===== معاينة الصور ===== */
.preview-container {
  margin-top: 10px;
}

.preview-container h4 {
  margin: 15px 0 10px;
  color: #1b5e52;
  font-size: 14px;
}

.preview {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
  gap: 12px;
  margin-top: 10px;
}

.preview img {
  width: 100%;
  height: 120px;
  object-fit: cover;
  border-radius: 10px;
  border: 2px solid #e0e6e5;
  transition: transform 0.3s ease;
}

.preview img:hover {
  transform: scale(1.03);
  border-color: #0a3b40;
}

/* ===== الأزرار ===== */
.button-container {
  display: flex;
  gap: 15px;
  margin-top: 30px;
}

button {
  flex: 1;
  padding: 16px;
  font-size: 17px;
  font-weight: 700;
  border: none;
  border-radius: 12px;
  cursor: pointer;
  transition: all 0.3s ease;
  font-family: 'KufamLocal', sans-serif;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
}

#printBtn {
  background: linear-gradient(135deg, #0a3b40 0%, #1b5e52 100%);
  color: white;
}

#printBtn:hover {
  background: linear-gradient(135deg, #083136 0%, #164d44 100%);
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(10, 59, 64, 0.2);
}

#resetBtn {
  background: #f0f4f3;
  color: #4f6f68;
  border: 2px solid #cfd8dc;
}

#resetBtn:hover {
  background: #e8eff0;
  border-color: #8fbfb3;
}

.load-defaults-btn {
  background: #1b5e52;
  color: white;
  margin-top: 10px;
  padding: 10px 15px;
  font-size: 14px;
  width: auto;
  flex: none;
}

.load-defaults-btn:hover {
  background: #164d44;
}

/* ===== قالب التقرير ===== */
.report { display: none; }

/* =================== الطباعة =================== */
@page {
  size: A4;
  margin: 14mm;
}

@media print {
  body {
    background: white;
    padding: 0;
  }
  
  .tool { display: none; }
  .report { display: block; }

  .page {
    page-break-after: always;
    padding-bottom: 20mm;
  }
  
  .page:last-child { page-break-after: auto; }

  /* ===== الهيدر ===== */
  .header-full {
    background: linear-gradient(135deg, #0a3b40 0%, #1b5e52 100%);
    color: white;
    border-radius: 18px;
    padding: 22px;
    text-align: center;
    margin-bottom: 20px;
  }

  .header-full img {
    width: 110px;
    margin-bottom: 12px;
  }

  .header-full h1 {
    margin: 0;
    font-size: 20px;
    font-weight: 700;
    letter-spacing: 0.5px;
  }

  .header-full h2 {
    margin: 8px 0 0;
    font-size: 15px;
    font-weight: 400;
    opacity: 0.9;
  }

  .school-name {
    background: #0a3b40;
    color: white;
    width: fit-content;
    margin: 15px auto 20px;
    padding: 10px 35px;
    border-radius: 14px;
    font-size: 16px;
    font-weight: 700;
    text-align: center;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }

  /* ===== معلومات التقرير في جميع الصفحات ===== */
  .report-info-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 12px;
    margin-bottom: 20px;
    background: #f9fbfb;
    padding: 15px;
    border-radius: 14px;
    border: 2px solid #cfd8dc;
    font-size: 14px;
  }

  .report-info-item {
    text-align: center;
  }

  .report-info-label {
    display: block;
    background: #0a3b40;
    color: white;
    border-radius: 10px;
    padding: 6px;
    font-weight: 700;
    margin-bottom: 8px;
    font-size: 13px;
  }

  .report-info-value {
    padding: 4px;
    min-height: 20px;
  }

  /* ===== محتوى ===== */
  .grid-desc {
    display: grid;
    grid-template-columns: 1fr 90px 1fr;
    gap: 15px;
    margin-top: 20px;
  }

  .desc-box {
    border: 2px solid #cfd8dc;
    border-radius: 16px;
    padding: 18px;
    background: #f9fbfb;
    font-size: 14px;
    line-height: 1.6;
  }

  .desc-box strong {
    display: block;
    color: #0a3b40;
    margin-bottom: 10px;
    font-size: 16px;
    border-bottom: 1px dashed #cfd8dc;
    padding-bottom: 8px;
  }

  .desc-box p {
    margin: 8px 0;
    white-space: pre-line;
  }

  /* ===== المربع النصفي المعدل ===== */
  .vertical {
    background: #eef3f1;
    border-radius: 16px;
    display: grid;
    grid-template-columns: 1fr 1px 1fr;
    align-items: center;
    padding: 15px 8px;
    font-weight: 600;
    height: 100%;
  }

  .vertical .right {
    writing-mode: vertical-rl;
    font-size: 13px;
    color: #1b5e52;
    text-align: center;
    font-weight: 700;
  }

  .vertical .left {
    writing-mode: vertical-lr;
    transform: rotate(180deg);
    font-size: 13px;
    color: #4f6f68;
    text-align: center;
    font-weight: 700;
  }

  .vertical .divider {
    width: 1px;
    height: 85%;
    background: #8fbfb3;
    margin: auto;
  }

  /* ===== الصور ===== */
  .images-page {
    margin-top: 20px;
  }
  
  .images-page h3 {
    text-align: center;
    color: #0a3b40;
    font-size: 20px;
    margin-bottom: 20px;
    padding-bottom: 10px;
    border-bottom: 2px solid #cfd8dc;
  }

  .images {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 15px;
    margin-top: 15px;
  }

  .images img {
    width: 100%;
    height: 180px;
    object-fit: cover;
    border-radius: 12px;
    border: 2px solid #b0bec5;
  }
  
  /* ===== فوتر الصفحة ===== */
  .page-footer {
    position: absolute;
    bottom: 10mm;
    left: 14mm;
    right: 14mm;
    text-align: center;
    color: #666;
    font-size: 12px;
    border-top: 1px solid #ddd;
    padding-top: 10px;
  }
}
</style>
</head>

<body>

<!-- ========= الأداة ========= -->
<div class="tool">
  <div class="tool-header">
    <h1>🖋️ أداة إعداد التقارير المدرسية</h1>
    <p>اختر نوع التقرير لتحميل النصوص الافتراضية، ثم عدل كما تشاء</p>
  </div>

  <div class="input-group">
    <label>🏫 اسم المدرسة</label>
    <input type="text" id="schoolInput" placeholder="أدخل اسم المدرسة">
  </div>

  <div class="input-group">
    <label>📄 عنوان التقرير</label>
    <select id="reportType">
      <option value="">اختر نوع التقرير</option>
      <option value="تقرير تنفيذ استراتيجية">تقرير تنفيذ استراتيجية</option>
      <option value="تقرير تنفيذ أنشطة داخل الفصل">تقرير تنفيذ أنشطة داخل الفصل</option>
      <option value="تقرير نشاط إثرائي">تقرير نشاط إثرائي</option>
      <option value="تقرير خطة علاجية">تقرير خطة علاجية</option>
      <option value="تقرير تكريم المتميزين">تقرير تكريم المتميزين</option>
    </select>
    <div class="default-text-note">سيتم تحميل نصوص افتراضية عند الاختيار</div>
  </div>

  <button class="load-defaults-btn" onclick="loadDefaultTexts()">📥 تحميل النصوص الافتراضية للتقريـر المختار</button>

  <div class="input-group">
    <label>📅 تاريخ التنفيذ</label>
    <input type="text" id="dateInput" placeholder="يوم / شهر / سنة">
  </div>

  <div class="input-group">
    <label>👥 المستهدفون</label>
    <input type="text" id="targetInput" placeholder="الفئة المستهدفة">
  </div>

  <div class="input-group">
    <label>🔢 عدد المستفيدين</label>
    <input type="text" id="countInput" placeholder="عدد المشاركين">
  </div>

  <div class="input-group">
    <label>📝 الوصف المختصر</label>
    <button class="clear-default-btn" onclick="clearField('desc1Input')">مسح</button>
    <textarea id="desc1Input" placeholder="وصف مختصر للنشاط أو البرنامج" rows="6"></textarea>
    <div class="default-text-note">يمكنك حذف هذا النص والكتابة بما يناسبك (6 أسطر كحد أقصى)</div>
  </div>

  <div class="input-group">
    <label>⚙️ إجراءات التنفيذ</label>
    <button class="clear-default-btn" onclick="clearField('desc2Input')">مسح</button>
    <textarea id="desc2Input" placeholder="الخطوات والإجراءات التنفيذية" rows="6"></textarea>
    <div class="default-text-note">يمكنك حذف هذا النص والكتابة بما يناسبك (6 أسطر كحد أقصى)</div>
  </div>

  <div class="input-group">
    <label>📊 النتائج</label>
    <button class="clear-default-btn" onclick="clearField('desc3Input')">مسح</button>
    <textarea id="desc3Input" placeholder="النتائج المتحققة من التنفيذ"></textarea>
    <div class="default-text-note">يمكنك حذف هذا النص والكتابة بما يناسبك</div>
  </div>

  <div class="input-group">
    <label>💡 التوصيات</label>
    <button class="clear-default-btn" onclick="clearField('desc4Input')">مسح</button>
    <textarea id="desc4Input" placeholder="التوصيات والمقترحات"></textarea>
    <div class="default-text-note">يمكنك حذف هذا النص والكتابة بما يناسبك</div>
  </div>

  <div class="input-group">
    <label>🖼️ إرفاق الصور (اختياري)</label>
    <input type="file" id="imageInput" multiple accept="image/*">
    <div class="preview-container">
      <h4>معاينة الصور المرفوعة:</h4>
      <div class="preview" id="preview"></div>
    </div>
  </div>

  <div class="button-container">
    <button id="resetBtn" onclick="resetForm()">🔄 مسح النموذج</button>
    <button id="printBtn" onclick="generateReport()">📥 تصدير PDF</button>
  </div>
</div>

<!-- ========= التقرير ========= -->
<div class="report">

<!-- الصفحة الأولى -->
<div class="page">
  <div class="header-full">
    <img src="https://i.ibb.co/2037zjqy/IMG-2102.jpg" alt="شعار الوزارة">
    <h1>الإدارة العامة للتعليم</h1>
    <h2>وزارة التعليم</h2>
  </div>

  <div class="school-name" id="school"></div>

  <!-- معلومات التقرير - الصفحة الأولى -->
  <div class="report-info-grid" id="reportInfo1">
    <div class="report-info-item">
      <span class="report-info-label">عنوان التقرير</span>
      <div class="report-info-value" id="title1"></div>
    </div>
    <div class="report-info-item">
      <span class="report-info-label">تاريخ التنفيذ</span>
      <div class="report-info-value" id="date1"></div>
    </div>
    <div class="report-info-item">
      <span class="report-info-label">المستهدفون</span>
      <div class="report-info-value" id="target1"></div>
    </div>
    <div class="report-info-item">
      <span class="report-info-label">عدد المستفيدين</span>
      <div class="report-info-value" id="count1"></div>
    </div>
  </div>

  <div class="grid-desc">
    <div class="desc-box">
      <strong>وصف مختصر</strong>
      <p id="desc1"></p>
    </div>

    <div class="vertical">
      <div class="right">وصف مختصر</div>
      <div class="divider"></div>
      <div class="left">إجراءات التنفيذ</div>
    </div>

    <div class="desc-box">
      <strong>إجراءات التنفيذ</strong>
      <p id="desc2"></p>
    </div>
  </div>
  
  <div class="page-footer">صفحة 1 من 3</div>
</div>

<!-- الصفحة الثانية -->
<div class="page">
  <div class="header-full">
    <img src="https://i.ibb.co/2037zjqy/IMG-2102.jpg" alt="شعار الوزارة">
    <h1>الإدارة العامة للتعليم</h1>
    <h2>وزارة التعليم</h2>
  </div>

  <div class="school-name" id="school2"></div>

  <!-- معلومات التقرير - الصفحة الثانية -->
  <div class="report-info-grid" id="reportInfo2">
    <div class="report-info-item">
      <span class="report-info-label">عنوان التقرير</span>
      <div class="report-info-value" id="title2"></div>
    </div>
    <div class="report-info-item">
      <span class="report-info-label">تاريخ التنفيذ</span>
      <div class="report-info-value" id="date2"></div>
    </div>
    <div class="report-info-item">
      <span class="report-info-label">المستهدفون</span>
      <div class="report-info-value" id="target2"></div>
    </div>
    <div class="report-info-item">
      <span class="report-info-label">عدد المستفيدين</span>
      <div class="report-info-value" id="count2"></div>
    </div>
  </div>

  <div class="grid-desc">
    <div class="desc-box">
      <strong>النتائج</strong>
      <p id="desc3"></p>
    </div>

    <div class="vertical">
      <div class="right">النتائج</div>
      <div class="divider"></div>
      <div class="left">التوصيات</div>
    </div>

    <div class="desc-box">
      <strong>التوصيات</strong>
      <p id="desc4"></p>
    </div>
  </div>
  
  <div class="page-footer">صفحة 2 من 3</div>
</div>

<!-- الصفحة الثالثة -->
<div class="page images-page">
  <div class="header-full">
    <img src="https://i.ibb.co/2037zjqy/IMG-2102.jpg" alt="شعار الوزارة">
    <h1>الإدارة العامة للتعليم</h1>
    <h2>وزارة التعليم</h2>
  </div>

  <div class="school-name" id="school3"></div>

  <!-- معلومات التقرير - الصفحة الثالثة -->
  <div class="report-info-grid" id="reportInfo3">
    <div class="report-info-item">
      <span class="report-info-label">عنوان التقرير</span>
      <div class="report-info-value" id="title3"></div>
    </div>
    <div class="report-info-item">
      <span class="report-info-label">تاريخ التنفيذ</span>
      <div class="report-info-value" id="date3"></div>
    </div>
    <div class="report-info-item">
      <span class="report-info-label">المستهدفون</span>
      <div class="report-info-value" id="target3"></div>
    </div>
    <div class="report-info-item">
      <span class="report-info-label">عدد المستفيدين</span>
      <div class="report-info-value" id="count3"></div>
    </div>
  </div>

  <h3>📸 شواهد الصور</h3>
  <div class="images" id="imagesContainer"></div>
  <div class="page-footer">صفحة 3 من 3</div>
</div>

</div>

<script>
// عناصر DOM
const schoolInput = document.getElementById('schoolInput');
const reportType = document.getElementById('reportType');
const dateInput = document.getElementById('dateInput');
const targetInput = document.getElementById('targetInput');
const countInput = document.getElementById('countInput');
const desc1Input = document.getElementById('desc1Input');
const desc2Input = document.getElementById('desc2Input');
const desc3Input = document.getElementById('desc3Input');
const desc4Input = document.getElementById('desc4Input');
const imageInput = document.getElementById('imageInput');

// عناصر التقرير
const schoolElement = document.getElementById('school');
const schoolElement2 = document.getElementById('school2');
const schoolElement3 = document.getElementById('school3');
const titleElement = document.getElementById('title1');
const titleElement2 = document.getElementById('title2');
const titleElement3 = document.getElementById('title3');
const dateElement = document.getElementById('date1');
const dateElement2 = document.getElementById('date2');
const dateElement3 = document.getElementById('date3');
const targetElement = document.getElementById('target1');
const targetElement2 = document.getElementById('target2');
const targetElement3 = document.getElementById('target3');
const countElement = document.getElementById('count1');
const countElement2 = document.getElementById('count2');
const countElement3 = document.getElementById('count3');
const desc1Element = document.getElementById('desc1');
const desc2Element = document.getElementById('desc2');
const desc3Element = document.getElementById('desc3');
const desc4Element = document.getElementById('desc4');

// النصوص الافتراضية لكل نوع تقرير (مختصرة إلى 6 أسطر)
const defaultTexts = {
  "تقرير تنفيذ استراتيجية": {
    desc1: "تنفيذ استراتيجية تدريسية متطورة لتحسين نواتج التعلم.\n\nاستهدفت رفع مستوى المهارات الأساسية.\n\nاعتمدت على أساليب التعلم النشط.\n\nركزت على التفاعل والمشاركة الصفية.\n\nتم تطبيقها وفق خطة زمنية محددة.\n\nشارك فيها جميع معلمي المادة.",
    desc2: "عقد ورشة عمل للمعلمين للتعريف بالاستراتيجية.\n\nتصميم أدوات تقييم قبلي وبعدي.\n\nتطبيق الاستراتيجية داخل الفصول.\n\nمتابعة أسبوعية من فريق التطوير.\n\nتوثيق الممارسات الناجحة.\n\nتقييم أثر التنفيذ على الطلاب.",
    desc3: "1. تحسن ملحوظ في دافعية الطلاب نحو التعلم\n2. ارتفاع في نسب التفاعل الصفي بنسبة 40%\n3. تحسن في نتائج الاختبارات التكوينية\n4. رضا المعلمين عن الأساليب الجديدة بنسبة 85%\n5. توثيق 15 ممارسة ناجحة قابلة للتعميم",
    desc4: "1. تعميم الاستراتيجية على جميع الصفوف المماثلة\n2. تدريب معلمين جدد على الاستراتيجية\n3. توفير موارد إضافية لدعم التنفيذ\n4. استمرار المتابعة والتقييم الدوري\n5. عقد لقاءات تبادل خبرات بين المعلمين"
  },
  "تقرير تنفيذ أنشطة داخل الفصل": {
    desc1: "سلسلة أنشطة صفية تفاعلية لتعزيز المهارات.\n\nركزت على التفكير الناقد والتعلم التعاوني.\n\nدمجت التقنية والألعاب التعليمية.\n\nصممت لتناسب مختلف أنماط التعلم.\n\nنفذت في بيئة صفية محفزة.\n\nاستهدفت جميع طلاب الصف.",
    desc2: "تقسيم الطلاب إلى مجموعات تعاونية.\n\nتوزيع المهام والأدوار على المجموعات.\n\nاستخدام وسائل تعليمية تفاعلية.\n\nتخصيص وقت للمناقشة والعرض.\n\nتقديم تغذية راجعة فورية.\n\nتقويم أداء المجموعات.",
    desc3: "1. تفاعل إيجابي من جميع الطلاب مع الأنشطة\n2. تنمية مهارات العمل الجماعي والتعاون\n3. تحسن في قدرة الطلاب على التعبير عن الأفكار\n4. زيادة ثقة الطلاب بأنفسهم\n5. تحقيق الأهداف التعليمية المخطط لها بنسبة 90%",
    desc4: "1. الاستمرار في تطبيق الأنشطة التفاعلية بشكل دوري\n2. تنويع أساليب التقويم المستخدمة\n3. تخصيص وقت كافٍ لكل نشاط\n4. تدريب الطلاب على مهارات الحوار والمناقشة\n5. توثيق الأنشطة الناجحة في بنك الأنشطة المدرسية"
  },
  "تقرير نشاط إثرائي": {
    desc1: "نشاط إثرائي خارج الإطار الدراسي.\n\nهدف إلى تنمية مواهب الطلاب وصقل مهاراتهم.\n\nغطى مجالات فنية وأدبية وعلمية.\n\nشارك فيه طلاب بمختلف اهتماماتهم.\n\nنظم في بيئة جاذبة ومحفزة.\n\nاستمر لمدة فصل دراسي كامل.",
    desc2: "تحديد المجالات الإثرائية المطلوبة.\n\nدعوة الطلاب للمشاركة حسب اهتماماتهم.\n\nتوفير المواد والأدوات اللازمة.\n\nتنظيم ورش العمل والجلسات التدريبية.\n\nمتابعة تقدم المشاركين أسبوعياً.\n\nعرض منتجات الطلاب وإنجازاتهم.",
    desc3: "1. اكتشاف مواهب جديدة لدى 25 طالباً\n2. تنمية الثقة بالنفس لدى المشاركين\n3. إنتاج أعمال فنية وأدبية متميزة\n4. زيادة الانتماء للمدرسة والمجتمع\n5. رضا أولياء الأمور عن الأنشطة الإثرائية",
    desc4: "1. استمرار النشاط الإثرائي كبرنامج دائم\n2. تخصيص مساحة مناسبة للأنشطة الإثرائية\n3. تدريب معلمين متخصصين في المجالات المختلفة\n4. مشاركة الأعمال في معارض ومناسبات\n5. توفير جوائز تشجيعية للمتميزين"
  },
  "تقرير خطة علاجية": {
    desc1: "خطة علاجية شاملة للطلاب المتعثرين.\n\nهدفت لرفع المستوى التحصيلي.\n\nتجاوزت الصعوبات التعليمية.\n\nركزت على المواد الأساسية.\n\nصممت برامج فردية وجماعية.\n\nتابعت التقدم أسبوعياً.",
    desc2: "تشخيص الصعوبات التعليمية لكل طالب.\n\nوضع أهداف علاجية قابلة للقياس.\n\nتصميم برامج علاجية فردية وجماعية.\n\nتنفيذ جلسات علاجية مكثفة.\n\nمتابعة التقدم وتعديل الخطة.\n\nتواصل مع أولياء الأمور.",
    desc3: "1. تحسن ملحوظ في مستوى 18 طالباً من أصل 25\n2. ارتفاع درجات الطلاب في الاختبارات\n3. تحسن في دافعية التعلم لدى الطلاب المتعثرين\n4. انخفاض نسبة الغياب بين الطلاب المستهدفين\n5. رضا أولياء الأمور عن الخطة العلاجية",
    desc4: "1. الاستمرار في المتابعة للطلاب الذين يحتاجون مزيداً من الوقت\n2. تدريب المعلمين على استراتيجيات العلاج الفعالة\n3. توفير مواد تعليمية علاجية إضافية\n4. عقد لقاءات دورية مع أولياء الأمور\n5. توثيق الحالات الناجحة للاستفادة منها مستقبلاً"
  },
  "تقرير تكريم المتميزين": {
    desc1: "حفل تكريم للطلاب المتميزين بمختلف المجالات.\n\nهدف لتحفيز الطلاب وتعزيز التنافس الإيجابي.\n\nشمل المجالات الدراسية والسلوكية.\n\nتضمن الرياضية والفنية والإبداعية.\n\nنظم بحضور أولياء الأمور.\n\nشمل فقرات فنية وتكريمية.",
    desc2: "تحديد معايير التميز والتفوق.\n\nترشيح الطلاب المتميزين من قبل المعلمين.\n\nتشكيل لجنة لاختيار المكرمين.\n\nإعداد شهادات التقدير والهدايا.\n\nتنظيم حفل التكريم.\n\nتغطية إعلامية للفعالية.",
    desc3: "1. تكريم 35 طالباً وطالبة في مختلف المجالات\n2. ارتفاع الروح المعنوية لدى الطلاب المكرمين\n3. تحفيز باقي الطلاب للسعي نحو التميز\n4. تعزيز الشراكة مع أولياء الأمور\n5. تغطية إعلامية إيجابية للفعالية",
    desc4: "1. جعل التكريم حدثاً سنوياً للمدرسة\n2. تنويع مجالات التكريم لتشمل جميع المواهب\n3. ربط التكريم بجوائز معنوية ومادية\n4. توثيق إنجازات المتميزين في سجلات المدرسة\n5. إشراك الطلاب في تنظيم فعاليات التكريم"
  }
};

// تحديث جميع نسخ التقرير في الوقت الحقيقي
function updateAllReports() {
  // اسم المدرسة في جميع الصفحات
  schoolElement.textContent = schoolInput.value;
  schoolElement2.textContent = schoolInput.value;
  schoolElement3.textContent = schoolInput.value;
  
  // عنوان التقرير في جميع الصفحات
  titleElement.textContent = reportType.value;
  titleElement2.textContent = reportType.value;
  titleElement3.textContent = reportType.value;
  
  // تاريخ التنفيذ في جميع الصفحات
  dateElement.textContent = dateInput.value;
  dateElement2.textContent = dateInput.value;
  dateElement3.textContent = dateInput.value;
  
  // المستهدفون في جميع الصفحات
  targetElement.textContent = targetInput.value;
  targetElement2.textContent = targetInput.value;
  targetElement3.textContent = targetInput.value;
  
  // عدد المستفيدين في جميع الصفحات
  countElement.textContent = countInput.value;
  countElement2.textContent = countInput.value;
  countElement3.textContent = countInput.value;
  
  // المحتوى
  desc1Element.textContent = desc1Input.value;
  desc2Element.textContent = desc2Input.value;
  desc3Element.textContent = desc3Input.value;
  desc4Element.textContent = desc4Input.value;
}

// إضافة المستمعين للأحداث
schoolInput.addEventListener('input', updateAllReports);
reportType.addEventListener('change', () => {
  updateAllReports();
  // تحديث العنوان في الواجهة أيضًا
  const title = reportType.value;
  titleElement.textContent = title;
  titleElement2.textContent = title;
  titleElement3.textContent = title;
});
dateInput.addEventListener('input', updateAllReports);
targetInput.addEventListener('input', updateAllReports);
countInput.addEventListener('input', updateAllReports);
desc1Input.addEventListener('input', () => desc1Element.textContent = desc1Input.value);
desc2Input.addEventListener('input', () => desc2Element.textContent = desc2Input.value);
desc3Input.addEventListener('input', () => desc3Element.textContent = desc3Input.value);
desc4Input.addEventListener('input', () => desc4Element.textContent = desc4Input.value);

// تحميل النصوص الافتراضية
function loadDefaultTexts() {
  const selectedReport = reportType.value;
  
  if (!selectedReport) {
    alert('⚠️ الرجاء اختيار نوع التقرير أولاً');
    reportType.focus();
    return;
  }
  
  if (confirm(`هل تريد تحميل النصوص الافتراضية لتقرير "${selectedReport}"؟\n(يمكنك تعديلها لاحقاً كما تشاء)`)) {
    const texts = defaultTexts[selectedReport];
    
    desc1Input.value = texts.desc1;
    desc2Input.value = texts.desc2;
    desc3Input.value = texts.desc3;
    desc4Input.value = texts.desc4;
    
    // تحديث المعاينة
    desc1Element.textContent = texts.desc1;
    desc2Element.textContent = texts.desc2;
    desc3Element.textContent = texts.desc3;
    desc4Element.textContent = texts.desc4;
    
    alert('✅ تم تحميل النصوص الافتراضية بنجاح\nيمكنك الآن تعديلها كما تريد');
  }
}

// مسح حقل معين
function clearField(fieldId) {
  const field = document.getElementById(fieldId);
  field.value = '';
  
  // تحديث المعاينة
  if (fieldId === 'desc1Input') desc1Element.textContent = '';
  if (fieldId === 'desc2Input') desc2Element.textContent = '';
  if (fieldId === 'desc3Input') desc3Element.textContent = '';
  if (fieldId === 'desc4Input') desc4Element.textContent = '';
}

// تحميل الصور
imageInput.addEventListener('change', function(e) {
  const preview = document.getElementById('preview');
  const container = document.getElementById('imagesContainer');
  
  preview.innerHTML = '';
  container.innerHTML = '';
  
  const files = Array.from(e.target.files);
  
  files.forEach((file, index) => {
    if (!file.type.startsWith('image/')) return;
    
    const reader = new FileReader();
    reader.onload = function(e) {
      // صورة المعاينة
      const previewImg = document.createElement('img');
      previewImg.src = e.target.result;
      previewImg.title = `صورة ${index + 1}`;
      preview.appendChild(previewImg);
      
      // صورة التقرير
      const reportImg = document.createElement('img');
      reportImg.src = e.target.result;
      reportImg.alt = `شاهد ${index + 1}`;
      container.appendChild(reportImg);
    };
    reader.readAsDataURL(file);
  });
});

// توليد التقرير
function generateReport() {
  // التحقق من الحقول المطلوبة
  if (!schoolInput.value.trim()) {
    alert('⚠️ الرجاء إدخال اسم المدرسة');
    schoolInput.focus();
    return;
  }
  
  if (!reportType.value) {
    alert('⚠️ الرجاء اختيار نوع التقرير');
    reportType.focus();
    return;
  }
  
  if (!dateInput.value.trim()) {
    alert('⚠️ الرجاء إدخال تاريخ التنفيذ');
    dateInput.focus();
    return;
  }
  
  // تحديث جميع نسخ التقرير
  updateAllReports();
  
  // تعيين قيم افتراضية إذا كانت فارغة
  if (!targetInput.value.trim()) {
    targetElement.textContent = targetElement2.textContent = targetElement3.textContent = 'غير محدد';
  }
  
  if (!countInput.value.trim()) {
    countElement.textContent = countElement2.textContent = countElement3.textContent = 'غير محدد';
  }
  
  if (!desc1Input.value.trim()) {
    desc1Element.textContent = 'لا يوجد وصف';
  }
  
  if (!desc2Input.value.trim()) {
    desc2Element.textContent = 'لا توجد إجراءات محددة';
  }
  
  if (!desc3Input.value.trim()) {
    desc3Element.textContent = 'لا توجد نتائج مسجلة';
  }
  
  if (!desc4Input.value.trim()) {
    desc4Element.textContent = 'لا توجد توصيات';
  }
  
  // إظهار رسالة نجاح
  alert('✅ تم إنشاء التقرير بنجاح! جارٍ فتح نافذة الطباعة...');
  
  // تأخير بسيط لضمان تحديث العناصر
  setTimeout(() => {
    window.print();
  }, 500);
}

// مسح النموذج
function resetForm() {
  if (confirm('هل تريد مسح جميع الحقول؟')) {
    schoolInput.value = '';
    reportType.selectedIndex = 0;
    dateInput.value = '';
    targetInput.value = '';
    countInput.value = '';
    desc1Input.value = '';
    desc2Input.value = '';
    desc3Input.value = '';
    desc4Input.value = '';
    imageInput.value = '';
    
    // مسح المعاينة
    document.getElementById('preview').innerHTML = '';
    document.getElementById('imagesContainer').innerHTML = '';
    
    // إعادة تعيين التقرير
    updateAllReports();
    
    // إعادة تعيين القيم الخاصة
    desc1Element.textContent = '';
    desc2Element.textContent = '';
    desc3Element.textContent = '';
    desc4Element.textContent = '';
    
    alert('✅ تم مسح النموذج بنجاح');
  }
}

// تعيين تاريخ افتراضي
window.onload = function() {
  const today = new Date();
  const formattedDate = `${today.getDate()}/${today.getMonth() + 1}/${today.getFullYear()}`;
  dateInput.value = formattedDate;
  
  // تحديث جميع النسخ بالتاريخ
  updateAllReports();
};
</script>

</body>
</html>