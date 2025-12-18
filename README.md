
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>إعداد تقرير تنفيذ استراتيجية - أداء الواجبات الوظيفية</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://unpkg.com/docx@7.7.0/build/index.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/FileSaver.js/2.0.5/FileSaver.min.js"></script>
    <style>
        /* جميع الأنماط السابقة تبقى كما هي */
        /* Reset & Base Styles */
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        :root {
            --primary-color: #2c5aa0;
            --primary-dark: #1e3d6f;
            --primary-light: #4a7bc8;
            --secondary-color: #f0f4f8;
            --light-color: #f9f9f9;
            --dark-color: #333;
            --gray-color: #666;
            --border-color: #ddd;
            --shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            --radius: 8px;
            --transition: all 0.3s ease;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f5f5f5;
            color: var(--dark-color);
            line-height: 1.6;
            min-height: 100vh;
            padding: 0;
            direction: rtl;
        }

        /* Header */
        .header {
            background: linear-gradient(135deg, var(--primary-color), var(--primary-dark));
            color: white;
            padding: 25px 20px;
            text-align: center;
            position: fixed;
            top: 0;
            width: 100%;
            z-index: 1000;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
        }

        .header h1 {
            font-size: 24px;
            margin-bottom: 10px;
            font-weight: 700;
        }

        .header-subtitle {
            font-size: 16px;
            opacity: 0.9;
        }

        /* Main Content Container */
        .main-container {
            margin-top: 120px;
            padding: 0 20px 40px;
            max-width: 1200px;
            margin-left: auto;
            margin-right: auto;
        }

        /* Report Form Container */
        .report-form-container {
            background-color: white;
            border-radius: var(--radius);
            box-shadow: var(--shadow);
            padding: 30px;
            margin-bottom: 30px;
        }

        /* Section Headers */
        .section-header {
            color: var(--primary-color);
            border-right: 4px solid var(--primary-color);
            padding-right: 15px;
            margin: 30px 0 20px;
            font-size: 22px;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .section-header i {
            font-size: 20px;
        }

        .section-subtitle {
            color: var(--gray-color);
            font-size: 16px;
            margin-bottom: 25px;
            padding-right: 20px;
        }

        /* Form Styles */
        .form-group {
            margin-bottom: 25px;
        }

        .form-label {
            display: block;
            margin-bottom: 10px;
            font-weight: 600;
            color: var(--dark-color);
            font-size: 16px;
        }

        .form-label.required::after {
            content: " *";
            color: #ff6b6b;
        }

        .form-input, .form-select, .form-textarea {
            width: 100%;
            padding: 14px;
            border: 1px solid var(--border-color);
            border-radius: var(--radius);
            font-size: 16px;
            font-family: inherit;
            transition: var(--transition);
            background-color: white;
        }

        .form-input:focus, .form-select:focus, .form-textarea:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(44, 90, 160, 0.1);
        }

        .form-textarea {
            min-height: 120px;
            resize: vertical;
            line-height: 1.6;
        }

        .form-row {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
        }

        /* Form Example */
        .form-example {
            font-size: 14px;
            color: var(--gray-color);
            margin-top: 5px;
            font-style: italic;
        }

        /* Upload Area */
        .upload-section {
            margin-top: 30px;
            border-top: 1px dashed var(--border-color);
            padding-top: 30px;
        }

        .upload-area {
            border: 2px dashed var(--border-color);
            border-radius: var(--radius);
            padding: 40px 20px;
            text-align: center;
            background-color: var(--light-color);
            cursor: pointer;
            transition: var(--transition);
            margin-bottom: 20px;
        }

        .upload-area:hover {
            border-color: var(--primary-color);
            background-color: #f0f7ff;
        }

        .upload-area.dragover {
            border-color: var(--primary-color);
            background-color: #e8f0fe;
        }

        .upload-icon {
            font-size: 48px;
            color: var(--primary-color);
            margin-bottom: 15px;
            opacity: 0.7;
        }

        .upload-text {
            font-size: 16px;
            color: var(--gray-color);
            margin-bottom: 10px;
        }

        .upload-hint {
            font-size: 14px;
            color: var(--gray-color);
        }

        /* Image Preview */
        .image-preview {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }

        .preview-item {
            position: relative;
            border-radius: var(--radius);
            overflow: hidden;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            border: 1px solid var(--border-color);
        }

        .preview-img {
            width: 100%;
            height: 180px;
            object-fit: cover;
            display: block;
        }

        .preview-remove {
            position: absolute;
            top: 10px;
            left: 10px;
            background: rgba(255, 107, 107, 0.9);
            color: white;
            border: none;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 14px;
            transition: var(--transition);
        }

        .preview-remove:hover {
            background: #ff6b6b;
            transform: scale(1.1);
        }

        /* Buttons */
        .btn {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 14px 28px;
            border-radius: var(--radius);
            cursor: pointer;
            font-size: 16px;
            font-weight: 500;
            transition: var(--transition);
            text-decoration: none;
            min-height: 50px;
        }

        .btn:hover {
            background-color: var(--primary-dark);
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        .btn:active {
            transform: translateY(0);
        }

        .btn-secondary {
            background-color: #6c757d;
        }

        .btn-secondary:hover {
            background-color: #5a6268;
        }

        .btn-success {
            background-color: #4caf50;
        }

        .btn-success:hover {
            background-color: #3d8b40;
        }

        .btn-outline {
            background-color: transparent;
            border: 2px solid var(--primary-color);
            color: var(--primary-color);
        }

        .btn-outline:hover {
            background-color: var(--primary-color);
            color: white;
        }

        .btn-block {
            width: 100%;
        }

        /* Action Buttons */
        .action-buttons {
            display: flex;
            justify-content: space-between;
            margin-top: 50px;
            padding-top: 30px;
            border-top: 1px solid var(--border-color);
            gap: 15px;
            flex-wrap: wrap;
        }

        /* Instruction Box */
        .instruction-box {
            background-color: #f0f7ff;
            border-right: 4px solid var(--primary-color);
            padding: 20px;
            border-radius: var(--radius);
            margin-bottom: 30px;
        }

        .instruction-box h3 {
            color: var(--primary-color);
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        /* Export Options Modal */
        .export-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            z-index: 2000;
            align-items: center;
            justify-content: center;
        }

        .export-modal-content {
            background-color: white;
            border-radius: var(--radius);
            width: 90%;
            max-width: 500px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.2);
            animation: modalFade 0.3s;
        }

        @keyframes modalFade {
            from { opacity: 0; transform: translateY(-20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .export-modal-header {
            background-color: var(--primary-color);
            color: white;
            padding: 20px;
            border-radius: var(--radius) var(--radius) 0 0;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .export-modal-title {
            font-size: 20px;
            font-weight: 600;
        }

        .export-modal-close {
            background: none;
            border: none;
            color: white;
            font-size: 24px;
            cursor: pointer;
            width: 30px;
            height: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .export-modal-body {
            padding: 30px;
        }

        .export-options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin: 20px 0;
        }

        .export-option {
            border: 2px solid var(--border-color);
            border-radius: var(--radius);
            padding: 25px 15px;
            text-align: center;
            cursor: pointer;
            transition: var(--transition);
        }

        .export-option:hover {
            border-color: var(--primary-color);
            transform: translateY(-5px);
        }

        .export-option i {
            font-size: 40px;
            margin-bottom: 15px;
            color: var(--primary-color);
        }

        .export-option-title {
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 10px;
            color: var(--dark-color);
        }

        .export-option-desc {
            font-size: 14px;
            color: var(--gray-color);
        }

        .export-actions {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-top: 30px;
        }

        /* Scroll Indicator */
        .scroll-indicator {
            position: fixed;
            bottom: 30px;
            left: 30px;
            background: var(--primary-color);
            color: white;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            cursor: pointer;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
            transition: var(--transition);
            z-index: 100;
        }

        .scroll-indicator:hover {
            background-color: var(--primary-dark);
            transform: scale(1.1);
        }

        .scroll-indicator.hidden {
            display: none;
        }

        /* Responsive Design */
        @media (max-width: 992px) {
            .form-row {
                grid-template-columns: 1fr;
            }
            
            .header h1 {
                font-size: 22px;
            }
            
            .main-container {
                padding: 0 15px 30px;
                margin-top: 110px;
            }
            
            .report-form-container {
                padding: 20px;
            }
            
            .export-options {
                grid-template-columns: 1fr;
            }
        }

        @media (max-width: 768px) {
            .header {
                padding: 20px 15px;
            }
            
            .header h1 {
                font-size: 20px;
            }
            
            .section-header {
                font-size: 20px;
            }
            
            .action-buttons {
                flex-direction: column;
            }
            
            .action-buttons .btn {
                width: 100%;
            }
            
            .scroll-indicator {
                bottom: 20px;
                left: 20px;
                width: 45px;
                height: 45px;
            }
        }

        @media (max-width: 576px) {
            .header h1 {
                font-size: 18px;
            }
            
            .header-subtitle {
                font-size: 14px;
            }
            
            .main-container {
                padding: 0 10px 20px;
                margin-top: 100px;
            }
            
            .report-form-container {
                padding: 15px;
            }
            
            .section-header {
                font-size: 18px;
            }
            
            .form-input, .form-select, .form-textarea {
                padding: 12px;
                font-size: 15px;
            }
            
            .export-modal-content {
                width: 95%;
                margin: 10px;
            }
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 10px;
        }

        ::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 5px;
        }

        ::-webkit-scrollbar-thumb {
            background: #c1c1c1;
            border-radius: 5px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: #a8a8a8;
        }
    </style>
</head>
<body>
    <!-- Header -->
    <div class="header">
        <h1>إعداد تقرير - أداء الواجبات الوظيفية</h1>
        <div class="header-subtitle">تقرير تنفيذ استراتيجية - الإدارة العامة للتعليم بمنطقة الرياض</div>
    </div>

    <!-- Main Content -->
    <div class="main-container">
        <!-- Instruction Box -->
        <div class="instruction-box">
            <h3><i class="fas fa-info-circle"></i> تعليمات إعداد التقرير</h3>
            <p>يرجى تعبئة جميع الحقول المطلوبة (*) بدقة. يمكنك التمرير لأسفل لرؤية كافة أقسام التقرير.</p>
        </div>

        <!-- Report Form -->
        <div class="report-form-container">
            <!-- جميع أقسام النموذج تبقى كما هي -->
            <!-- Section 1: Report Type -->
            <div class="form-section">
                <h2 class="section-header"><i class="fas fa-file-signature"></i> اختيار نوع التقرير</h2>
                <p class="section-subtitle">اختر نوع التقرير لهذا البند</p>
                
                <div class="form-group">
                    <label class="form-label required">أداء الواجبات الوظيفية (البند رقم 1)</label>
                    <select class="form-select" id="reportType">
                        <option value="">اختر نوع التقرير...</option>
                        <option value="strategy" selected>تقرير تنفيذ استراتيجية</option>
                        <option value="activity-session">تقرير حصة النشاط</option>
                        <option value="class-activities">تقرير أنشطة داخل الفصل</option>
                        <option value="remedial">تقرير نشاط إلزائي</option>
                        <option value="visits">تقرير تبادل الزيارات</option>
                    </select>
                </div>
            </div>

            <!-- Section 2: Main Data -->
            <div class="form-section">
                <h2 class="section-header"><i class="fas fa-database"></i> البيانات الرئيسية</h2>
                <p class="section-subtitle">البيانات الرئيسية (تظهر في التقرير)</p>
                
                <div class="form-row">
                    <div class="form-group">
                        <label class="form-label required">اسم المنطقة</label>
                        <input type="text" class="form-input" id="region" placeholder="مثال: الرياض" value="الرياض">
                        <div class="form-example">مثال: الرياض</div>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label required">اسم المدرسة</label>
                        <input type="text" class="form-input" id="school" placeholder="اسم المدرسة" value="مدرسة النموذجية الثانوية">
                    </div>
                </div>
                
                <div class="form-row">
                    <div class="form-group">
                        <label class="form-label required">مدير المدرسة</label>
                        <input type="text" class="form-input" id="principal" placeholder="مدير المدرسة" value="أ. علي محمد أحمد">
                        <div class="form-example">مثال: أ. علي محمد أحمد</div>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label required">معد التقرير</label>
                        <input type="text" class="form-input" id="reporter" placeholder="معد التقرير" value="أ. أحمد عبدالله السعيد">
                        <div class="form-example">مثال: أ. أحمد عبدالله السعيد</div>
                    </div>
                </div>
                
                <div class="form-group">
                    <label class="form-label required">عنوان التقرير</label>
                    <input type="text" class="form-input" id="reportTitle" placeholder="عنوان التقرير" value="تقرير تنفيذ استراتيجية">
                </div>
                
                <div class="form-group">
                    <label class="form-label required">تابع للمناهج (نعم/لا)</label>
                    <select class="form-select" id="curriculumRelated">
                        <option value="نعم" selected>نعم</option>
                        <option value="لا">لا</option>
                    </select>
                </div>
            </div>

            <!-- Section 3: Program Details -->
            <div class="form-section">
                <h2 class="section-header"><i class="fas fa-calendar-alt"></i> تفاصيل البرنامج</h2>
                
                <div class="form-row">
                    <div class="form-group">
                        <label class="form-label required">تاريخ البرنامج (هجري)</label>
                        <input type="text" class="form-input" id="programDate" placeholder="1447-06-12" value="1447-06-12">
                        <div class="form-example">التاريخ الهجري: 1447-06-12</div>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label required">مكان التنفيذ</label>
                        <input type="text" class="form-input" id="location" placeholder="مثال: قاعة مصادر التعلم" value="قاعة مصادر التعلم">
                        <div class="form-example">مثال: قاعة مصادر التعلم - الفصل الدراسي</div>
                    </div>
                </div>
                
                <div class="form-row">
                    <div class="form-group">
                        <label class="form-label required">المستهدفون</label>
                        <input type="text" class="form-input" id="target" placeholder="مثال: طلاب الصف الثالث ثانوي" value="طلاب الصف الثالث ثانوي">
                        <div class="form-example">مثال: طلاب الصف الثالث ثانوي</div>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label required">عدد المستفيدين</label>
                        <input type="number" class="form-input" id="beneficiaries" placeholder="مثال: 25 طالباً" value="25">
                        <div class="form-example">مثال: 25 طالباً</div>
                    </div>
                </div>
            </div>

            <!-- Section 4: Activity Description -->
            <div class="form-section">
                <h2 class="section-header"><i class="fas fa-align-left"></i> وصف النشاط</h2>
                
                <div class="form-group">
                    <label class="form-label required">وصف مختصر لما تم تنفيذه</label>
                    <textarea class="form-textarea" id="description" placeholder="وصف مختصر لما تم تنفيذه في النشاط">تم تنفيذ استراتيجية التدريس وفق الخطة المعتمدة، مع توزيع الطلاب على مجموعات عمل تعاونية وتنويع الأنشطة بما يناسب ميولهم واحتياجاتهم. تم تطبيق استراتيجية التعلم النشط من خلال أنشطة عملية وتفاعلية.</textarea>
                    <div class="form-example">يجب أن يتضمن الوصف ملخصًا واضحًا للنشاط المنفذ</div>
                </div>
            </div>

            <!-- Section 5: Implementation Procedures -->
            <div class="form-section">
                <h2 class="section-header"><i class="fas fa-tasks"></i> إجراءات التنفيذ</h2>
                
                <div class="form-group">
                    <label class="form-label required">إجراءات التنفيذ (افصل بين النقاط بفاصلة)</label>
                    <textarea class="form-textarea" id="procedures" placeholder="أدخل إجراءات التنفيذ">إعداد خطة حصة النشاط وتحديد الأهداف والأنشطة المناسبة, توزيع الطلاب إلى مجموعات عمل وتوضيح المهام لكل مجموعة, توفير المواد والأدوات اللازمة للنشاط, متابعة تنفيذ الطلاب للنشاط وتقديم التوجيه اللازم, تقييم مخرجات النشاط من قبل الطلاب والمعلم</textarea>
                    <div class="form-example">أدخل كل إجراء في سطر جديد أو افصل بين النقاط بفاصلة</div>
                </div>
            </div>

            <!-- Section 6: Results -->
            <div class="form-section">
                <h2 class="section-header"><i class="fas fa-chart-line"></i> النتائج</h2>
                
                <div class="form-group">
                    <label class="form-label required">النتائج (افصل بين النقاط بفاصلة)</label>
                    <textarea class="form-textarea" id="results" placeholder="أدخل النتائج المتحققة">تفاعل إيجابي من الطلاب أثناء تنفيذ استراتيجية التدريس, تنمية روح التعاون والعمل الجماعي بين الطلاب, اكتشاف مواهب الطلاب في مجالات متنوعة, تطبيق المعرفة النظرية في أنشطة عملية, زيادة دافعية الطلاب للتعلم والمشاركة</textarea>
                    <div class="form-example">اذكر النتائج الإيجابية التي تحققت من تنفيذ النشاط</div>
                </div>
            </div>

            <!-- Section 7: Recommendations -->
            <div class="form-section">
                <h2 class="section-header"><i class="fas fa-lightbulb"></i> التوصيات</h2>
                
                <div class="form-group">
                    <label class="form-label required">التوصيات</label>
                    <textarea class="form-textarea" id="recommendations" placeholder="أدخل التوصيات">الاستمرار في تنويع استراتيجيات التدريس وتوثيق الممارسات المميزة لإثراء التجارب المستقبلية. توفير المزيد من الموارد والأدوات اللازمة للأنشطة العملية. تشجيع الطلاب المبدعين للمشاركة في المسابقات والمنافسات الخارجية. عقد ورش عمل للمعلمين لتبادل الخبرات في مجال استراتيجيات التدريس الحديثة.</textarea>
                    <div class="form-example">قدم توصيات للتحسين والتطوير في المستقبل</div>
                </div>
            </div>

            <!-- Section 8: Attachments -->
            <div class="form-section upload-section">
                <h2 class="section-header"><i class="fas fa-images"></i> الصور المرفقة بالتقرير</h2>
                <p class="section-subtitle">صورتان كحد أقصى</p>
                
                <div class="upload-area" id="uploadArea">
                    <div class="upload-icon">
                        <i class="fas fa-cloud-upload-alt"></i>
                    </div>
                    <div class="upload-text">انقر لرفع الصور أو اسحبها إلى هنا</div>
                    <div class="upload-hint">الحجم الأقصى: 5MB لكل صورة | الصيغ المدعومة: JPG, PNG, GIF</div>
                    <input type="file" id="imageUpload" accept="image/*" multiple style="display: none;">
                </div>
                
                <div class="image-preview" id="imagePreview"></div>
                
                <div class="form-group" style="margin-top: 20px;">
                    <label class="form-label">نصائح للصور المرفقة:</label>
                    <ul style="padding-right: 20px; color: var(--gray-color); font-size: 14px;">
                        <li>صورة توثيق تنفيذ النشاط داخل الصف أو ساحة المدرسة</li>
                        <li>صورة لأعمال أو منتجات الطلاب الناتجة عن النشاط</li>
                        <li>صورة لعرض الطلاب لمخرجاتهم أو مشاركتهم في النشاط</li>
                        <li>يفضل إرفاق صور واضحة توثق التنفيذ أو النماذج أو أعمال الطلاب</li>
                    </ul>
                </div>
            </div>

            <!-- Action Buttons -->
            <div class="action-buttons">
                <button class="btn btn-secondary" id="saveDraft">
                    <i class="fas fa-save"></i> حفظ كمسودة
                </button>
                
                <div style="display: flex; gap: 15px;">
                    <button class="btn btn-outline" id="previewReport">
                        <i class="fas fa-eye"></i> معاينة التقرير
                    </button>
                    <button class="btn btn-success" id="submitReport">
                        <i class="fas fa-check-circle"></i> إنشاء التقرير
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Export Options Modal -->
    <div class="export-modal" id="exportModal">
        <div class="export-modal-content">
            <div class="export-modal-header">
                <div class="export-modal-title">
                    <i class="fas fa-download"></i> تصدير التقرير
                </div>
                <button class="export-modal-close" id="closeExportModal">&times;</button>
            </div>
            <div class="export-modal-body">
                <p style="text-align: center; margin-bottom: 20px; color: var(--gray-color);">
                    اختر الصيغة المناسبة لتصدير التقرير
                </p>
                
                <div class="export-options">
                    <div class="export-option" data-format="pdf">
                        <i class="fas fa-file-pdf"></i>
                        <div class="export-option-title">PDF</div>
                        <div class="export-option-desc">نسخة للطباعة والمراجعة</div>
                    </div>
                    
                    <div class="export-option" data-format="word">
                        <i class="fas fa-file-word"></i>
                        <div class="export-option-title">Microsoft Word</div>
                        <div class="export-option-desc">نسخة قابلة للتعديل</div>
                    </div>
                    
                    <div class="export-option" data-format="html">
                        <i class="fas fa-file-code"></i>
                        <div class="export-option-title">HTML</div>
                        <div class="export-option-desc">نسخة ويب تفاعلية</div>
                    </div>
                </div>
                
                <div class="export-actions">
                    <button class="btn btn-outline" id="cancelExport">
                        إلغاء
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Scroll to Top Button -->
    <div class="scroll-indicator hidden" id="scrollToTop">
        <i class="fas fa-arrow-up"></i>
    </div>

    <!-- Scripts -->
    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // ========== العناصر الرئيسية ==========
            const uploadArea = document.getElementById('uploadArea');
            const imageUpload = document.getElementById('imageUpload');
            const imagePreview = document.getElementById('imagePreview');
            const scrollToTopBtn = document.getElementById('scrollToTop');
            const saveDraftBtn = document.getElementById('saveDraft');
            const previewReportBtn = document.getElementById('previewReport');
            const submitReportBtn = document.getElementById('submitReport');
            const exportModal = document.getElementById('exportModal');
            const closeExportModal = document.getElementById('closeExportModal');
            const cancelExport = document.getElementById('cancelExport');
            const exportOptions = document.querySelectorAll('.export-option');
            
            // ========== متغيرات التطبيق ==========
            let uploadedImages = [];
            let currentReportData = null;
            
            // ========== تهيئة الأحداث ==========
            setupEventListeners();
            
            // ========== تحميل البيانات الأولية ==========
            loadInitialData();
            
            // ========== إعداد أحداث العناصر ==========
            function setupEventListeners() {
                // رفع الصور
                uploadArea.addEventListener('click', function() {
                    imageUpload.click();
                });
                
                uploadArea.addEventListener('dragover', function(e) {
                    e.preventDefault();
                    this.classList.add('dragover');
                });
                
                uploadArea.addEventListener('dragleave', function() {
                    this.classList.remove('dragover');
                });
                
                uploadArea.addEventListener('drop', function(e) {
                    e.preventDefault();
                    this.classList.remove('dragover');
                    
                    const files = e.dataTransfer.files;
                    handleImageUpload(files);
                });
                
                imageUpload.addEventListener('change', function(e) {
                    const files = e.target.files;
                    handleImageUpload(files);
                });
                
                // التمرير للأعلى
                scrollToTopBtn.addEventListener('click', function() {
                    window.scrollTo({
                        top: 0,
                        behavior: 'smooth'
                    });
                });
                
                // التحكم في ظهور زر التمرير للأعلى
                window.addEventListener('scroll', function() {
                    if (window.scrollY > 300) {
                        scrollToTopBtn.classList.remove('hidden');
                    } else {
                        scrollToTopBtn.classList.add('hidden');
                    }
                });
                
                // حفظ المسودة
                saveDraftBtn.addEventListener('click', function() {
                    saveAsDraft();
                });
                
                // معاينة التقرير
                previewReportBtn.addEventListener('click', function() {
                    previewReport();
                });
                
                // إنشاء التقرير
                submitReportBtn.addEventListener('click', function() {
                    submitReport();
                });
                
                // التحقق من الحقول المطلوبة
                document.querySelectorAll('.form-input, .form-textarea, .form-select').forEach(input => {
                    input.addEventListener('blur', function() {
                        validateField(this);
                    });
                    
                    input.addEventListener('input', function() {
                        if (this.value.trim()) {
                            this.style.borderColor = '';
                        }
                    });
                });
                
                // التحكم في نافذة التصدير
                closeExportModal.addEventListener('click', function() {
                    exportModal.style.display = 'none';
                });
                
                cancelExport.addEventListener('click', function() {
                    exportModal.style.display = 'none';
                });
                
                // اختيار صيغة التصدير
                exportOptions.forEach(option => {
                    option.addEventListener('click', function() {
                        const format = this.dataset.format;
                        exportReport(format);
                    });
                });
                
                // إغلاق نافذة التصدير عند النقر خارجها
                window.addEventListener('click', function(event) {
                    if (event.target === exportModal) {
                        exportModal.style.display = 'none';
                    }
                });
            }
            
            // ========== معالجة رفع الصور ==========
            function handleImageUpload(files) {
                // التحقق من عدد الصور
                if (uploadedImages.length + files.length > 2) {
                    alert('يمكنك رفع صورتين كحد أقصى فقط');
                    return;
                }
                
                for (let i = 0; i < files.length; i++) {
                    const file = files[i];
                    
                    // التحقق من نوع الملف
                    if (!file.type.startsWith('image/')) {
                        alert('الرجاء رفع ملفات صور فقط (JPG, PNG, GIF)');
                        continue;
                    }
                    
                    // التحقق من حجم الملف (5MB)
                    if (file.size > 5 * 1024 * 1024) {
                        alert('حجم الصورة يجب أن يكون أقل من 5MB');
                        continue;
                    }
                    
                    const reader = new FileReader();
                    
                    reader.onload = function(e) {
                        uploadedImages.push({
                            data: e.target.result,
                            name: file.name,
                            type: file.type
                        });
                        updateImagePreview();
                    };
                    
                    reader.readAsDataURL(file);
                }
                
                // إعادة تعيين حقل الرفع
                imageUpload.value = '';
            }
            
            // ========== تحديث معاينة الصور ==========
            function updateImagePreview() {
                imagePreview.innerHTML = '';
                
                uploadedImages.forEach((imgData, index) => {
                    const item = document.createElement('div');
                    item.className = 'preview-item';
                    
                    item.innerHTML = `
                        <img src="${imgData.data}" class="preview-img" alt="صورة ${index + 1}">
                        <button class="preview-remove" data-index="${index}">
                            <i class="fas fa-times"></i>
                        </button>
                    `;
                    
                    imagePreview.appendChild(item);
                });
                
                // إضافة أحداث لحذف الصور
                document.querySelectorAll('.preview-remove').forEach(btn => {
                    btn.addEventListener('click', function() {
                        const index = parseInt(this.dataset.index);
                        uploadedImages.splice(index, 1);
                        updateImagePreview();
                    });
                });
            }
            
            // ========== تحميل البيانات الأولية ==========
            function loadInitialData() {
                // إخفاء زر التمرير للأعلى في البداية
                scrollToTopBtn.classList.add('hidden');
                
                // تحميل المسودة المحفوظة إن وجدت
                const savedDraft = localStorage.getItem('reportDraft');
                if (savedDraft) {
                    try {
                        const draftData = JSON.parse(savedDraft);
                        if (confirm('يوجد تقرير محفوظ كمسودة. هل تريد استكماله؟')) {
                            loadDraftData(draftData);
                        }
                    } catch (e) {
                        console.error('Error loading draft:', e);
                    }
                }
            }
            
            // ========== تحميل بيانات المسودة ==========
            function loadDraftData(draftData) {
                document.getElementById('reportType').value = draftData.type || 'strategy';
                document.getElementById('reportTitle').value = draftData.title || 'تقرير تنفيذ استراتيجية';
                document.getElementById('curriculumRelated').value = draftData.curriculumRelated || 'نعم';
                document.getElementById('programDate').value = draftData.programDate || '1447-06-12';
                document.getElementById('location').value = draftData.location || '';
                document.getElementById('target').value = draftData.target || '';
                document.getElementById('beneficiaries').value = draftData.beneficiaries || '25';
                document.getElementById('description').value = draftData.description || '';
                document.getElementById('procedures').value = draftData.procedures ? (Array.isArray(draftData.procedures) ? draftData.procedures.join(', ') : draftData.procedures) : '';
                document.getElementById('results').value = draftData.results ? (Array.isArray(draftData.results) ? draftData.results.join(', ') : draftData.results) : '';
                document.getElementById('recommendations').value = draftData.recommendations || '';
                
                // تحميل الصور
                if (draftData.images && draftData.images.length > 0) {
                    uploadedImages = [...draftData.images];
                    updateImagePreview();
                }
                
                alert('تم تحميل بيانات المسودة بنجاح');
            }
            
            // ========== التحقق من الحقول ==========
            function validateField(field) {
                if (field.hasAttribute('required') && !field.value.trim()) {
                    field.style.borderColor = '#ff6b6b';
                    return false;
                }
                
                field.style.borderColor = '';
                return true;
            }
            
            // ========== التحقق من النموذج كامل ==========
            function validateForm() {
                let isValid = true;
                const requiredFields = document.querySelectorAll('[required]');
                
                requiredFields.forEach(field => {
                    if (!validateField(field)) {
                        isValid = false;
                    }
                });
                
                return isValid;
            }
            
            // ========== حفظ كمسودة ==========
            function saveAsDraft() {
                if (!validateForm()) {
                    alert('يرجى ملء جميع الحقول المطلوبة قبل الحفظ');
                    return;
                }
                
                const reportData = collectReportData();
                reportData.status = 'draft';
                reportData.savedAt = new Date().toLocaleString('ar-SA');
                
                // حفظ البيانات
                localStorage.setItem('reportDraft', JSON.stringify(reportData));
                
                alert('تم حفظ التقرير كمسودة بنجاح!\n' + reportData.savedAt);
            }
            
            // ========== معاينة التقرير ==========
            function previewReport() {
                if (!validateForm()) {
                    alert('يرجى ملء جميع الحقول المطلوبة قبل المعاينة');
                    return;
                }
                
                currentReportData = collectReportData();
                
                // فتح نافذة جديدة للمعاينة
                const previewWindow = window.open('', '_blank');
                previewWindow.document.write(generatePreviewHTML(currentReportData));
                previewWindow.document.close();
            }
            
            // ========== إنشاء التقرير النهائي ==========
            function submitReport() {
                if (!validateForm()) {
                    alert('يرجى ملء جميع الحقول المطلوبة قبل الإنشاء');
                    return;
                }
                
                currentReportData = collectReportData();
                currentReportData.status = 'completed';
                currentReportData.submissionDate = new Date().toLocaleDateString('ar-SA');
                currentReportData.reportNumber = generateReportNumber();
                
                // عرض نافذة اختيار صيغة التصدير
                exportModal.style.display = 'flex';
            }
            
            // ========== تصدير التقرير ==========
            async function exportReport(format) {
                if (!currentReportData) {
                    alert('لا توجد بيانات للتقرير');
                    return;
                }
                
                exportModal.style.display = 'none';
                
                switch(format) {
                    case 'pdf':
                        await exportToPDF();
                        break;
                    case 'word':
                        await exportToWord();
                        break;
                    case 'html':
                        exportToHTML();
                        break;
                }
                
                // حفظ التقرير النهائي
                currentReportData.exportedAt = new Date().toLocaleString('ar-SA');
                currentReportData.exportFormat = format;
                localStorage.setItem('lastReport', JSON.stringify(currentReportData));
                
                // عرض رسالة النجاح
                alert(`تم تصدير التقرير بنجاح إلى صيغة ${format.toUpperCase()}!\nرقم التقرير: ${currentReportData.reportNumber}`);
                
                // إعادة تعيين النموذج
                setTimeout(() => {
                    if (confirm('هل تريد إعادة تعيين النموذج لبدء تقرير جديد؟')) {
                        resetForm();
                    }
                }, 1000);
            }
            
            // ========== تصدير إلى PDF ==========
            async function exportToPDF() {
                const { jsPDF } = window.jspdf;
                const doc = new jsPDF({
                    orientation: 'portrait',
                    unit: 'mm',
                    format: 'a4'
                });
                
                // إضافة دعم النصوص العربية
                doc.setFont('Times', 'normal');
                doc.setFontSize(12);
                
                // العنوان الرئيسي
                doc.setFontSize(16);
                doc.setTextColor(44, 90, 160);
                doc.text(currentReportData.title, 105, 20, { align: 'center' });
                
                // معلومات التقرير
                doc.setFontSize(12);
                doc.setTextColor(0, 0, 0);
                doc.text(`الإدارة العامة للتعليم بمنطقة ${currentReportData.region}`, 105, 30, { align: 'center' });
                doc.text(`تاريخ البرنامج: ${currentReportData.programDate}`, 105, 35, { align: 'center' });
                
                // الخط الفاصل
                doc.setDrawColor(44, 90, 160);
                doc.setLineWidth(0.5);
                doc.line(20, 40, 190, 40);
                
                let yPos = 50;
                
                // البيانات الأساسية
                doc.setFontSize(14);
                doc.setTextColor(44, 90, 160);
                doc.text('البيانات الأساسية', 190, yPos, { align: 'right' });
                yPos += 10;
                
                doc.setFontSize(12);
                doc.setTextColor(0, 0, 0);
                doc.text(`المدرسة: ${currentReportData.school}`, 190, yPos, { align: 'right' });
                yPos += 7;
                doc.text(`مدير المدرسة: ${currentReportData.principal}`, 190, yPos, { align: 'right' });
                yPos += 7;
                doc.text(`معد التقرير: ${currentReportData.reporter}`, 190, yPos, { align: 'right' });
                yPos += 7;
                doc.text(`مكان التنفيذ: ${currentReportData.location}`, 190, yPos, { align: 'right' });
                yPos += 7;
                doc.text(`المستهدفون: ${currentReportData.target}`, 190, yPos, { align: 'right' });
                yPos += 7;
                doc.text(`عدد المستفيدين: ${currentReportData.beneficiaries}`, 190, yPos, { align: 'right' });
                yPos += 7;
                doc.text(`تابع للمناهج: ${currentReportData.curriculumRelated}`, 190, yPos, { align: 'right' });
                yPos += 15;
                
                // وصف النشاط
                doc.setFontSize(14);
                doc.setTextColor(44, 90, 160);
                doc.text('وصف مختصر لما تم تنفيذه', 190, yPos, { align: 'right' });
                yPos += 10;
                
                doc.setFontSize(12);
                doc.setTextColor(0, 0, 0);
                const descriptionLines = doc.splitTextToSize(currentReportData.description, 170);
                doc.text(descriptionLines, 190, yPos, { align: 'right' });
                yPos += (descriptionLines.length * 7) + 10;
                
                // إجراءات التنفيذ
                if (currentReportData.procedures && currentReportData.procedures.length > 0) {
                    doc.setFontSize(14);
                    doc.setTextColor(44, 90, 160);
                    doc.text('إجراءات التنفيذ', 190, yPos, { align: 'right' });
                    yPos += 10;
                    
                    doc.setFontSize(12);
                    doc.setTextColor(0, 0, 0);
                    currentReportData.procedures.forEach((procedure, index) => {
                        const procLines = doc.splitTextToSize(`${index + 1}. ${procedure}`, 170);
                        doc.text(procLines, 190, yPos, { align: 'right' });
                        yPos += (procLines.length * 7) + 5;
                    });
                    yPos += 5;
                }
                
                // إذا تجاوزنا صفحة، نضيف صفحة جديدة
                if (yPos > 250) {
                    doc.addPage();
                    yPos = 20;
                }
                
                // النتائج
                if (currentReportData.results && currentReportData.results.length > 0) {
                    doc.setFontSize(14);
                    doc.setTextColor(44, 90, 160);
                    doc.text('النتائج', 190, yPos, { align: 'right' });
                    yPos += 10;
                    
                    doc.setFontSize(12);
                    doc.setTextColor(0, 0, 0);
                    currentReportData.results.forEach((result, index) => {
                        const resultLines = doc.splitTextToSize(`${index + 1}. ${result}`, 170);
                        doc.text(resultLines, 190, yPos, { align: 'right' });
                        yPos += (resultLines.length * 7) + 5;
                    });
                    yPos += 5;
                }
                
                // التوصيات
                doc.setFontSize(14);
                doc.setTextColor(44, 90, 160);
                doc.text('التوصيات', 190, yPos, { align: 'right' });
                yPos += 10;
                
                doc.setFontSize(12);
                doc.setTextColor(0, 0, 0);
                const recommendationLines = doc.splitTextToSize(currentReportData.recommendations, 170);
                doc.text(recommendationLines, 190, yPos, { align: 'right' });
                yPos += (recommendationLines.length * 7) + 15;
                
                // التوقيعات
                doc.setLineWidth(0.3);
                doc.line(20, yPos, 190, yPos);
                yPos += 10;
                
                doc.setFontSize(12);
                doc.text(`مدير المدرسة: ${currentReportData.principal}`, 40, yPos);
                doc.text('التوقيع: _______________', 40, yPos + 7);
                
                doc.text(`معد التقرير: ${currentReportData.reporter}`, 140, yPos);
                doc.text('التوقيع: _______________', 140, yPos + 7);
                
                // حفظ الملف
                doc.save(`تقرير_${currentReportData.reportNumber}.pdf`);
            }
            
            // ========== تصدير إلى Word ==========
            async function exportToWord() {
                const docx = window.docx;
                
                // إنشاء محتوى الوثيقة
                const doc = new docx.Document({
                    sections: [{
                        properties: {
                            direction: "rtl"
                        },
                        children: [
                            // العنوان
                            new docx.Paragraph({
                                text: currentReportData.title,
                                heading: docx.HeadingLevel.TITLE,
                                alignment: docx.AlignmentType.CENTER,
                                spacing: {
                                    after: 200
                                }
                            }),
                            
                            // معلومات التقرير
                            new docx.Paragraph({
                                text: `الإدارة العامة للتعليم بمنطقة ${currentReportData.region}`,
                                alignment: docx.AlignmentType.CENTER
                            }),
                            new docx.Paragraph({
                                text: `تاريخ البرنامج: ${currentReportData.programDate}`,
                                alignment: docx.AlignmentType.CENTER,
                                spacing: {
                                    after: 200
                                }
                            }),
                            
                            // البيانات الأساسية
                            new docx.Paragraph({
                                text: "البيانات الأساسية",
                                heading: docx.HeadingLevel.HEADING_1,
                                spacing: {
                                    before: 200
                                }
                            }),
                            new docx.Paragraph({
                                text: `المدرسة: ${currentReportData.school}`
                            }),
                            new docx.Paragraph({
                                text: `مدير المدرسة: ${currentReportData.principal}`
                            }),
                            new docx.Paragraph({
                                text: `معد التقرير: ${currentReportData.reporter}`
                            }),
                            new docx.Paragraph({
                                text: `مكان التنفيذ: ${currentReportData.location}`
                            }),
                            new docx.Paragraph({
                                text: `المستهدفون: ${currentReportData.target}`
                            }),
                            new docx.Paragraph({
                                text: `عدد المستفيدين: ${currentReportData.beneficiaries}`,
                                spacing: {
                                    after: 200
                                }
                            }),
                            
                            // وصف النشاط
                            new docx.Paragraph({
                                text: "وصف مختصر لما تم تنفيذه",
                                heading: docx.HeadingLevel.HEADING_1
                            }),
                            new docx.Paragraph({
                                text: currentReportData.description,
                                spacing: {
                                    after: 200
                                }
                            }),
                            
                            // إجراءات التنفيذ
                            new docx.Paragraph({
                                text: "إجراءات التنفيذ",
                                heading: docx.HeadingLevel.HEADING_1
                            }),
                            ...(currentReportData.procedures || []).map(procedure => 
                                new docx.Paragraph({
                                    text: `• ${procedure}`,
                                    bullet: {
                                        level: 0
                                    }
                                })
                            ),
                            
                            new docx.Paragraph({
                                spacing: {
                                    after: 200
                                }
                            }),
                            
                            // النتائج
                            new docx.Paragraph({
                                text: "النتائج",
                                heading: docx.HeadingLevel.HEADING_1
                            }),
                            ...(currentReportData.results || []).map(result => 
                                new docx.Paragraph({
                                    text: `• ${result}`,
                                    bullet: {
                                        level: 0
                                    }
                                })
                            ),
                            
                            new docx.Paragraph({
                                spacing: {
                                    after: 200
                                }
                            }),
                            
                            // التوصيات
                            new docx.Paragraph({
                                text: "التوصيات",
                                heading: docx.HeadingLevel.HEADING_1
                            }),
                            new docx.Paragraph({
                                text: currentReportData.recommendations,
                                spacing: {
                                    after: 200
                                }
                            }),
                            
                            // التوقيعات
                            new docx.Paragraph({
                                children: [
                                    new docx.TextRun({
                                        text: "مدير المدرسة: ",
                                        bold: true
                                    }),
                                    new docx.TextRun(currentReportData.principal)
                                ]
                            }),
                            new docx.Paragraph({
                                text: "التوقيع: _______________",
                                spacing: {
                                    after: 100
                                }
                            }),
                            
                            new docx.Paragraph({
                                children: [
                                    new docx.TextRun({
                                        text: "معد التقرير: ",
                                        bold: true
                                    }),
                                    new docx.TextRun(currentReportData.reporter)
                                ]
                            }),
                            new docx.Paragraph({
                                text: "التوقيع: _______________"
                            })
                        ]
                    }]
                });
                
                // تحميل الوثيقة
                const buffer = await docx.Packer.toBlob(doc);
                saveAs(buffer, `تقرير_${currentReportData.reportNumber}.docx`);
            }
            
            // ========== تصدير إلى HTML ==========
            function exportToHTML() {
                const htmlContent = generatePreviewHTML(currentReportData);
                const blob = new Blob([htmlContent], { type: 'text/html' });
                saveAs(blob, `تقرير_${currentReportData.reportNumber}.html`);
            }
            
            // ========== جمع بيانات التقرير ==========
            function collectReportData() {
                return {
                    type: document.getElementById('reportType').value,
                    region: document.getElementById('region').value,
                    school: document.getElementById('school').value,
                    principal: document.getElementById('principal').value,
                    reporter: document.getElementById('reporter').value,
                    title: document.getElementById('reportTitle').value,
                    curriculumRelated: document.getElementById('curriculumRelated').value,
                    programDate: document.getElementById('programDate').value,
                    location: document.getElementById('location').value,
                    target: document.getElementById('target').value,
                    beneficiaries: document.getElementById('beneficiaries').value,
                    description: document.getElementById('description').value,
                    procedures: document.getElementById('procedures').value.split(',').map(p => p.trim()).filter(p => p),
                    results: document.getElementById('results').value.split(',').map(r => r.trim()).filter(r => r),
                    recommendations: document.getElementById('recommendations').value,
                    images: [...uploadedImages]
                };
            }
            
            // ========== توليد HTML للمعاينة ==========
            function generatePreviewHTML(reportData) {
                return `
                    <!DOCTYPE html>
                    <html dir="rtl" lang="ar">
                    <head>
                        <meta charset="UTF-8">
                        <meta name="viewport" content="width=device-width, initial-scale=1.0">
                        <title>${reportData.title}</title>
                        <style>
                            body { 
                                font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; 
                                padding: 30px; 
                                direction: rtl; 
                                line-height: 1.8;
                                color: #333;
                                background-color: #f9f9f9;
                            }
                            .report-container {
                                max-width: 1000px;
                                margin: 0 auto;
                                background: white;
                                padding: 40px;
                                box-shadow: 0 0 20px rgba(0,0,0,0.1);
                                border-radius: 10px;
                            }
                            h1 { 
                                color: #2c5aa0; 
                                text-align: center; 
                                margin-bottom: 20px;
                                font-size: 28px;
                            }
                            .header { 
                                text-align: center; 
                                margin-bottom: 40px;
                                padding-bottom: 20px;
                                border-bottom: 2px solid #2c5aa0;
                            }
                            .section { 
                                margin-bottom: 35px;
                                padding: 20px;
                                background: #f8fafc;
                                border-radius: 8px;
                                border-right: 4px solid #2c5aa0;
                            }
                            .section-title { 
                                color: #2c5aa0; 
                                border-right: 3px solid #2c5aa0; 
                                padding-right: 15px;
                                margin-bottom: 20px;
                                font-size: 22px;
                            }
                            .info-item {
                                margin-bottom: 12px;
                                font-size: 16px;
                            }
                            .info-item strong {
                                color: #2c5aa0;
                                min-width: 150px;
                                display: inline-block;
                            }
                            .images { 
                                display: flex; 
                                gap: 20px; 
                                flex-wrap: wrap; 
                                margin-top: 15px; 
                                justify-content: center;
                            }
                            .image-container { 
                                max-width: 300px; 
                                border: 1px solid #ddd; 
                                padding: 15px;
                                border-radius: 8px;
                                background: white;
                            }
                            .image-container img { 
                                width: 100%; 
                                height: auto;
                                border-radius: 4px;
                            }
                            .signatures {
                                display: flex;
                                justify-content: space-around;
                                margin-top: 60px;
                                padding-top: 30px;
                                border-top: 2px solid #2c5aa0;
                            }
                            .signature-box {
                                text-align: center;
                                width: 300px;
                            }
                            .signature-line {
                                width: 200px;
                                height: 2px;
                                background: #333;
                                margin: 30px auto 10px;
                            }
                            @media print {
                                body { background: white; }
                                .report-container { box-shadow: none; }
                                .images { page-break-inside: avoid; }
                            }
                        </style>
                    </head>
                    <body>
                        <div class="report-container">
                            <div class="header">
                                <h1>${reportData.title}</h1>
                                <p style="font-size: 18px;">الإدارة العامة للتعليم بمنطقة ${reportData.region}</p>
                                <p style="font-size: 16px; color: #666;">تاريخ البرنامج: ${reportData.programDate}</p>
                                <p style="font-size: 14px; color: #888;">رقم التقرير: ${reportData.reportNumber || 'TR-' + new Date().getTime()}</p>
                            </div>
                            
                            <div class="section">
                                <h3 class="section-title">البيانات الأساسية</h3>
                                <div class="info-item"><strong>المدرسة:</strong> ${reportData.school}</div>
                                <div class="info-item"><strong>مدير المدرسة:</strong> ${reportData.principal}</div>
                                <div class="info-item"><strong>معد التقرير:</strong> ${reportData.reporter}</div>
                                <div class="info-item"><strong>مكان التنفيذ:</strong> ${reportData.location}</div>
                                <div class="info-item"><strong>المستهدفون:</strong> ${reportData.target}</div>
                                <div class="info-item"><strong>عدد المستفيدين:</strong> ${reportData.beneficiaries}</div>
                                <div class="info-item"><strong>تابع للمناهج:</strong> ${reportData.curriculumRelated}</div>
                            </div>
                            
                            <div class="section">
                                <h3 class="section-title">وصف مختصر لما تم تنفيذه</h3>
                                <p style="font-size: 16px; text-align: justify;">${reportData.description}</p>
                            </div>
                            
                            ${reportData.procedures && reportData.procedures.length > 0 ? `
                            <div class="section">
                                <h3 class="section-title">إجراءات التنفيذ</h3>
                                <ol style="padding-right: 20px; font-size: 16px;">
                                    ${reportData.procedures.map(proc => `<li style="margin-bottom: 10px;">${proc}</li>`).join('')}
                                </ol>
                            </div>
                            ` : ''}
                            
                            ${reportData.results && reportData.results.length > 0 ? `
                            <div class="section">
                                <h3 class="section-title">النتائج</h3>
                                <ol style="padding-right: 20px; font-size: 16px;">
                                    ${reportData.results.map(result => `<li style="margin-bottom: 10px;">${result}</li>`).join('')}
                                </ol>
                            </div>
                            ` : ''}
                            
                            <div class="section">
                                <h3 class="section-title">التوصيات</h3>
                                <p style="font-size: 16px; text-align: justify;">${reportData.recommendations}</p>
                            </div>
                            
                            ${reportData.images && reportData.images.length > 0 ? `
                            <div class="section">
                                <h3 class="section-title">الصور المرفقة</h3>
                                <div class="images">
                                    ${reportData.images.map((img, idx) => `
                                        <div class="image-container">
                                            <img src="${img.data}" alt="صورة ${idx + 1}">
                                            <p style="text-align:center; margin-top:10px; color: #666;">صورة ${idx + 1}</p>
                                        </div>
                                    `).join('')}
                                </div>
                            </div>
                            ` : ''}
                            
                            <div class="signatures">
                                <div class="signature-box">
                                    <p><strong>مدير المدرسة:</strong></p>
                                    <p>${reportData.principal}</p>
                                    <div class="signature-line"></div>
                                    <p>التوقيع</p>
                                </div>
                                
                                <div class="signature-box">
                                    <p><strong>معد التقرير:</strong></p>
                                    <p>${reportData.reporter}</p>
                                    <div class="signature-line"></div>
                                    <p>التوقيع</p>
                                </div>
                            </div>
                            
                            <div style="text-align: center; margin-top: 40px; color: #888; font-size: 14px;">
                                <p>تم إنشاء هذا التقرير بواسطة نظام إعداد التقارير - ${new Date().toLocaleDateString('ar-SA')}</p>
                            </div>
                        </div>
                    </body>
                    </html>
                `;
            }
            
            // ========== توليد رقم التقرير ==========
            function generateReportNumber() {
                const prefix = 'TR';
                const year = new Date().getFullYear();
                const month = (new Date().getMonth() + 1).toString().padStart(2, '0');
                const day = new Date().getDate().toString().padStart(2, '0');
                const random = Math.floor(Math.random() * 1000).toString().padStart(3, '0');
                return `${prefix}-${year}${month}${day}-${random}`;
            }
            
            // ========== إعادة تعيين النموذج ==========
            function resetForm() {
                // إعادة تعيين الحقول
                document.getElementById('programDate').value = '1447-06-12';
                document.getElementById('location').value = '';
                document.getElementById('target').value = '';
                document.getElementById('beneficiaries').value = '25';
                document.getElementById('description').value = '';
                document.getElementById('procedures').value = '';
                document.getElementById('results').value = '';
                document.getElementById('recommendations').value = '';
                
                // إعادة تعيين الصور
                uploadedImages = [];
                imagePreview.innerHTML = '';
                
                // حذف المسودة
                localStorage.removeItem('reportDraft');
                
                // التمرير للأعلى
                window.scrollTo({
                    top: 0,
                    behavior: 'smooth'
                });
            }
            
            // ========== الحفظ التلقائي ==========
            setInterval(() => {
                if (validateForm()) {
                    const reportData = collectReportData();
                    reportData.status = 'draft';
                    reportData.autoSaved = new Date().toLocaleTimeString('ar-SA');
                    localStorage.setItem('reportDraft', JSON.stringify(reportData));
                }
            }, 30000);
        });
    </script>
</body>
</html>