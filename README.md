<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام إعداد التقارير - أداء الواجبات الوظيفية</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://unpkg.com/docx@7.7.0/build/index.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/FileSaver.js/2.0.5/FileSaver.min.js"></script>
    <style>
        :root {
            --primary-color: #2c5aa0;
            --primary-dark: #1e3d6f;
            --primary-light: #4a7bc8;
            --secondary-color: #f0f4f8;
            --light-color: #f9f9f9;
            --dark-color: #333;
            --gray-color: #666;
            --border-color: #ddd;
            --success-color: #28a745;
            --warning-color: #ffc107;
            --danger-color: #dc3545;
            --shadow: 0 2px 15px rgba(0, 0, 0, 0.08);
            --shadow-lg: 0 5px 25px rgba(0, 0, 0, 0.1);
            --radius: 10px;
            --transition: all 0.3s ease;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Segoe UI', 'Cairo', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #f5f7fa 0%, #e4e8f0 100%);
            color: var(--dark-color);
            line-height: 1.6;
            min-height: 100vh;
            padding: 0;
            direction: rtl;
        }

        /* Header */
        .header {
            background: linear-gradient(135deg, var(--primary-color) 0%, var(--primary-dark) 100%);
            color: white;
            padding: 25px 20px;
            text-align: center;
            position: fixed;
            top: 0;
            width: 100%;
            z-index: 1000;
            box-shadow: var(--shadow-lg);
        }

        .header h1 {
            font-size: 26px;
            margin-bottom: 8px;
            font-weight: 700;
            text-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }

        .header-subtitle {
            font-size: 16px;
            opacity: 0.9;
            font-weight: 300;
        }

        /* Main Container */
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
            box-shadow: var(--shadow-lg);
            padding: 40px;
            margin-bottom: 30px;
            border: 1px solid rgba(255,255,255,0.2);
            position: relative;
            overflow: hidden;
        }

        .report-form-container::before {
            content: '';
            position: absolute;
            top: 0;
            right: 0;
            width: 100%;
            height: 5px;
            background: linear-gradient(90deg, var(--primary-color) 0%, var(--primary-light) 100%);
        }

        /* Section Headers */
        .section-header {
            color: var(--primary-color);
            border-right: 5px solid var(--primary-color);
            padding-right: 20px;
            margin: 40px 0 25px;
            font-size: 24px;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 12px;
            position: relative;
        }

        .section-header i {
            font-size: 22px;
            background: rgba(44, 90, 160, 0.1);
            padding: 10px;
            border-radius: 8px;
            width: 50px;
            height: 50px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .section-subtitle {
            color: var(--gray-color);
            font-size: 16px;
            margin-bottom: 30px;
            padding-right: 25px;
            line-height: 1.7;
        }

        /* Form Styles */
        .form-group {
            margin-bottom: 30px;
        }

        .form-label {
            display: block;
            margin-bottom: 12px;
            font-weight: 600;
            color: var(--dark-color);
            font-size: 16px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .form-label i {
            color: var(--primary-color);
            font-size: 18px;
        }

        .form-label.required::after {
            content: " *";
            color: var(--danger-color);
            font-weight: bold;
        }

        .form-input, .form-select, .form-textarea {
            width: 100%;
            padding: 16px;
            border: 2px solid var(--border-color);
            border-radius: var(--radius);
            font-size: 16px;
            font-family: inherit;
            transition: var(--transition);
            background-color: white;
            box-shadow: inset 0 2px 4px rgba(0,0,0,0.05);
        }

        .form-input:focus, .form-select:focus, .form-textarea:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 4px rgba(44, 90, 160, 0.15);
        }

        .form-textarea {
            min-height: 140px;
            resize: vertical;
            line-height: 1.8;
        }

        .form-row {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
        }

        /* Form Example */
        .form-example {
            font-size: 14px;
            color: var(--gray-color);
            margin-top: 8px;
            font-style: italic;
            padding-right: 5px;
        }

        /* Upload Area */
        .upload-section {
            margin-top: 40px;
            border-top: 2px dashed var(--border-color);
            padding-top: 40px;
        }

        .upload-area {
            border: 3px dashed var(--border-color);
            border-radius: var(--radius);
            padding: 50px 30px;
            text-align: center;
            background-color: var(--light-color);
            cursor: pointer;
            transition: var(--transition);
            margin-bottom: 25px;
            position: relative;
            overflow: hidden;
        }

        .upload-area:hover {
            border-color: var(--primary-color);
            background-color: rgba(44, 90, 160, 0.02);
            transform: translateY(-2px);
        }

        .upload-area.dragover {
            border-color: var(--primary-color);
            background-color: rgba(44, 90, 160, 0.05);
            animation: pulse 1.5s infinite;
        }

        @keyframes pulse {
            0% { box-shadow: 0 0 0 0 rgba(44, 90, 160, 0.2); }
            70% { box-shadow: 0 0 0 15px rgba(44, 90, 160, 0); }
            100% { box-shadow: 0 0 0 0 rgba(44, 90, 160, 0); }
        }

        .upload-icon {
            font-size: 56px;
            color: var(--primary-color);
            margin-bottom: 20px;
            opacity: 0.8;
        }

        .upload-text {
            font-size: 18px;
            color: var(--dark-color);
            margin-bottom: 12px;
            font-weight: 500;
        }

        .upload-hint {
            font-size: 15px;
            color: var(--gray-color);
            max-width: 500px;
            margin: 0 auto;
        }

        /* Image Preview */
        .image-preview {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }

        .preview-item {
            position: relative;
            border-radius: var(--radius);
            overflow: hidden;
            box-shadow: var(--shadow);
            border: 1px solid var(--border-color);
            transition: var(--transition);
        }

        .preview-item:hover {
            transform: translateY(-5px);
            box-shadow: var(--shadow-lg);
        }

        .preview-img {
            width: 100%;
            height: 200px;
            object-fit: cover;
            display: block;
            transition: var(--transition);
        }

        .preview-item:hover .preview-img {
            transform: scale(1.05);
        }

        .preview-remove {
            position: absolute;
            top: 15px;
            left: 15px;
            background: rgba(220, 53, 69, 0.9);
            color: white;
            border: none;
            width: 35px;
            height: 35px;
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 16px;
            transition: var(--transition);
            box-shadow: 0 2px 8px rgba(0,0,0,0.2);
        }

        .preview-remove:hover {
            background: var(--danger-color);
            transform: scale(1.1);
        }

        /* Buttons */
        .btn {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 16px 32px;
            border-radius: var(--radius);
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            transition: var(--transition);
            text-decoration: none;
            min-height: 55px;
            box-shadow: 0 4px 12px rgba(44, 90, 160, 0.2);
            position: relative;
            overflow: hidden;
        }

        .btn::after {
            content: '';
            position: absolute;
            top: 50%;
            right: 50%;
            width: 0;
            height: 0;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 50%;
            transform: translate(50%, -50%);
            transition: width 0.6s, height 0.6s;
        }

        .btn:hover::after {
            width: 300px;
            height: 300px;
        }

        .btn:hover {
            background-color: var(--primary-dark);
            transform: translateY(-3px);
            box-shadow: 0 6px 18px rgba(44, 90, 160, 0.3);
        }

        .btn:active {
            transform: translateY(-1px);
        }

        .btn-secondary {
            background-color: #6c757d;
        }

        .btn-secondary:hover {
            background-color: #5a6268;
        }

        .btn-success {
            background-color: var(--success-color);
        }

        .btn-success:hover {
            background-color: #218838;
        }

        .btn-outline {
            background-color: transparent;
            border: 2px solid var(--primary-color);
            color: var(--primary-color);
            box-shadow: none;
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
            margin-top: 60px;
            padding-top: 40px;
            border-top: 2px solid var(--border-color);
            gap: 20px;
            flex-wrap: wrap;
        }

        /* Instruction Box */
        .instruction-box {
            background: linear-gradient(135deg, #f0f7ff 0%, #e8f0fe 100%);
            border-right: 5px solid var(--primary-color);
            padding: 25px;
            border-radius: var(--radius);
            margin-bottom: 40px;
            box-shadow: var(--shadow);
            position: relative;
            overflow: hidden;
        }

        .instruction-box::before {
            content: '';
            position: absolute;
            top: 0;
            right: 0;
            width: 100px;
            height: 100px;
            background: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Cpath fill='%232c5aa0' fill-opacity='0.05' d='M0,0 L100,0 L100,100 Z'/%3E%3C/svg%3E");
            background-size: cover;
        }

        .instruction-box h3 {
            color: var(--primary-color);
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 12px;
            font-size: 22px;
        }

        .instruction-box p {
            color: var(--dark-color);
            font-size: 16px;
            line-height: 1.8;
            position: relative;
            z-index: 1;
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
            backdrop-filter: blur(5px);
            z-index: 2000;
            align-items: center;
            justify-content: center;
            animation: fadeIn 0.3s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .export-modal-content {
            background-color: white;
            border-radius: var(--radius);
            width: 90%;
            max-width: 600px;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
            animation: modalSlideIn 0.4s ease;
            overflow: hidden;
        }

        @keyframes modalSlideIn {
            from { opacity: 0; transform: translateY(-30px) scale(0.95); }
            to { opacity: 1; transform: translateY(0) scale(1); }
        }

        .export-modal-header {
            background: linear-gradient(135deg, var(--primary-color) 0%, var(--primary-dark) 100%);
            color: white;
            padding: 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .export-modal-title {
            font-size: 22px;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .export-modal-close {
            background: rgba(255, 255, 255, 0.2);
            border: none;
            color: white;
            font-size: 28px;
            cursor: pointer;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: var(--transition);
        }

        .export-modal-close:hover {
            background: rgba(255, 255, 255, 0.3);
            transform: rotate(90deg);
        }

        .export-modal-body {
            padding: 40px;
        }

        .export-options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 25px;
            margin: 30px 0;
        }

        .export-option {
            border: 2px solid var(--border-color);
            border-radius: var(--radius);
            padding: 30px 20px;
            text-align: center;
            cursor: pointer;
            transition: var(--transition);
            position: relative;
            overflow: hidden;
        }

        .export-option::before {
            content: '';
            position: absolute;
            top: 0;
            right: 0;
            width: 100%;
            height: 5px;
            background: linear-gradient(90deg, var(--primary-color) 0%, var(--primary-light) 100%);
            transform: translateY(-100%);
            transition: var(--transition);
        }

        .export-option:hover::before {
            transform: translateY(0);
        }

        .export-option:hover {
            border-color: var(--primary-color);
            transform: translateY(-10px);
            box-shadow: var(--shadow-lg);
        }

        .export-option i {
            font-size: 48px;
            margin-bottom: 20px;
            color: var(--primary-color);
            transition: var(--transition);
        }

        .export-option:hover i {
            transform: scale(1.1);
        }

        .export-option-title {
            font-size: 20px;
            font-weight: 700;
            margin-bottom: 12px;
            color: var(--dark-color);
            transition: var(--transition);
        }

        .export-option:hover .export-option-title {
            color: var(--primary-color);
        }

        .export-option-desc {
            font-size: 15px;
            color: var(--gray-color);
            line-height: 1.6;
        }

        .export-actions {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 40px;
        }

        /* Scroll Indicator */
        .scroll-indicator {
            position: fixed;
            bottom: 40px;
            left: 40px;
            background: linear-gradient(135deg, var(--primary-color) 0%, var(--primary-light) 100%);
            color: white;
            width: 55px;
            height: 55px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 22px;
            cursor: pointer;
            box-shadow: 0 6px 20px rgba(44, 90, 160, 0.3);
            transition: var(--transition);
            z-index: 100;
            opacity: 0;
            transform: translateY(20px);
        }

        .scroll-indicator.visible {
            opacity: 1;
            transform: translateY(0);
        }

        .scroll-indicator:hover {
            background: var(--primary-dark);
            transform: translateY(-5px) scale(1.05);
        }

        /* Success Message */
        .success-message {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) scale(0.9);
            background: white;
            padding: 40px;
            border-radius: var(--radius);
            box-shadow: 0 15px 40px rgba(0,0,0,0.2);
            text-align: center;
            z-index: 3000;
            opacity: 0;
            visibility: hidden;
            transition: var(--transition);
            max-width: 500px;
            width: 90%;
        }

        .success-message.active {
            opacity: 1;
            visibility: visible;
            transform: translate(-50%, -50%) scale(1);
        }

        .success-icon {
            font-size: 70px;
            color: var(--success-color);
            margin-bottom: 25px;
            animation: bounce 1s ease;
        }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% {transform: translateY(0);}
            40% {transform: translateY(-20px);}
            60% {transform: translateY(-10px);}
        }

        .success-title {
            font-size: 26px;
            color: var(--primary-color);
            margin-bottom: 15px;
            font-weight: 700;
        }

        .success-details {
            color: var(--gray-color);
            font-size: 16px;
            margin-bottom: 25px;
            line-height: 1.8;
        }

        /* Loading Overlay */
        .loading-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(255, 255, 255, 0.9);
            backdrop-filter: blur(5px);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 4000;
            flex-direction: column;
            gap: 25px;
        }

        .loading-overlay.active {
            display: flex;
            animation: fadeIn 0.3s ease;
        }

        .loading-spinner {
            width: 60px;
            height: 60px;
            border: 5px solid var(--border-color);
            border-top: 5px solid var(--primary-color);
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .loading-text {
            font-size: 18px;
            color: var(--primary-color);
            font-weight: 600;
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
                padding: 30px;
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
                width: 50px;
                height: 50px;
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
                padding: 20px;
            }
            
            .section-header {
                font-size: 18px;
            }
            
            .form-input, .form-select, .form-textarea {
                padding: 14px;
                font-size: 15px;
            }
            
            .export-modal-content {
                width: 95%;
                margin: 10px;
            }
            
            .success-message {
                padding: 30px 20px;
            }
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 12px;
        }

        ::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 10px;
        }

        ::-webkit-scrollbar-thumb {
            background: linear-gradient(135deg, var(--primary-color) 0%, var(--primary-light) 100%);
            border-radius: 10px;
            border: 3px solid #f1f1f1;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: var(--primary-dark);
        }

        /* Form Validation Styles */
        .form-input.invalid, .form-select.invalid, .form-textarea.invalid {
            border-color: var(--danger-color);
            background-color: rgba(220, 53, 69, 0.05);
        }

        .validation-error {
            color: var(--danger-color);
            font-size: 14px;
            margin-top: 5px;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .validation-error i {
            font-size: 16px;
        }
    </style>
</head>
<body>
    <!-- Loading Overlay -->
    <div class="loading-overlay" id="loadingOverlay">
        <div class="loading-spinner"></div>
        <div class="loading-text" id="loadingText">جاري معالجة البيانات...</div>
    </div>

    <!-- Success Message -->
    <div class="success-message" id="successMessage">
        <div class="success-icon">
            <i class="fas fa-check-circle"></i>
        </div>
        <h3 class="success-title" id="successTitle">تم إنشاء التقرير بنجاح!</h3>
        <p class="success-details" id="successDetails">جاري تحميل الملف...</p>
        <button class="btn btn-success" id="closeSuccessMessage">
            <i class="fas fa-check"></i> موافق
        </button>
    </div>

    <!-- Header -->
    <div class="header">
        <h1>نظام إعداد التقارير - أداء الواجبات الوظيفية</h1>
        <div class="header-subtitle">الإدارة العامة للتعليم بمنطقة الرياض</div>
    </div>

    <!-- Main Content -->
    <div class="main-container">
        <!-- Instruction Box -->
        <div class="instruction-box">
            <h3><i class="fas fa-info-circle"></i> تعليمات إعداد التقرير</h3>
            <p>يرجى تعبئة جميع الحقول المطلوبة (*) بدقة لتتمكن من إنشاء التقرير بشكل صحيح. يمكنك حفظ العمل كمسودة والعودة إليه لاحقاً.</p>
        </div>

        <!-- Report Form -->
        <div class="report-form-container">
            <!-- Section 1: Report Type -->
            <div class="form-section">
                <h2 class="section-header"><i class="fas fa-file-signature"></i> اختيار نوع التقرير</h2>
                <p class="section-subtitle">اختر نوع التقرير المناسب لهذا البند من القائمة التالية</p>
                
                <div class="form-group">
                    <label class="form-label required"><i class="fas fa-tasks"></i> أداء الواجبات الوظيفية (البند رقم 1)</label>
                    <select class="form-select" id="reportType">
                        <option value="">اختر نوع التقرير...</option>
                        <option value="strategy" selected>تقرير تنفيذ استراتيجية</option>
                        <option value="activity-session">تقرير حصة النشاط</option>
                        <option value="class-activities">تقرير أنشطة داخل الفصل</option>
                        <option value="remedial">تقرير نشاط إلزائي</option>
                        <option value="visits">تقرير تبادل الزيارات</option>
                    </select>
                    <div id="reportTypeError" class="validation-error" style="display: none;">
                        <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                    </div>
                </div>
            </div>

            <!-- Section 2: Main Data -->
            <div class="form-section">
                <h2 class="section-header"><i class="fas fa-database"></i> البيانات الرئيسية</h2>
                <p class="section-subtitle">البيانات الرئيسية التي ستظهر في رأس التقرير النهائي</p>
                
                <div class="form-row">
                    <div class="form-group">
                        <label class="form-label required"><i class="fas fa-map-marker-alt"></i> اسم المنطقة</label>
                        <input type="text" class="form-input" id="region" placeholder="مثال: الرياض" value="الرياض">
                        <div class="form-example">مثال: الرياض، مكة المكرمة، المدينة المنورة</div>
                        <div id="regionError" class="validation-error" style="display: none;">
                            <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label required"><i class="fas fa-school"></i> اسم المدرسة</label>
                        <input type="text" class="form-input" id="school" placeholder="اسم المدرسة" value="مدرسة النموذجية الثانوية">
                        <div id="schoolError" class="validation-error" style="display: none;">
                            <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                        </div>
                    </div>
                </div>
                
                <div class="form-row">
                    <div class="form-group">
                        <label class="form-label required"><i class="fas fa-user-tie"></i> مدير المدرسة</label>
                        <input type="text" class="form-input" id="principal" placeholder="مدير المدرسة" value="أ. علي محمد أحمد">
                        <div class="form-example">مثال: أ. علي محمد أحمد، د. محمد بن عبدالله</div>
                        <div id="principalError" class="validation-error" style="display: none;">
                            <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label required"><i class="fas fa-user-edit"></i> معد التقرير</label>
                        <input type="text" class="form-input" id="reporter" placeholder="معد التقرير" value="أ. أحمد عبدالله السعيد">
                        <div class="form-example">مثال: أ. أحمد عبدالله السعيد، م. خالد محمد</div>
                        <div id="reporterError" class="validation-error" style="display: none;">
                            <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                        </div>
                    </div>
                </div>
                
                <div class="form-group">
                    <label class="form-label required"><i class="fas fa-heading"></i> عنوان التقرير</label>
                    <input type="text" class="form-input" id="reportTitle" placeholder="عنوان التقرير" value="تقرير تنفيذ استراتيجية">
                    <div id="reportTitleError" class="validation-error" style="display: none;">
                        <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                    </div>
                </div>
                
                <div class="form-group">
                    <label class="form-label required"><i class="fas fa-book"></i> تابع للمناهج (نعم/لا)</label>
                    <select class="form-select" id="curriculumRelated">
                        <option value="نعم" selected>نعم</option>
                        <option value="لا">لا</option>
                    </select>
                    <div id="curriculumRelatedError" class="validation-error" style="display: none;">
                        <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                    </div>
                </div>
            </div>

            <!-- Section 3: Program Details -->
            <div class="form-section">
                <h2 class="section-header"><i class="fas fa-calendar-alt"></i> تفاصيل البرنامج</h2>
                <p class="section-subtitle">التفاصيل الزمنية والمكانية للبرنامج المنفذ</p>
                
                <div class="form-row">
                    <div class="form-group">
                        <label class="form-label required"><i class="fas fa-calendar"></i> تاريخ البرنامج (هجري)</label>
                        <input type="text" class="form-input" id="programDate" placeholder="1447-06-12" value="1447-06-12">
                        <div class="form-example">التاريخ الهجري بالصيغة: 1447-06-12</div>
                        <div id="programDateError" class="validation-error" style="display: none;">
                            <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label required"><i class="fas fa-map-marker"></i> مكان التنفيذ</label>
                        <input type="text" class="form-input" id="location" placeholder="مثال: قاعة مصادر التعلم" value="قاعة مصادر التعلم">
                        <div class="form-example">مثال: قاعة مصادر التعلم، الفصل الدراسي، الساحة المدرسية</div>
                        <div id="locationError" class="validation-error" style="display: none;">
                            <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                        </div>
                    </div>
                </div>
                
                <div class="form-row">
                    <div class="form-group">
                        <label class="form-label required"><i class="fas fa-users"></i> المستهدفون</label>
                        <input type="text" class="form-input" id="target" placeholder="مثال: طلاب الصف الثالث ثانوي" value="طلاب الصف الثالث ثانوي">
                        <div class="form-example">مثال: طلاب الصف الثالث ثانوي، معلمو المرحلة الابتدائية</div>
                        <div id="targetError" class="validation-error" style="display: none;">
                            <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label required"><i class="fas fa-user-check"></i> عدد المستفيدين</label>
                        <input type="number" class="form-input" id="beneficiaries" placeholder="مثال: 25 طالباً" value="25" min="1">
                        <div class="form-example">أدخل عدد المستفيدين من البرنامج (رقم فقط)</div>
                        <div id="beneficiariesError" class="validation-error" style="display: none;">
                            <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                        </div>
                    </div>
                </div>
            </div>

            <!-- Section 4: Activity Description -->
            <div class="form-section">
                <h2 class="section-header"><i class="fas fa-align-left"></i> وصف النشاط</h2>
                <p class="section-subtitle">وصف شامل وواضح للنشاط الذي تم تنفيذه</p>
                
                <div class="form-group">
                    <label class="form-label required"><i class="fas fa-clipboard-list"></i> وصف مختصر لما تم تنفيذه</label>
                    <textarea class="form-textarea" id="description" placeholder="وصف مختصر لما تم تنفيذه في النشاط">تم تنفيذ استراتيجية التدريس وفق الخطة المعتمدة، مع توزيع الطلاب على مجموعات عمل تعاونية وتنويع الأنشطة بما يناسب ميولهم واحتياجاتهم. تم تطبيق استراتيجية التعلم النشط من خلال أنشطة عملية وتفاعلية.</textarea>
                    <div class="form-example">يجب أن يتضمن الوصف ملخصاً واضحاً وشاملاً للنشاط المنفذ</div>
                    <div id="descriptionError" class="validation-error" style="display: none;">
                        <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                    </div>
                </div>
            </div>

            <!-- Section 5: Implementation Procedures -->
            <div class="form-section">
                <h2 class="section-header"><i class="fas fa-tasks"></i> إجراءات التنفيذ</h2>
                <p class="section-subtitle">الخطوات والإجراءات التي تم اتباعها لتنفيذ النشاط</p>
                
                <div class="form-group">
                    <label class="form-label required"><i class="fas fa-list-ol"></i> إجراءات التنفيذ (افصل بين النقاط بفاصلة)</label>
                    <textarea class="form-textarea" id="procedures" placeholder="أدخل إجراءات التنفيذ">إعداد خطة حصة النشاط وتحديد الأهداف والأنشطة المناسبة, توزيع الطلاب إلى مجموعات عمل وتوضيح المهام لكل مجموعة, توفير المواد والأدوات اللازمة للنشاط, متابعة تنفيذ الطلاب للنشاط وتقديم التوجيه اللازم, تقييم مخرجات النشاط من قبل الطلاب والمعلم</textarea>
                    <div class="form-example">أدخل كل إجراء في سطر جديد أو افصل بين النقاط بفاصلة (,) كل إجراء يجب أن يكون جملة كاملة</div>
                    <div id="proceduresError" class="validation-error" style="display: none;">
                        <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                    </div>
                </div>
            </div>

            <!-- Section 6: Results -->
            <div class="form-section">
                <h2 class="section-header"><i class="fas fa-chart-line"></i> النتائج</h2>
                <p class="section-subtitle">النتائج المتحققة والأثر الإيجابي للنشاط</p>
                
                <div class="form-group">
                    <label class="form-label required"><i class="fas fa-chart-bar"></i> النتائج (افصل بين النقاط بفاصلة)</label>
                    <textarea class="form-textarea" id="results" placeholder="أدخل النتائج المتحققة">تفاعل إيجابي من الطلاب أثناء تنفيذ استراتيجية التدريس, تنمية روح التعاون والعمل الجماعي بين الطلاب, اكتشاف مواهب الطلاب في مجالات متنوعة, تطبيق المعرفة النظرية في أنشطة عملية, زيادة دافعية الطلاب للتعلم والمشاركة</textarea>
                    <div class="form-example">اذكر النتائج الإيجابية التي تحققت من تنفيذ النشاط بشكل واضح ومفصل</div>
                    <div id="resultsError" class="validation-error" style="display: none;">
                        <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                    </div>
                </div>
            </div>

            <!-- Section 7: Recommendations -->
            <div class="form-section">
                <h2 class="section-header"><i class="fas fa-lightbulb"></i> التوصيات</h2>
                <p class="section-subtitle">توصيات للتحسين والتطوير في المستقبل</p>
                
                <div class="form-group">
                    <label class="form-label required"><i class="fas fa-comments"></i> التوصيات</label>
                    <textarea class="form-textarea" id="recommendations" placeholder="أدخل التوصيات">الاستمرار في تنويع استراتيجيات التدريس وتوثيق الممارسات المميزة لإثراء التجارب المستقبلية. توفير المزيد من الموارد والأدوات اللازمة للأنشطة العملية. تشجيع الطلاب المبدعين للمشاركة في المسابقات والمنافسات الخارجية. عقد ورش عمل للمعلمين لتبادل الخبرات في مجال استراتيجيات التدريس الحديثة.</textarea>
                    <div class="form-example">قدم توصيات واضحة وعملية للتحسين والتطوير في المستقبل</div>
                    <div id="recommendationsError" class="validation-error" style="display: none;">
                        <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                    </div>
                </div>
            </div>

            <!-- Section 8: Attachments -->
            <div class="form-section upload-section">
                <h2 class="section-header"><i class="fas fa-images"></i> الصور المرفقة بالتقرير</h2>
                <p class="section-subtitle">صور توثيقية للنشاط المنفذ (صورتان كحد أقصى)</p>
                
                <div class="upload-area" id="uploadArea">
                    <div class="upload-icon">
                        <i class="fas fa-cloud-upload-alt"></i>
                    </div>
                    <div class="upload-text">انقر لرفع الصور أو اسحبها إلى هنا</div>
                    <div class="upload-hint">الحجم الأقصى: 5MB لكل صورة | الصيغ المدعومة: JPG, PNG, GIF | الحد الأقصى: صورتان</div>
                    <input type="file" id="imageUpload" accept="image/*" multiple style="display: none;">
                </div>
                
                <div class="image-preview" id="imagePreview"></div>
                
                <div class="form-group" style="margin-top: 20px;">
                    <label class="form-label"><i class="fas fa-tips"></i> نصائح للصور المرفقة:</label>
                    <ul style="padding-right: 20px; color: var(--gray-color); font-size: 14px; line-height: 1.8;">
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
                
                <div style="display: flex; gap: 20px; flex-wrap: wrap;">
                    <button class="btn btn-outline" id="previewReport">
                        <i class="fas fa-eye"></i> معاينة التقرير
                    </button>
                    <button class="btn btn-success" id="submitReport">
                        <i class="fas fa-check-circle"></i> إنشاء التقرير النهائي
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
                    <i class="fas fa-download"></i> تصدير التقرير النهائي
                </div>
                <button class="export-modal-close" id="closeExportModal">&times;</button>
            </div>
            <div class="export-modal-body">
                <p style="text-align: center; margin-bottom: 20px; color: var(--gray-color); font-size: 16px; line-height: 1.6;">
                    اختر الصيغة المناسبة لتصدير التقرير النهائي. ستظهر رسالة تأكيد عند اكتمال التصدير.
                </p>
                
                <div class="export-options">
                    <div class="export-option" data-format="word">
                        <i class="fas fa-file-word"></i>
                        <div class="export-option-title">Microsoft Word</div>
                        <div class="export-option-desc">نسق احترافي قابلة للتعديل والطباعة مع تنسيق متقدم</div>
                    </div>
                    
                    <div class="export-option" data-format="html">
                        <i class="fas fa-file-code"></i>
                        <div class="export-option-title">الصفحة كاملة</div>
                        <div class="export-option-desc">نسخة ويب تفاعلية مع تنسيق احترافي متكامل</div>
                    </div>
                </div>
                
                <div class="export-actions">
                    <button class="btn btn-outline" id="cancelExport">
                        <i class="fas fa-times"></i> إلغاء
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Scroll to Top Button -->
    <div class="scroll-indicator" id="scrollToTop">
        <i class="fas fa-arrow-up"></i>
    </div>

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
            const loadingOverlay = document.getElementById('loadingOverlay');
            const loadingText = document.getElementById('loadingText');
            const successMessage = document.getElementById('successMessage');
            const successTitle = document.getElementById('successTitle');
            const successDetails = document.getElementById('successDetails');
            const closeSuccessMessage = document.getElementById('closeSuccessMessage');
            
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
                        scrollToTopBtn.classList.add('visible');
                    } else {
                        scrollToTopBtn.classList.remove('visible');
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
                            this.classList.remove('invalid');
                            const errorDiv = document.getElementById(`${this.id}Error`);
                            if (errorDiv) errorDiv.style.display = 'none';
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
                
                // إغلاق رسالة النجاح
                closeSuccessMessage.addEventListener('click', function() {
                    successMessage.classList.remove('active');
                });
            }
            
            // ========== معالجة رفع الصور ==========
            function handleImageUpload(files) {
                // التحقق من عدد الصور
                if (uploadedImages.length + files.length > 2) {
                    showError('يمكنك رفع صورتين كحد أقصى فقط');
                    return;
                }
                
                for (let i = 0; i < files.length; i++) {
                    const file = files[i];
                    
                    // التحقق من نوع الملف
                    if (!file.type.startsWith('image/')) {
                        showError('الرجاء رفع ملفات صور فقط (JPG, PNG, GIF)');
                        continue;
                    }
                    
                    // التحقق من حجم الملف (5MB)
                    if (file.size > 5 * 1024 * 1024) {
                        showError('حجم الصورة يجب أن يكون أقل من 5MB');
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
                
                showSuccess('تم تحميل بيانات المسودة بنجاح');
            }
            
            // ========== التحقق من الحقول ==========
            function validateField(field) {
                const errorDiv = document.getElementById(`${field.id}Error`);
                
                if (field.hasAttribute('required') && !field.value.trim()) {
                    field.classList.add('invalid');
                    if (errorDiv) errorDiv.style.display = 'flex';
                    return false;
                }
                
                field.classList.remove('invalid');
                if (errorDiv) errorDiv.style.display = 'none';
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
                    showError('يرجى ملء جميع الحقول المطلوبة قبل الحفظ');
                    return;
                }
                
                const reportData = collectReportData();
                reportData.status = 'draft';
                reportData.savedAt = new Date().toLocaleString('ar-SA');
                
                // حفظ البيانات
                localStorage.setItem('reportDraft', JSON.stringify(reportData));
                
                showSuccess('تم حفظ التقرير كمسودة بنجاح!\n' + reportData.savedAt);
            }
            
            // ========== معاينة التقرير ==========
            function previewReport() {
                if (!validateForm()) {
                    showError('يرجى ملء جميع الحقول المطلوبة قبل المعاينة');
                    return;
                }
                
                currentReportData = collectReportData();
                currentReportData.reportNumber = generateReportNumber();
                
                // فتح نافذة جديدة للمعاينة
                const previewWindow = window.open('', '_blank');
                previewWindow.document.write(generatePreviewHTML(currentReportData));
                previewWindow.document.close();
            }
            
            // ========== إنشاء التقرير النهائي ==========
            function submitReport() {
                if (!validateForm()) {
                    showError('يرجى ملء جميع الحقول المطلوبة قبل الإنشاء');
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
                    showError('لا توجد بيانات للتقرير');
                    return;
                }
                
                exportModal.style.display = 'none';
                showLoading(`جاري تحضير التقرير بصيغة ${format === 'word' ? 'Word' : 'HTML'}...`);
                
                try {
                    switch(format) {
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
                    hideLoading();
                    showExportSuccess(format);
                    
                } catch (error) {
                    hideLoading();
                    showError(`حدث خطأ أثناء التصدير: ${error.message}`);
                }
            }
            
            // ========== تصدير إلى Word (تنسيق احترافي) ==========
            async function exportToWord() {
                const docx = window.docx;
                
                // إنشاء محتوى الوثيقة بتنسيق احترافي
                const doc = new docx.Document({
                    sections: [{
                        properties: {
                            page: {
                                margin: {
                                    top: 1440,    // 1 inch = 1440 twips
                                    right: 1440,
                                    bottom: 1440,
                                    left: 1440
                                },
                                pageNumbers: {
                                    start: 1,
                                    formatType: docx.PageNumberFormat.DECIMAL
                                }
                            }
                        },
                        children: [
                            // عنوان الصفحة مع ترويسة
                            new docx.Paragraph({
                                children: [
                                    new docx.TextRun({
                                        text: "الإدارة العامة للتعليم",
                                        bold: true,
                                        size: 32,
                                        font: "Traditional Arabic"
                                    })
                                ],
                                alignment: docx.AlignmentType.CENTER,
                                spacing: {
                                    after: 400
                                }
                            }),
                            
                            new docx.Paragraph({
                                children: [
                                    new docx.TextRun({
                                        text: `بمنطقة ${currentReportData.region}`,
                                        bold: true,
                                        size: 28,
                                        font: "Traditional Arabic"
                                    })
                                ],
                                alignment: docx.AlignmentType.CENTER,
                                spacing: {
                                    after: 600
                                }
                            }),
                            
                            // العنوان الرئيسي
                            new docx.Paragraph({
                                children: [
                                    new docx.TextRun({
                                        text: currentReportData.title,
                                        bold: true,
                                        size: 36,
                                        font: "Traditional Arabic",
                                        color: "2c5aa0"
                                    })
                                ],
                                alignment: docx.AlignmentType.CENTER,
                                border: {
                                    bottom: {
                                        color: "2c5aa0",
                                        size: 8,
                                        space: 1,
                                        style: docx.BorderStyle.SINGLE
                                    }
                                },
                                spacing: {
                                    after: 600
                                }
                            }),
                            
                            // معلومات التقرير
                            new docx.Paragraph({
                                children: [
                                    new docx.TextRun({
                                        text: `رقم التقرير: ${currentReportData.reportNumber}`,
                                        size: 22,
                                        font: "Traditional Arabic"
                                    })
                                ],
                                alignment: docx.AlignmentType.RIGHT,
                                spacing: {
                                    after: 200
                                }
                            }),
                            
                            new docx.Paragraph({
                                children: [
                                    new docx.TextRun({
                                        text: `تاريخ البرنامج: ${currentReportData.programDate}`,
                                        size: 22,
                                        font: "Traditional Arabic"
                                    })
                                ],
                                alignment: docx.AlignmentType.RIGHT,
                                spacing: {
                                    after: 400
                                }
                            }),
                            
                            // القسم الأول: البيانات الأساسية
                            new docx.Paragraph({
                                children: [
                                    new docx.TextRun({
                                        text: "البيانات الأساسية",
                                        bold: true,
                                        size: 28,
                                        font: "Traditional Arabic",
                                        color: "2c5aa0"
                                    })
                                ],
                                alignment: docx.AlignmentType.RIGHT,
                                spacing: {
                                    before: 400,
                                    after: 300
                                }
                            }),
                            
                            // جدول البيانات الأساسية
                            new docx.Table({
                                rows: [
                                    new docx.TableRow({
                                        children: [
                                            new docx.TableCell({
                                                children: [new docx.Paragraph({
                                                    children: [new docx.TextRun({
                                                        text: "المدرسة:",
                                                        bold: true,
                                                        size: 24,
                                                        font: "Traditional Arabic"
                                                    })]
                                                })],
                                                shading: {
                                                    fill: "f0f4f8"
                                                },
                                                width: {
                                                    size: 30,
                                                    type: docx.WidthType.PERCENTAGE
                                                }
                                            }),
                                            new docx.TableCell({
                                                children: [new docx.Paragraph({
                                                    children: [new docx.TextRun({
                                                        text: currentReportData.school,
                                                        size: 24,
                                                        font: "Traditional Arabic"
                                                    })]
                                                })],
                                                width: {
                                                    size: 70,
                                                    type: docx.WidthType.PERCENTAGE
                                                }
                                            })
                                        ]
                                    }),
                                    new docx.TableRow({
                                        children: [
                                            new docx.TableCell({
                                                children: [new docx.Paragraph({
                                                    children: [new docx.TextRun({
                                                        text: "مدير المدرسة:",
                                                        bold: true,
                                                        size: 24,
                                                        font: "Traditional Arabic"
                                                    })]
                                                })],
                                                shading: {
                                                    fill: "f0f4f8"
                                                }
                                            }),
                                            new docx.TableCell({
                                                children: [new docx.Paragraph({
                                                    children: [new docx.TextRun({
                                                        text: currentReportData.principal,
                                                        size: 24,
                                                        font: "Traditional Arabic"
                                                    })]
                                                })]
                                            })
                                        ]
                                    }),
                                    new docx.TableRow({
                                        children: [
                                            new docx.TableCell({
                                                children: [new docx.Paragraph({
                                                    children: [new docx.TextRun({
                                                        text: "معد التقرير:",
                                                        bold: true,
                                                        size: 24,
                                                        font: "Traditional Arabic"
                                                    })]
                                                })],
                                                shading: {
                                                    fill: "f0f4f8"
                                                }
                                            }),
                                            new docx.TableCell({
                                                children: [new docx.Paragraph({
                                                    children: [new docx.TextRun({
                                                        text: currentReportData.reporter,
                                                        size: 24,
                                                        font: "Traditional Arabic"
                                                    })]
                                                })]
                                            })
                                        ]
                                    }),
                                    new docx.TableRow({
                                        children: [
                                            new docx.TableCell({
                                                children: [new docx.Paragraph({
                                                    children: [new docx.TextRun({
                                                        text: "مكان التنفيذ:",
                                                        bold: true,
                                                        size: 24,
                                                        font: "Traditional Arabic"
                                                    })]
                                                })],
                                                shading: {
                                                    fill: "f0f4f8"
                                                }
                                            }),
                                            new docx.TableCell({
                                                children: [new docx.Paragraph({
                                                    children: [new docx.TextRun({
                                                        text: currentReportData.location,
                                                        size: 24,
                                                        font: "Traditional Arabic"
                                                    })]
                                                })]
                                            })
                                        ]
                                    }),
                                    new docx.TableRow({
                                        children: [
                                            new docx.TableCell({
                                                children: [new docx.Paragraph({
                                                    children: [new docx.TextRun({
                                                        text: "المستهدفون:",
                                                        bold: true,
                                                        size: 24,
                                                        font: "Traditional Arabic"
                                                    })]
                                                })],
                                                shading: {
                                                    fill: "f0f4f8"
                                                }
                                            }),
                                            new docx.TableCell({
                                                children: [new docx.Paragraph({
                                                    children: [new docx.TextRun({
                                                        text: currentReportData.target,
                                                        size: 24,
                                                        font: "Traditional Arabic"
                                                    })]
                                                })]
                                            })
                                        ]
                                    }),
                                    new docx.TableRow({
                                        children: [
                                            new docx.TableCell({
                                                children: [new docx.Paragraph({
                                                    children: [new docx.TextRun({
                                                        text: "عدد المستفيدين:",
                                                        bold: true,
                                                        size: 24,
                                                        font: "Traditional Arabic"
                                                    })]
                                                })],
                                                shading: {
                                                    fill: "f0f4f8"
                                                }
                                            }),
                                            new docx.TableCell({
                                                children: [new docx.Paragraph({
                                                    children: [new docx.TextRun({
                                                        text: currentReportData.beneficiaries,
                                                        size: 24,
                                                        font: "Traditional Arabic"
                                                    })]
                                                })]
                                            })
                                        ]
                                    }),
                                    new docx.TableRow({
                                        children: [
                                            new docx.TableCell({
                                                children: [new docx.Paragraph({
                                                    children: [new docx.TextRun({
                                                        text: "تابع للمناهج:",
                                                        bold: true,
                                                        size: 24,
                                                        font: "Traditional Arabic"
                                                    })]
                                                })],
                                                shading: {
                                                    fill: "f0f4f8"
                                                }
                                            }),
                                            new docx.TableCell({
                                                children: [new docx.Paragraph({
                                                    children: [new docx.TextRun({
                                                        text: currentReportData.curriculumRelated,
                                                        size: 24,
                                                        font: "Traditional Arabic"
                                                    })]
                                                })]
                                            })
                                        ]
                                    })
                                ],
                                width: {
                                    size: 100,
                                    type: docx.WidthType.PERCENTAGE
                                },
                                borders: {
                                    insideHorizontal: {
                                        style: docx.BorderStyle.SINGLE,
                                        size: 1,
                                        color: "CCCCCC"
                                    },
                                    insideVertical: {
                                        style: docx.BorderStyle.SINGLE,
                                        size: 1,
                                        color: "CCCCCC"
                                    }
                                }
                            }),
                            
                            // القسم الثاني: وصف النشاط
                            new docx.Paragraph({
                                children: [
                                    new docx.TextRun({
                                        text: "وصف مختصر لما تم تنفيذه",
                                        bold: true,
                                        size: 28,
                                        font: "Traditional Arabic",
                                        color: "2c5aa0"
                                    })
                                ],
                                alignment: docx.AlignmentType.RIGHT,
                                spacing: {
                                    before: 600,
                                    after: 300
                                }
                            }),
                            
                            new docx.Paragraph({
                                children: [
                                    new docx.TextRun({
                                        text: currentReportData.description,
                                        size: 24,
                                        font: "Traditional Arabic"
                                    })
                                ],
                                alignment: docx.AlignmentType.RIGHT,
                                spacing: {
                                    after: 400
                                }
                            }),
                            
                            // القسم الثالث: إجراءات التنفيذ
                            new docx.Paragraph({
                                children: [
                                    new docx.TextRun({
                                        text: "إجراءات التنفيذ",
                                        bold: true,
                                        size: 28,
                                        font: "Traditional Arabic",
                                        color: "2c5aa0"
                                    })
                                ],
                                alignment: docx.AlignmentType.RIGHT,
                                spacing: {
                                    before: 400,
                                    after: 300
                                }
                            }),
                            
                            ...(currentReportData.procedures || []).map((procedure, index) => 
                                new docx.Paragraph({
                                    children: [
                                        new docx.TextRun({
                                            text: `${index + 1}. ${procedure}`,
                                            size: 24,
                                            font: "Traditional Arabic"
                                        })
                                    ],
                                    alignment: docx.AlignmentType.RIGHT,
                                    spacing: {
                                        after: 150
                                    },
                                    bullet: {
                                        level: 0
                                    }
                                })
                            ),
                            
                            // القسم الرابع: النتائج
                            new docx.Paragraph({
                                children: [
                                    new docx.TextRun({
                                        text: "النتائج",
                                        bold: true,
                                        size: 28,
                                        font: "Traditional Arabic",
                                        color: "2c5aa0"
                                    })
                                ],
                                alignment: docx.AlignmentType.RIGHT,
                                spacing: {
                                    before: 600,
                                    after: 300
                                }
                            }),
                            
                            ...(currentReportData.results || []).map((result, index) => 
                                new docx.Paragraph({
                                    children: [
                                        new docx.TextRun({
                                            text: `${index + 1}. ${result}`,
                                            size: 24,
                                            font: "Traditional Arabic"
                                        })
                                    ],
                                    alignment: docx.AlignmentType.RIGHT,
                                    spacing: {
                                        after: 150
                                    },
                                    bullet: {
                                        level: 0
                                    }
                                })
                            ),
                            
                            // القسم الخامس: التوصيات
                            new docx.Paragraph({
                                children: [
                                    new docx.TextRun({
                                        text: "التوصيات",
                                        bold: true,
                                        size: 28,
                                        font: "Traditional Arabic",
                                        color: "2c5aa0"
                                    })
                                ],
                                alignment: docx.AlignmentType.RIGHT,
                                spacing: {
                                    before: 600,
                                    after: 300
                                }
                            }),
                            
                            new docx.Paragraph({
                                children: [
                                    new docx.TextRun({
                                        text: currentReportData.recommendations,
                                        size: 24,
                                        font: "Traditional Arabic"
                                    })
                                ],
                                alignment: docx.AlignmentType.RIGHT,
                                spacing: {
                                    after: 600
                                }
                            }),
                            
                            // التوقيعات
                            new docx.Paragraph({
                                children: [
                                    new docx.TextRun({
                                        text: "التوقيعات",
                                        bold: true,
                                        size: 28,
                                        font: "Traditional Arabic",
                                        color: "2c5aa0"
                                    })
                                ],
                                alignment: docx.AlignmentType.CENTER,
                                spacing: {
                                    before: 800,
                                    after: 400
                                }
                            }),
                            
                            new docx.Table({
                                rows: [
                                    new docx.TableRow({
                                        children: [
                                            new docx.TableCell({
                                                children: [
                                                    new docx.Paragraph({
                                                        children: [
                                                            new docx.TextRun({
                                                                text: "مدير المدرسة",
                                                                bold: true,
                                                                size: 24,
                                                                font: "Traditional Arabic"
                                                            })
                                                        ],
                                                        alignment: docx.AlignmentType.CENTER
                                                    }),
                                                    new docx.Paragraph({
                                                        children: [
                                                            new docx.TextRun({
                                                                text: currentReportData.principal,
                                                                size: 22,
                                                                font: "Traditional Arabic"
                                                            })
                                                        ],
                                                        alignment: docx.AlignmentType.CENTER
                                                    }),
                                                    new docx.Paragraph({
                                                        children: [
                                                            new docx.TextRun({
                                                                text: "________________________",
                                                                size: 24,
                                                                font: "Traditional Arabic"
                                                            })
                                                        ],
                                                        alignment: docx.AlignmentType.CENTER
                                                    }),
                                                    new docx.Paragraph({
                                                        children: [
                                                            new docx.TextRun({
                                                                text: "التوقيع",
                                                                size: 20,
                                                                font: "Traditional Arabic",
                                                                color: "666666"
                                                            })
                                                        ],
                                                        alignment: docx.AlignmentType.CENTER
                                                    })
                                                ],
                                                margins: {
                                                    top: 200,
                                                    bottom: 200
                                                }
                                            }),
                                            new docx.TableCell({
                                                children: [
                                                    new docx.Paragraph({
                                                        children: [
                                                            new docx.TextRun({
                                                                text: "معد التقرير",
                                                                bold: true,
                                                                size: 24,
                                                                font: "Traditional Arabic"
                                                            })
                                                        ],
                                                        alignment: docx.AlignmentType.CENTER
                                                    }),
                                                    new docx.Paragraph({
                                                        children: [
                                                            new docx.TextRun({
                                                                text: currentReportData.reporter,
                                                                size: 22,
                                                                font: "Traditional Arabic"
                                                            })
                                                        ],
                                                        alignment: docx.AlignmentType.CENTER
                                                    }),
                                                    new docx.Paragraph({
                                                        children: [
                                                            new docx.TextRun({
                                                                text: "________________________",
                                                                size: 24,
                                                                font: "Traditional Arabic"
                                                            })
                                                        ],
                                                        alignment: docx.AlignmentType.CENTER
                                                    }),
                                                    new docx.Paragraph({
                                                        children: [
                                                            new docx.TextRun({
                                                                text: "التوقيع",
                                                                size: 20,
                                                                font: "Traditional Arabic",
                                                                color: "666666"
                                                            })
                                                        ],
                                                        alignment: docx.AlignmentType.CENTER
                                                    })
                                                ],
                                                margins: {
                                                    top: 200,
                                                    bottom: 200
                                                }
                                            })
                                        ]
                                    })
                                ],
                                width: {
                                    size: 100,
                                    type: docx.WidthType.PERCENTAGE
                                }
                            }),
                            
                            // تذييل الصفحة
                            new docx.Paragraph({
                                children: [
                                    new docx.TextRun({
                                        text: `تم إنشاء هذا التقرير بواسطة نظام إعداد التقارير - ${new Date().toLocaleDateString('ar-SA')}`,
                                        size: 18,
                                        font: "Traditional Arabic",
                                        color: "666666",
                                        italics: true
                                    })
                                ],
                                alignment: docx.AlignmentType.CENTER,
                                spacing: {
                                    before: 800
                                }
                            })
                        ]
                    }]
                });
                
                // تحميل الوثيقة
                const buffer = await docx.Packer.toBlob(doc);
                saveAs(buffer, `تقرير_${currentReportData.reportNumber}.docx`);
            }
            
            // ========== تصدير إلى HTML (تنسيق احترافي) ==========
            function exportToHTML() {
                const htmlContent = generateProfessionalPreviewHTML(currentReportData);
                const blob = new Blob([htmlContent], { type: 'text/html;charset=utf-8' });
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
            
            // ========== توليد HTML احترافي للمعاينة ==========
            function generateProfessionalPreviewHTML(reportData) {
                return `
                    <!DOCTYPE html>
                    <html dir="rtl" lang="ar">
                    <head>
                        <meta charset="UTF-8">
                        <meta name="viewport" content="width=device-width, initial-scale=1.0">
                        <title>${reportData.title}</title>
                        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
                        <style>
                            @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700&display=swap');
                            
                            * {
                                margin: 0;
                                padding: 0;
                                box-sizing: border-box;
                            }
                            
                            body {
                                font-family: 'Cairo', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
                                line-height: 1.8;
                                color: #333;
                                background: linear-gradient(135deg, #f8fafc 0%, #e8f0fe 100%);
                                min-height: 100vh;
                                padding: 40px 20px;
                                direction: rtl;
                            }
                            
                            .report-container {
                                max-width: 1000px;
                                margin: 0 auto;
                                background: white;
                                padding: 50px;
                                box-shadow: 0 20px 60px rgba(0,0,0,0.15);
                                border-radius: 20px;
                                position: relative;
                                overflow: hidden;
                                border: 1px solid rgba(255,255,255,0.3);
                            }
                            
                            .report-container::before {
                                content: '';
                                position: absolute;
                                top: 0;
                                right: 0;
                                width: 100%;
                                height: 8px;
                                background: linear-gradient(90deg, #2c5aa0 0%, #4a7bc8 100%);
                            }
                            
                            .header {
                                text-align: center;
                                margin-bottom: 60px;
                                position: relative;
                                padding-bottom: 30px;
                            }
                            
                            .header::after {
                                content: '';
                                position: absolute;
                                bottom: 0;
                                right: 50%;
                                transform: translateX(50%);
                                width: 200px;
                                height: 4px;
                                background: linear-gradient(90deg, #2c5aa0 0%, #4a7bc8 100%);
                                border-radius: 2px;
                            }
                            
                            h1 {
                                color: #2c5aa0;
                                font-size: 36px;
                                margin-bottom: 20px;
                                font-weight: 800;
                                text-shadow: 0 2px 4px rgba(0,0,0,0.1);
                            }
                            
                            .subtitle {
                                color: #666;
                                font-size: 22px;
                                font-weight: 600;
                                margin-bottom: 10px;
                            }
                            
                            .report-info {
                                display: flex;
                                justify-content: center;
                                gap: 40px;
                                margin-top: 30px;
                                flex-wrap: wrap;
                            }
                            
                            .info-item {
                                background: #f0f7ff;
                                padding: 15px 25px;
                                border-radius: 12px;
                                font-size: 18px;
                                display: flex;
                                align-items: center;
                                gap: 10px;
                                box-shadow: 0 4px 12px rgba(0,0,0,0.08);
                                transition: transform 0.3s ease;
                            }
                            
                            .info-item:hover {
                                transform: translateY(-5px);
                            }
                            
                            .info-item i {
                                color: #2c5aa0;
                                font-size: 20px;
                            }
                            
                            .section {
                                margin-bottom: 50px;
                                padding: 30px;
                                background: #f8fafc;
                                border-radius: 15px;
                                border-right: 5px solid #2c5aa0;
                                box-shadow: 0 6px 20px rgba(0,0,0,0.05);
                                position: relative;
                                overflow: hidden;
                            }
                            
                            .section::before {
                                content: '';
                                position: absolute;
                                top: 0;
                                right: 0;
                                width: 100px;
                                height: 100px;
                                background: linear-gradient(135deg, rgba(44, 90, 160, 0.05) 0%, transparent 100%);
                                border-radius: 0 0 0 100%;
                            }
                            
                            .section-title {
                                color: #2c5aa0;
                                font-size: 28px;
                                margin-bottom: 25px;
                                font-weight: 700;
                                display: flex;
                                align-items: center;
                                gap: 15px;
                            }
                            
                            .section-title i {
                                background: rgba(44, 90, 160, 0.1);
                                padding: 12px;
                                border-radius: 10px;
                                width: 55px;
                                height: 55px;
                                display: flex;
                                align-items: center;
                                justify-content: center;
                            }
                            
                            .basic-info-grid {
                                display: grid;
                                grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
                                gap: 25px;
                                margin-bottom: 30px;
                            }
                            
                            .info-card {
                                background: white;
                                padding: 25px;
                                border-radius: 12px;
                                box-shadow: 0 4px 15px rgba(0,0,0,0.05);
                                border: 1px solid #e8f0fe;
                                transition: transform 0.3s ease;
                            }
                            
                            .info-card:hover {
                                transform: translateY(-5px);
                                box-shadow: 0 8px 25px rgba(0,0,0,0.1);
                            }
                            
                            .info-label {
                                color: #2c5aa0;
                                font-weight: 600;
                                font-size: 18px;
                                margin-bottom: 10px;
                                display: flex;
                                align-items: center;
                                gap: 10px;
                            }
                            
                            .info-value {
                                color: #333;
                                font-size: 20px;
                                font-weight: 500;
                                padding-right: 10px;
                            }
                            
                            .content-box {
                                background: white;
                                padding: 30px;
                                border-radius: 12px;
                                margin-bottom: 25px;
                                box-shadow: 0 4px 15px rgba(0,0,0,0.05);
                                border: 1px solid #e8f0fe;
                            }
                            
                            .content-box p {
                                font-size: 20px;
                                line-height: 1.8;
                                color: #444;
                                text-align: justify;
                            }
                            
                            .list-container {
                                padding-right: 20px;
                            }
                            
                            .list-item {
                                display: flex;
                                align-items: flex-start;
                                gap: 15px;
                                margin-bottom: 20px;
                                padding: 15px;
                                background: white;
                                border-radius: 10px;
                                border-right: 4px solid #2c5aa0;
                                box-shadow: 0 3px 10px rgba(0,0,0,0.05);
                                transition: transform 0.3s ease;
                            }
                            
                            .list-item:hover {
                                transform: translateX(-10px);
                            }
                            
                            .list-number {
                                background: #2c5aa0;
                                color: white;
                                width: 35px;
                                height: 35px;
                                border-radius: 50%;
                                display: flex;
                                align-items: center;
                                justify-content: center;
                                font-weight: bold;
                                font-size: 18px;
                                flex-shrink: 0;
                            }
                            
                            .list-text {
                                font-size: 18px;
                                color: #444;
                                flex: 1;
                            }
                            
                            .image-gallery {
                                display: grid;
                                grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
                                gap: 25px;
                                margin-top: 30px;
                            }
                            
                            .image-card {
                                border-radius: 15px;
                                overflow: hidden;
                                box-shadow: 0 10px 30px rgba(0,0,0,0.15);
                                transition: transform 0.3s ease;
                                position: relative;
                            }
                            
                            .image-card:hover {
                                transform: translateY(-10px) scale(1.02);
                            }
                            
                            .image-card img {
                                width: 100%;
                                height: 250px;
                                object-fit: cover;
                                display: block;
                            }
                            
                            .image-caption {
                                background: rgba(44, 90, 160, 0.9);
                                color: white;
                                padding: 15px;
                                text-align: center;
                                font-size: 16px;
                            }
                            
                            .signatures {
                                display: flex;
                                justify-content: space-around;
                                margin-top: 80px;
                                padding-top: 40px;
                                border-top: 3px solid #2c5aa0;
                                flex-wrap: wrap;
                                gap: 40px;
                            }
                            
                            .signature-box {
                                text-align: center;
                                width: 300px;
                                padding: 30px;
                                background: #f8fafc;
                                border-radius: 15px;
                                box-shadow: 0 8px 25px rgba(0,0,0,0.08);
                                position: relative;
                                transition: transform 0.3s ease;
                            }
                            
                            .signature-box:hover {
                                transform: translateY(-10px);
                            }
                            
                            .signature-title {
                                color: #2c5aa0;
                                font-size: 24px;
                                font-weight: 700;
                                margin-bottom: 15px;
                            }
                            
                            .signature-name {
                                font-size: 22px;
                                color: #333;
                                margin-bottom: 30px;
                                font-weight: 600;
                            }
                            
                            .signature-line {
                                width: 200px;
                                height: 3px;
                                background: #333;
                                margin: 30px auto 15px;
                                border-radius: 2px;
                            }
                            
                            .signature-label {
                                color: #666;
                                font-size: 18px;
                                font-style: italic;
                            }
                            
                            .footer {
                                text-align: center;
                                margin-top: 60px;
                                padding-top: 30px;
                                border-top: 2px dashed #ddd;
                                color: #888;
                                font-size: 16px;
                            }
                            
                            @media (max-width: 768px) {
                                .report-container {
                                    padding: 30px 20px;
                                }
                                
                                h1 {
                                    font-size: 28px;
                                }
                                
                                .subtitle {
                                    font-size: 18px;
                                }
                                
                                .section-title {
                                    font-size: 24px;
                                }
                                
                                .basic-info-grid {
                                    grid-template-columns: 1fr;
                                }
                                
                                .signatures {
                                    flex-direction: column;
                                    align-items: center;
                                }
                                
                                .signature-box {
                                    width: 100%;
                                    max-width: 300px;
                                }
                                
                                .info-item {
                                    padding: 12px 20px;
                                    font-size: 16px;
                                }
                            }
                            
                            @media print {
                                body {
                                    background: white;
                                    padding: 0;
                                }
                                
                                .report-container {
                                    box-shadow: none;
                                    border-radius: 0;
                                    padding: 30px;
                                }
                                
                                .section, .info-card, .content-box, .list-item, .signature-box {
                                    break-inside: avoid;
                                }
                            }
                        </style>
                    </head>
                    <body>
                        <div class="report-container">
                            <div class="header">
                                <h1>${reportData.title}</h1>
                                <div class="subtitle">الإدارة العامة للتعليم بمنطقة ${reportData.region}</div>
                                
                                <div class="report-info">
                                    <div class="info-item">
                                        <i class="fas fa-hashtag"></i>
                                        <span>رقم التقرير: ${reportData.reportNumber}</span>
                                    </div>
                                    <div class="info-item">
                                        <i class="fas fa-calendar"></i>
                                        <span>تاريخ البرنامج: ${reportData.programDate}</span>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- البيانات الأساسية -->
                            <div class="section">
                                <h3 class="section-title">
                                    <i class="fas fa-database"></i>
                                    البيانات الأساسية
                                </h3>
                                
                                <div class="basic-info-grid">
                                    <div class="info-card">
                                        <div class="info-label">
                                            <i class="fas fa-school"></i>
                                            المدرسة
                                        </div>
                                        <div class="info-value">${reportData.school}</div>
                                    </div>
                                    
                                    <div class="info-card">
                                        <div class="info-label">
                                            <i class="fas fa-user-tie"></i>
                                            مدير المدرسة
                                        </div>
                                        <div class="info-value">${reportData.principal}</div>
                                    </div>
                                    
                                    <div class="info-card">
                                        <div class="info-label">
                                            <i class="fas fa-user-edit"></i>
                                            معد التقرير
                                        </div>
                                        <div class="info-value">${reportData.reporter}</div>
                                    </div>
                                    
                                    <div class="info-card">
                                        <div class="info-label">
                                            <i class="fas fa-map-marker"></i>
                                            مكان التنفيذ
                                        </div>
                                        <div class="info-value">${reportData.location}</div>
                                    </div>
                                    
                                    <div class="info-card">
                                        <div class="info-label">
                                            <i class="fas fa-users"></i>
                                            المستهدفون
                                        </div>
                                        <div class="info-value">${reportData.target}</div>
                                    </div>
                                    
                                    <div class="info-card">
                                        <div class="info-label">
                                            <i class="fas fa-user-check"></i>
                                            عدد المستفيدين
                                        </div>
                                        <div class="info-value">${reportData.beneficiaries}</div>
                                    </div>
                                    
                                    <div class="info-card">
                                        <div class="info-label">
                                            <i class="fas fa-book"></i>
                                            تابع للمناهج
                                        </div>
                                        <div class="info-value">${reportData.curriculumRelated}</div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- وصف النشاط -->
                            <div class="section">
                                <h3 class="section-title">
                                    <i class="fas fa-clipboard-list"></i>
                                    وصف مختصر لما تم تنفيذه
                                </h3>
                                
                                <div class="content-box">
                                    <p>${reportData.description}</p>
                                </div>
                            </div>
                            
                            <!-- إجراءات التنفيذ -->
                            ${reportData.procedures && reportData.procedures.length > 0 ? `
                            <div class="section">
                                <h3 class="section-title">
                                    <i class="fas fa-tasks"></i>
                                    إجراءات التنفيذ
                                </h3>
                                
                                <div class="list-container">
                                    ${reportData.procedures.map((procedure, index) => `
                                    <div class="list-item">
                                        <div class="list-number">${index + 1}</div>
                                        <div class="list-text">${procedure}</div>
                                    </div>
                                    `).join('')}
                                </div>
                            </div>
                            ` : ''}
                            
                            <!-- النتائج -->
                            ${reportData.results && reportData.results.length > 0 ? `
                            <div class="section">
                                <h3 class="section-title">
                                    <i class="fas fa-chart-line"></i>
                                    النتائج
                                </h3>
                                
                                <div class="list-container">
                                    ${reportData.results.map((result, index) => `
                                    <div class="list-item">
                                        <div class="list-number">${index + 1}</div>
                                        <div class="list-text">${result}</div>
                                    </div>
                                    `).join('')}
                                </div>
                            </div>
                            ` : ''}
                            
                            <!-- التوصيات -->
                            <div class="section">
                                <h3 class="section-title">
                                    <i class="fas fa-lightbulb"></i>
                                    التوصيات
                                </h3>
                                
                                <div class="content-box">
                                    <p>${reportData.recommendations}</p>
                                </div>
                            </div>
                            
                            <!-- الصور المرفقة -->
                            ${reportData.images && reportData.images.length > 0 ? `
                            <div class="section">
                                <h3 class="section-title">
                                    <i class="fas fa-images"></i>
                                    الصور المرفقة
                                </h3>
                                
                                <div class="image-gallery">
                                    ${reportData.images.map((img, idx) => `
                                    <div class="image-card">
                                        <img src="${img.data}" alt="صورة ${idx + 1}">
                                        <div class="image-caption">صورة ${idx + 1}: ${img.name}</div>
                                    </div>
                                    `).join('')}
                                </div>
                            </div>
                            ` : ''}
                            
                            <!-- التوقيعات -->
                            <div class="signatures">
                                <div class="signature-box">
                                    <div class="signature-title">مدير المدرسة</div>
                                    <div class="signature-name">${reportData.principal}</div>
                                    <div class="signature-line"></div>
                                    <div class="signature-label">التوقيع</div>
                                </div>
                                
                                <div class="signature-box">
                                    <div class="signature-title">معد التقرير</div>
                                    <div class="signature-name">${reportData.reporter}</div>
                                    <div class="signature-line"></div>
                                    <div class="signature-label">التوقيع</div>
                                </div>
                            </div>
                            
                            <!-- التذييل -->
                            <div class="footer">
                                <p>تم إنشاء هذا التقرير بواسطة نظام إعداد التقارير الإلكتروني</p>
                                <p>${new Date().toLocaleDateString('ar-SA', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })}</p>
                            </div>
                        </div>
                    </body>
                    </html>
                `;
            }
            
            // ========== توليد رقم التقرير ==========
            function generateReportNumber() {
                const prefix = 'REP';
                const year = new Date().getFullYear();
                const month = (new Date().getMonth() + 1).toString().padStart(2, '0');
                const day = new Date().getDate().toString().padStart(2, '0');
                const random = Math.floor(Math.random() * 10000).toString().padStart(4, '0');
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
            
            // ========== وظائف المساعدة ==========
            function showLoading(text) {
                loadingText.textContent = text;
                loadingOverlay.classList.add('active');
            }
            
            function hideLoading() {
                loadingOverlay.classList.remove('active');
            }
            
            function showError(message) {
                alert(`❌ ${message}`);
            }
            
            function showSuccess(message) {
                alert(`✅ ${message}`);
            }
            
            function showExportSuccess(format) {
                successTitle.textContent = 'تم إنشاء التقرير بنجاح!';
                successDetails.textContent = `تم تصدير التقرير بصيغة ${format === 'word' ? 'Microsoft Word' : 'HTML'}.\nرقم التقرير: ${currentReportData.reportNumber}`;
                successMessage.classList.add('active');
                
                // إعادة تعيين النموذج تلقائياً بعد 5 ثوانٍ
                setTimeout(() => {
                    if (confirm('هل تريد إعادة تعيين النموذج لبدء تقرير جديد؟')) {
                        successMessage.classList.remove('active');
                        resetForm();
                    }
                }, 5000);
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