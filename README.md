<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام إعداد التقارير التربوية - إدارة تعليم منطقة مكة المكرمة</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://unpkg.com/docx@7.7.0/build/index.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/FileSaver.js/2.0.5/FileSaver.min.js"></script>
    <style>
        :root {
            --primary-color: #2c3e50;
            --primary-dark: #1a252f;
            --primary-light: #3498db;
            --secondary-color: #ecf0f1;
            --accent-color: #e74c3c;
            --light-color: #f9f9f9;
            --dark-color: #2c3e50;
            --gray-color: #7f8c8d;
            --border-color: #bdc3c7;
            --success-color: #27ae60;
            --warning-color: #f39c12;
            --danger-color: #c0392b;
            --info-color: #2980b9;
            --shadow: 0 2px 15px rgba(0, 0, 0, 0.08);
            --shadow-lg: 0 5px 25px rgba(0, 0, 0, 0.1);
            --radius: 8px;
            --transition: all 0.3s ease;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Cairo', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
            color: var(--dark-color);
            line-height: 1.8;
            min-height: 100vh;
            padding: 0;
            direction: rtl;
        }

        @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700;800&display=swap');

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
            border-bottom: 4px solid var(--accent-color);
        }

        .header h1 {
            font-size: 28px;
            margin-bottom: 8px;
            font-weight: 800;
            text-shadow: 0 2px 4px rgba(0,0,0,0.2);
            font-family: 'Cairo', sans-serif;
        }

        .header-subtitle {
            font-size: 16px;
            opacity: 0.9;
            font-weight: 400;
            font-family: 'Cairo', sans-serif;
        }

        .main-container {
            margin-top: 130px;
            padding: 0 20px 40px;
            max-width: 1200px;
            margin-left: auto;
            margin-right: auto;
        }

        .report-form-container {
            background-color: white;
            border-radius: var(--radius);
            box-shadow: var(--shadow-lg);
            padding: 40px;
            margin-bottom: 30px;
            border: 1px solid rgba(255,255,255,0.2);
            position: relative;
            overflow: hidden;
            font-family: 'Cairo', sans-serif;
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

        .section-header {
            color: var(--primary-color);
            border-right: 4px solid var(--accent-color);
            padding-right: 20px;
            margin: 40px 0 25px;
            font-size: 24px;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 12px;
            position: relative;
            font-family: 'Cairo', sans-serif;
        }

        .section-header i {
            font-size: 22px;
            background: rgba(44, 62, 80, 0.1);
            padding: 12px;
            border-radius: 8px;
            width: 55px;
            height: 55px;
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
            font-family: 'Cairo', sans-serif;
        }

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
            font-family: 'Cairo', sans-serif;
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
            font-family: 'Cairo', sans-serif;
            transition: var(--transition);
            background-color: white;
            box-shadow: inset 0 2px 4px rgba(0,0,0,0.05);
        }

        .form-input:focus, .form-select:focus, .form-textarea:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 4px rgba(44, 62, 80, 0.15);
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

        .form-example {
            font-size: 14px;
            color: var(--gray-color);
            margin-top: 8px;
            font-style: italic;
            padding-right: 5px;
            font-family: 'Cairo', sans-serif;
        }

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
            background-color: rgba(44, 62, 80, 0.02);
            transform: translateY(-2px);
        }

        .upload-area.dragover {
            border-color: var(--primary-color);
            background-color: rgba(44, 62, 80, 0.05);
            animation: pulse 1.5s infinite;
        }

        @keyframes pulse {
            0% { box-shadow: 0 0 0 0 rgba(44, 62, 80, 0.2); }
            70% { box-shadow: 0 0 0 15px rgba(44, 62, 80, 0); }
            100% { box-shadow: 0 0 0 0 rgba(44, 62, 80, 0); }
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
            font-family: 'Cairo', sans-serif;
        }

        .upload-hint {
            font-size: 15px;
            color: var(--gray-color);
            max-width: 500px;
            margin: 0 auto;
            font-family: 'Cairo', sans-serif;
        }

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
            background: rgba(192, 57, 43, 0.9);
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
            box-shadow: 0 4px 12px rgba(44, 62, 80, 0.2);
            position: relative;
            overflow: hidden;
            font-family: 'Cairo', sans-serif;
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
            box-shadow: 0 6px 18px rgba(44, 62, 80, 0.3);
        }

        .btn:active {
            transform: translateY(-1px);
        }

        .btn-secondary {
            background-color: #7f8c8d;
        }

        .btn-secondary:hover {
            background-color: #6c757d;
        }

        .btn-success {
            background-color: var(--success-color);
        }

        .btn-success:hover {
            background-color: #219653;
        }

        .btn-info {
            background-color: var(--info-color);
        }

        .btn-info:hover {
            background-color: #1a6ea0;
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

        .action-buttons {
            display: flex;
            justify-content: space-between;
            margin-top: 60px;
            padding-top: 40px;
            border-top: 2px solid var(--border-color);
            gap: 20px;
            flex-wrap: wrap;
        }

        .instruction-box {
            background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
            border-right: 4px solid var(--accent-color);
            padding: 25px;
            border-radius: var(--radius);
            margin-bottom: 40px;
            box-shadow: var(--shadow);
            position: relative;
            overflow: hidden;
            font-family: 'Cairo', sans-serif;
        }

        .instruction-box::before {
            content: '';
            position: absolute;
            top: 0;
            right: 0;
            width: 100px;
            height: 100px;
            background: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'%3E%3Cpath fill='%23e74c3c' fill-opacity='0.05' d='M0,0 L100,0 L100,100 Z'/%3E%3C/svg%3E");
            background-size: cover;
        }

        .instruction-box h3 {
            color: var(--primary-color);
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 12px;
            font-size: 22px;
            font-family: 'Cairo', sans-serif;
        }

        .instruction-box p {
            color: var(--dark-color);
            font-size: 16px;
            line-height: 1.8;
            position: relative;
            z-index: 1;
            font-family: 'Cairo', sans-serif;
        }

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
            font-family: 'Cairo', sans-serif;
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
            font-family: 'Cairo', sans-serif;
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
            font-family: 'Cairo', sans-serif;
        }

        .export-option:hover .export-option-title {
            color: var(--primary-color);
        }

        .export-option-desc {
            font-size: 15px;
            color: var(--gray-color);
            line-height: 1.6;
            font-family: 'Cairo', sans-serif;
        }

        .export-actions {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 40px;
        }

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
            box-shadow: 0 6px 20px rgba(44, 62, 80, 0.3);
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
            font-family: 'Cairo', sans-serif;
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
            font-family: 'Cairo', sans-serif;
        }

        .success-details {
            color: var(--gray-color);
            font-size: 16px;
            margin-bottom: 25px;
            line-height: 1.8;
            font-family: 'Cairo', sans-serif;
        }

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
            font-family: 'Cairo', sans-serif;
        }

        /* تنسيقات زر الطباعة والوظائف الجديدة */
        .auto-fill-section {
            background: #f8f9fa;
            border-radius: var(--radius);
            padding: 20px;
            margin: 20px 0;
            border-right: 4px solid var(--info-color);
        }

        .auto-fill-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }

        .auto-fill-title {
            color: var(--info-color);
            font-weight: 600;
            font-size: 18px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .btn-sm {
            padding: 8px 16px;
            font-size: 14px;
            min-height: 40px;
        }

        .text-with-actions {
            position: relative;
        }

        .text-actions {
            position: absolute;
            top: 10px;
            left: 10px;
            display: flex;
            gap: 8px;
            z-index: 10;
        }

        .text-action-btn {
            background: rgba(255, 255, 255, 0.9);
            border: 1px solid var(--border-color);
            border-radius: 4px;
            padding: 6px 12px;
            font-size: 12px;
            cursor: pointer;
            transition: var(--transition);
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .text-action-btn:hover {
            background: var(--primary-color);
            color: white;
            border-color: var(--primary-color);
        }

        @media (max-width: 992px) {
            .form-row {
                grid-template-columns: 1fr;
            }
            
            .header h1 {
                font-size: 24px;
            }
            
            .main-container {
                padding: 0 15px 30px;
                margin-top: 120px;
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
            
            .text-actions {
                position: relative;
                top: 0;
                left: 0;
                margin-bottom: 10px;
                justify-content: flex-end;
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
                margin-top: 110px;
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

        ::-webkit-scrollbar {
            width: 10px;
        }

        ::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 5px;
        }

        ::-webkit-scrollbar-thumb {
            background: linear-gradient(135deg, var(--primary-color) 0%, var(--primary-light) 100%);
            border-radius: 5px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: var(--primary-dark);
        }

        .form-input.invalid, .form-select.invalid, .form-textarea.invalid {
            border-color: var(--danger-color);
            background-color: rgba(192, 57, 43, 0.05);
        }

        .validation-error {
            color: var(--danger-color);
            font-size: 14px;
            margin-top: 5px;
            display: flex;
            align-items: center;
            gap: 5px;
            font-family: 'Cairo', sans-serif;
        }

        .validation-error i {
            font-size: 16px;
        }
    </style>
</head>
<body>
    <div class="loading-overlay" id="loadingOverlay">
        <div class="loading-spinner"></div>
        <div class="loading-text" id="loadingText">جاري معالجة البيانات...</div>
    </div>

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

    <div class="header">
        <h1>نظام إعداد التقارير التربوية</h1>
        <div class="header-subtitle">إدارة تعليم منطقة مكة المكرمة</div>
    </div>

    <div class="main-container">
        <div class="instruction-box">
            <h3><i class="fas fa-info-circle"></i> تعليمات إعداد التقرير</h3>
            <p>يرجى تعبئة جميع الحقول المطلوبة (*) بدقة. يمكنك استخدام زر "تعبئة تلقائية" لملء الحقول بالنصوص المناسبة حسب نوع التقرير، ثم تعديلها حسب الحاجة.</p>
        </div>

        <div class="report-form-container">
            <div class="form-section">
                <h2 class="section-header"><i class="fas fa-file-signature"></i> اختيار نوع التقرير</h2>
                <p class="section-subtitle">اختر نوع التقرير المناسب لهذا البند من القائمة التالية</p>
                
                <div class="form-group">
                    <label class="form-label required"><i class="fas fa-tasks"></i> أداء الواجبات الوظيفية (البند رقم 1)</label>
                    <select class="form-select" id="reportType">
                        <option value="">اختر نوع التقرير...</option>
                        <option value="strategy" selected>تقرير تنفيذ استراتيجية تدريس</option>
                        <option value="activity-session">تقرير حصة النشاط الطلابي</option>
                        <option value="class-activities">تقرير الأنشطة الصفية</option>
                        <option value="educational-trip">تقرير رحلة تربوية</option>
                        <option value="workshop">تقرير ورشة عمل تربوية</option>
                        <option value="competition">تقرير مسابقة مدرسية</option>
                        <option value="parent-meeting">تقرير اجتماع أولياء الأمور</option>
                        <option value="training-program">تقرير برنامج تدريبي</option>
                        <option value="educational-project">تقرير مشروع تربوي</option>
                        <option value="scientific-club">تقرير النادي العلمي</option>
                        <option value="cultural-activity">تقرير نشاط ثقافي</option>
                        <option value="sports-activity">تقرير نشاط رياضي</option>
                        <option value="art-activity">تقرير نشاط فني</option>
                        <option value="technology-activity">تقرير نشاط تقني</option>
                    </select>
                    <div id="reportTypeError" class="validation-error" style="display: none;">
                        <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                    </div>
                </div>
                
                <div class="auto-fill-section">
                    <div class="auto-fill-header">
                        <div class="auto-fill-title">
                            <i class="fas fa-magic"></i> تعبئة تلقائية للحقول
                        </div>
                        <button class="btn btn-info btn-sm" id="autoFillBtn">
                            <i class="fas fa-bolt"></i> تعبئة تلقائية
                        </button>
                    </div>
                    <p style="color: var(--gray-color); font-size: 14px; line-height: 1.6;">
                        سيتم تعبئة الحقول التالية تلقائياً بناءً على نوع التقرير المحدد. يمكنك تعديل النصوص بعد ذلك حسب الحاجة.
                    </p>
                </div>
            </div>

            <div class="form-section">
                <h2 class="section-header"><i class="fas fa-database"></i> البيانات الرئيسية</h2>
                <p class="section-subtitle">البيانات الرئيسية التي ستظهر في رأس التقرير النهائي</p>
                
                <div class="form-row">
                    <div class="form-group">
                        <label class="form-label required"><i class="fas fa-map-marker-alt"></i> اسم المنطقة</label>
                        <input type="text" class="form-input" id="region" placeholder="مكة المكرمة" value="مكة المكرمة">
                        <div class="form-example">مثال: مكة المكرمة، المدينة المنورة، الرياض</div>
                        <div id="regionError" class="validation-error" style="display: none;">
                            <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label required"><i class="fas fa-school"></i> اسم المدرسة</label>
                        <input type="text" class="form-input" id="school" placeholder="اسم المدرسة" value="سعيد بن العاص المتوسطة">
                        <div id="schoolError" class="validation-error" style="display: none;">
                            <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                        </div>
                    </div>
                </div>
                
                <div class="form-row">
                    <div class="form-group">
                        <label class="form-label required"><i class="fas fa-user-tie"></i> مدير المدرسة</label>
                        <input type="text" class="form-input" id="principal" placeholder="مدير المدرسة" value="أ. نايف بن أحمد اللحياني">
                        <div class="form-example">مثال: أ. نايف بن أحمد اللحياني</div>
                        <div id="principalError" class="validation-error" style="display: none;">
                            <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label required"><i class="fas fa-user-edit"></i> معد التقرير</label>
                        <input type="text" class="form-input" id="reporter" placeholder="معد التقرير" value="أ. فهد بن محمد الخالدي">
                        <div class="form-example">مثال: أ. فهد بن محمد الخالدي</div>
                        <div id="reporterError" class="validation-error" style="display: none;">
                            <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                        </div>
                    </div>
                </div>
                
                <div class="form-group">
                    <label class="form-label required"><i class="fas fa-heading"></i> عنوان التقرير</label>
                    <input type="text" class="form-input" id="reportTitle" placeholder="عنوان التقرير" value="تقرير تنفيذ استراتيجية تدريس">
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
                        <input type="text" class="form-input" id="location" placeholder="مثال: قاعة المصادر" value="قاعة المصادر">
                        <div class="form-example">مثال: قاعة المصادر، الفصل الدراسي، الساحة المدرسية</div>
                        <div id="locationError" class="validation-error" style="display: none;">
                            <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                        </div>
                    </div>
                </div>
                
                <div class="form-row">
                    <div class="form-group">
                        <label class="form-label required"><i class="fas fa-users"></i> المستهدفون</label>
                        <input type="text" class="form-input" id="target" placeholder="مثال: طلاب الصف الثالث متوسط" value="طلاب الصف الثالث متوسط">
                        <div class="form-example">مثال: طلاب الصف الثالث متوسط، معلمو المرحلة</div>
                        <div id="targetError" class="validation-error" style="display: none;">
                            <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label class="form-label required"><i class="fas fa-user-check"></i> عدد المستفيدين</label>
                        <input type="number" class="form-input" id="beneficiaries" placeholder="مثال: 30" value="30" min="1">
                        <div class="form-example">أدخل عدد المستفيدين من البرنامج (رقم فقط)</div>
                        <div id="beneficiariesError" class="validation-error" style="display: none;">
                            <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                        </div>
                    </div>
                </div>
            </div>

            <div class="form-section">
                <h2 class="section-header"><i class="fas fa-align-left"></i> وصف النشاط</h2>
                <p class="section-subtitle">وصف شامل وواضح للنشاط الذي تم تنفيذه</p>
                
                <div class="form-group text-with-actions">
                    <div class="text-actions">
                        <button type="button" class="text-action-btn" id="clearDescription">
                            <i class="fas fa-trash-alt"></i> حذف النص
                        </button>
                    </div>
                    <label class="form-label required"><i class="fas fa-clipboard-list"></i> وصف مختصر لما تم تنفيذه</label>
                    <textarea class="form-textarea" id="description" placeholder="وصف مختصر لما تم تنفيذه في النشاط">تم تنفيذ استراتيجية التدريس وفق الخطة المعتمدة، مع توزيع الطلاب على مجموعات عمل تعاونية وتنويع الأنشطة بما يناسب ميولهم واحتياجاتهم. تم تطبيق استراتيجية التعلم النشط من خلال أنشطة عملية وتفاعلية.</textarea>
                    <div class="form-example">يجب أن يتضمن الوصف ملخصاً واضحاً وشاملاً للنشاط المنفذ</div>
                    <div id="descriptionError" class="validation-error" style="display: none;">
                        <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                    </div>
                </div>
            </div>

            <div class="form-section">
                <h2 class="section-header"><i class="fas fa-tasks"></i> إجراءات التنفيذ</h2>
                <p class="section-subtitle">الخطوات والإجراءات التي تم اتباعها لتنفيذ النشاط</p>
                
                <div class="form-group text-with-actions">
                    <div class="text-actions">
                        <button type="button" class="text-action-btn" id="clearProcedures">
                            <i class="fas fa-trash-alt"></i> حذف النص
                        </button>
                    </div>
                    <label class="form-label required"><i class="fas fa-list-ol"></i> إجراءات التنفيذ (افصل بين النقاط بفاصلة)</label>
                    <textarea class="form-textarea" id="procedures" placeholder="أدخل إجراءات التنفيذ">إعداد خطة حصة النشاط وتحديد الأهداف والأنشطة المناسبة, توزيع الطلاب إلى مجموعات عمل وتوضيح المهام لكل مجموعة, توفير المواد والأدوات اللازمة للنشاط, متابعة تنفيذ الطلاب للنشاط وتقديم التوجيه اللازم, تقييم مخرجات النشاط من قبل الطلاب والمعلم</textarea>
                    <div class="form-example">أدخل كل إجراء في سطر جديد أو افصل بين النقاط بفاصلة (,) كل إجراء يجب أن يكون جملة كاملة</div>
                    <div id="proceduresError" class="validation-error" style="display: none;">
                        <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                    </div>
                </div>
            </div>

            <div class="form-section">
                <h2 class="section-header"><i class="fas fa-chart-line"></i> النتائج</h2>
                <p class="section-subtitle">النتائج المتحققة والأثر الإيجابي للنشاط</p>
                
                <div class="form-group text-with-actions">
                    <div class="text-actions">
                        <button type="button" class="text-action-btn" id="clearResults">
                            <i class="fas fa-trash-alt"></i> حذف النص
                        </button>
                    </div>
                    <label class="form-label required"><i class="fas fa-chart-bar"></i> النتائج (افصل بين النقاط بفاصلة)</label>
                    <textarea class="form-textarea" id="results" placeholder="أدخل النتائج المتحققة">تفاعل إيجابي من الطلاب أثناء تنفيذ استراتيجية التدريس, تنمية روح التعاون والعمل الجماعي بين الطلاب, اكتشاف مواهب الطلاب في مجالات متنوعة, تطبيق المعرفة النظرية في أنشطة عملية, زيادة دافعية الطلاب للتعلم والمشاركة</textarea>
                    <div class="form-example">اذكر النتائج الإيجابية التي تحققت من تنفيذ النشاط بشكل واضح ومفصل</div>
                    <div id="resultsError" class="validation-error" style="display: none;">
                        <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                    </div>
                </div>
            </div>

            <div class="form-section">
                <h2 class="section-header"><i class="fas fa-lightbulb"></i> التوصيات</h2>
                <p class="section-subtitle">توصيات للتحسين والتطوير في المستقبل</p>
                
                <div class="form-group text-with-actions">
                    <div class="text-actions">
                        <button type="button" class="text-action-btn" id="clearRecommendations">
                            <i class="fas fa-trash-alt"></i> حذف النص
                        </button>
                    </div>
                    <label class="form-label required"><i class="fas fa-comments"></i> التوصيات</label>
                    <textarea class="form-textarea" id="recommendations" placeholder="أدخل التوصيات">الاستمرار في تنويع استراتيجيات التدريس وتوثيق الممارسات المميزة لإثراء التجارب المستقبلية. توفير المزيد من الموارد والأدوات اللازمة للأنشطة العملية. تشجيع الطلاب المبدعين للمشاركة في المسابقات والمنافسات الخارجية. عقد ورش عمل للمعلمين لتبادل الخبرات في مجال استراتيجيات التدريس الحديثة.</textarea>
                    <div class="form-example">قدم توصيات واضحة وعملية للتحسين والتطوير في المستقبل</div>
                    <div id="recommendationsError" class="validation-error" style="display: none;">
                        <i class="fas fa-exclamation-circle"></i> هذا الحقل مطلوب
                    </div>
                </div>
            </div>

            <div class="form-section upload-section">
                <h2 class="section-header"><i class="fas fa-images"></i> الصور المرفقة بالتقرير</h2>
                <p class="section-subtitle">صور توثيقية للنشاط المنفذ (صورتان كحد أقصى)</p>
                
                <div class="upload-area" id="uploadArea">
                    <div class="upload-icon">
                        <i class="fas fa-cloud-upload-alt"></i>
                    </div>
                    <div class="upload-text">انقر لرفع الصور أو اسحبها إلى هنا</div>
                    <div class="upload-hint">الحجم الأقصى: 5MB لكل صورة | الصيغ المدعومة: JPG, PNG, GIF | الحد الأقصى: 4 صور</div>
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

            <div class="action-buttons">
                <button class="btn btn-secondary" id="saveDraft">
                    <i class="fas fa-save"></i> حفظ كمسودة
                </button>
                
                <div style="display: flex; gap: 20px; flex-wrap: wrap;">
                    <button class="btn btn-outline" id="previewReport">
                        <i class="fas fa-eye"></i> معاينة التقرير
                    </button>
                    <button class="btn btn-success" id="createReport">
                        <i class="fas fa-file-alt"></i> إنشاء التقرير النهائي
                    </button>
                </div>
            </div>
        </div>
    </div>

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
                    اختر الصيغة المناسبة لتصدير التقرير النهائي. يمكنك طباعة التقرير مباشرة بعد إنشاء ملف Word.
                </p>
                
                <div class="export-options">
                    <div class="export-option" data-format="word">
                        <i class="fas fa-file-word"></i>
                        <div class="export-option-title">Microsoft Word</div>
                        <div class="export-option-desc">نسق احترافي قابلة للتعديل والطباعة مع تنسيق متقدم يدعم اللغة العربية</div>
                    </div>
                    
                    <div class="export-option" data-format="print">
                        <i class="fas fa-print"></i>
                        <div class="export-option-title">طباعة مباشرة</div>
                        <div class="export-option-desc">طباعة التقرير مباشرة على ورق A4 مع تنسيق احترافي</div>
                    </div>
                    
                    <div class="export-option" data-format="html">
                        <i class="fas fa-file-code"></i>
                        <div class="export-option-title">نسخة ويب</div>
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

    <div class="scroll-indicator" id="scrollToTop">
        <i class="fas fa-arrow-up"></i>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const uploadArea = document.getElementById('uploadArea');
            const imageUpload = document.getElementById('imageUpload');
            const imagePreview = document.getElementById('imagePreview');
            const scrollToTopBtn = document.getElementById('scrollToTop');
            const saveDraftBtn = document.getElementById('saveDraft');
            const previewReportBtn = document.getElementById('previewReport');
            const createReportBtn = document.getElementById('createReport');
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
            const autoFillBtn = document.getElementById('autoFillBtn');
            const clearDescription = document.getElementById('clearDescription');
            const clearProcedures = document.getElementById('clearProcedures');
            const clearResults = document.getElementById('clearResults');
            const clearRecommendations = document.getElementById('clearRecommendations');
            
            let uploadedImages = [];
            let currentReportData = null;
            
            // نصوص تلقائية لأنواع التقارير المختلفة
            const reportTemplates = {
                'strategy': {
                    description: 'تم تنفيذ استراتيجية تدريس حديثة تعتمد على التعلم النشط والتعاوني، حيث تم تصميم الأنشطة لتتناسب مع قدرات الطلاب المختلفة وتنمي مهارات التفكير العليا لديهم. ركزت الاستراتيجية على جعل الطالب محور العملية التعليمية.',
                    procedures: 'تحليل المحتوى التعليمي وتحديد الأهداف, تصميم أنشطة تعليمية متنوعة, تقسيم الطلاب إلى مجموعات عمل, توفير الأدوات والمواد التعليمية, تقديم التوجيه والإرشاد, تقييم الأداء وتقديم التغذية الراجعة',
                    results: 'تحسن ملحوظ في مستوى الفهم والاستيعاب, زيادة مشاركة الطلاب في الأنشطة الصفية, تنمية مهارات العمل الجماعي, ارتفاع مستوى التحصيل الدراسي, تعزيز الثقة بالنفس لدى الطلاب',
                    recommendations: 'الاستمرار في تطبيق استراتيجيات التعلم النشط, تنظيم ورش عمل للمعلمين حول استراتيجيات التدريس, توفير المزيد من الموارد التعليمية, توثيق التجارب الناجحة ونشرها'
                },
                'activity-session': {
                    description: 'تم تنفيذ حصة نشاط طلابي هادفة تهدف إلى تنمية المهارات الحياتية والاجتماعية للطلاب، حيث اشتملت على أنشطة عملية وتفاعلية تعزز القيم والمبادئ التربوية.',
                    procedures: 'تحديد أهداف حصة النشاط, إعداد المواد والأدوات اللازمة, تنظيم المكان وتجهيزه, شرح النشاط وتوزيع المهام, متابعة تنفيذ الطلاب, تقييم النتائج وتلخيصها',
                    results: 'تفاعل إيجابي من جميع الطلاب, اكتشاف مواهب وقدرات جديدة, تنمية روح التعاون والمسؤولية, تحسين المهارات الاجتماعية, زيادة الحماس للأنشطة المدرسية',
                    recommendations: 'تنويع أنشطة الحصص النشاطية, تخصيص مساحة أكبر للأنشطة, إشراك أولياء الأمور في بعض الأنشطة, تنظيم مسابقات بين الفصول'
                },
                'class-activities': {
                    description: 'تم تنفيذ مجموعة من الأنشطة الصفية المتنوعة التي تهدف إلى تعزيز عملية التعلم وجعلها أكثر متعة وفعالية، حيث تم دمج الأنشطة العملية مع النظرية.',
                    procedures: 'تخطيط الأنشطة المناسبة للمنهج, تحضير الوسائل التعليمية, تقسيم الوقت بين الأنشطة, تنفيذ الأنشطة بالتسلسل المناسب, تقييم مشاركة الطلاب, تحليل النتائج',
                    results: 'تحسين مستوى التركيز والانتباه, تنمية المهارات العملية, زيادة التفاعل داخل الفصل, تحسين العلاقة بين المعلم والطلاب, رفع مستوى التحصيل الدراسي',
                    recommendations: 'تطوير بنك للأنشطة الصفية, تدريب المعلمين على تصميم الأنشطة, توفير أدوات وأنشطة متنوعة, تقييم دوري لفعالية الأنشطة'
                },
                'educational-trip': {
                    description: 'تم تنظيم رحلة تربوية تعليمية هادفة إلى موقع ذو أهمية علمية أو تاريخية، حيث تعرف الطلاب على جوانب عملية تطبيقية لما درسوه نظرياً في المنهج.',
                    procedures: 'اختيار المكان المناسب للرحلة, الحصول على الموافقات الرسمية, تجهيز وسائل النقل والسلامة, إعداد برنامج الرحلة التفصيلي, تنفيذ الرحلة مع المراقبة المستمرة, تقييم الرحلة وجمع الملاحظات',
                    results: 'تعزيز المعرفة العملية للطلاب, تنمية مهارات الملاحظة والتسجيل, تعزيز الروح الجماعية, اكتساب خبرات جديدة, ربط المعرفة النظرية بالتطبيق العملي',
                    recommendations: 'تنويع وجهات الرحلات التربوية, زيادة عدد الرحلات خلال العام, إعداد أدلة إرشادية للرحلات, توثيق الرحلات بالصور والتقارير'
                },
                'workshop': {
                    description: 'تم عقد ورشة عمل تربوية متخصصة بهدف تطوير المهارات المهنية للمعلمين أو الطلاب، حيث تم التركيز على الجانب التطبيقي والعملي.',
                    procedures: 'تحديد موضوع وهدف الورشة, إعداد المحتوى والمواد التدريبية, اختيار المدربين المتخصصين, تجهيز القاعة والتجهيزات, تنفيذ جلسات الورشة, تقييم الأثر وتلخيص المخرجات',
                    results: 'اكتساب مهارات جديدة ومتخصصة, تحسين الممارسات التعليمية, تبادل الخبرات بين المشاركين, تطوير أساليب التدريس, زيادة الوعي بأحدث المستجدات التربوية',
                    recommendations: 'تنظيم ورش عمل دورية, دعوة خبراء متخصصين, تخصيص ميزانية للتدريب, توثيق مخرجات الورش وتعميمها'
                },
                'competition': {
                    description: 'تم تنظيم مسابقة مدرسية في أحد المجالات الأكاديمية أو الثقافية أو الرياضية بهدف تحفيز الطلاب وتنمية روح التنافس الإيجابي بينهم.',
                    procedures: 'تحديد نوع وموضوع المسابقة, وضع الشروط والقواعد, تشكيل لجان التحكيم, تسجيل المشاركين, تنفيذ مراحل المسابقة, إعلان النتائج وتكريم الفائزين',
                    results: 'اكتشاف المواهب المتميزة, تنمية روح المنافسة الشريفة, تشجيع الابتكار والإبداع, تعزيز الثقة بالنفس, نشر روح الحماس بين الطلاب',
                    recommendations: 'تنويع مجالات المسابقات, زيادة عدد المسابقات خلال العام, رفع مستوى الجوائز التشجيعية, توثيق المسابقات وإبراز المواهب'
                },
                'parent-meeting': {
                    description: 'تم عقد اجتماع لأولياء الأمور بهدف تعزيز الشراكة بين المدرسة والأسرة ومناقشة سبل تطوير العملية التعليمية ومتابعة تحصيل الطلاب.',
                    procedures: 'تحديد جدول أعمال الاجتماع, إرسال الدعوات لأولياء الأمور, تجهيز القاعة والعرض التقديمي, عقد الاجتماع وطرح المواضيع, مناقشة المقترحات والتوصيات, متابعة تنفيذ القرارات',
                    results: 'تحسين التواصل مع أولياء الأمور, زيادة وعي الأسر بالعملية التعليمية, التعرف على احتياجات الطلاب, تعزيز الشراكة المجتمعية, تحسين مستوى التحصيل الدراسي',
                    recommendations: 'زيادة عدد الاجتماعات الدورية, تنويع وسائل التواصل مع الأسر, إشراك أولياء الأمور في الأنشطة, إنشاء قنوات اتصال دائمة'
                },
                'training-program': {
                    description: 'تم تنفيذ برنامج تدريبي متكامل يهدف إلى تطوير المهارات المهنية أو الأكاديمية للمستفيدين، مع التركيز على الجانب التطبيقي العملي.',
                    procedures: 'تحليل الاحتياجات التدريبية, تصميم البرنامج التدريبي, إعداد المواد والأدوات, تنفيذ الجلسات التدريبية, متابعة التطبيق العملي, تقييم الأثر التدريبي',
                    results: 'تحسين الأداء المهني, اكتساب معارف ومهارات جديدة, رفع مستوى الكفاءة, تحسين جودة المخرجات, زيادة الرضا الوظيفي',
                    recommendations: 'استمرار البرامج التدريبية, تحديث المحتوى التدريبي, تخصيص ميزانية للتدريب, متابعة التطبيق بعد التدريب'
                },
                'educational-project': {
                    description: 'تم تنفيذ مشروع تربوي هادف يهدف إلى معالجة قضية تعليمية أو تنمية مهارة محددة لدى الطلاب، حيث تم تطبيق منهجية المشاريع في التعلم.',
                    procedures: 'تحديد فكرة المشروع وأهدافه, تخطيط مراحل التنفيذ, توزيع المهام والمسؤوليات, تنفيذ أنشطة المشروع, متابعة التقدم والإنجاز, تقييم النتائج والعرض',
                    results: 'تنمية مهارات البحث والاستقصاء, تعزيز العمل الجماعي, تطبيق المعرفة في حل مشكلات حقيقية, تنمية مهارات العرض والتقديم, زيادة الثقة بالنفس',
                    recommendations: 'تعميم منهجية المشاريع في التعليم, توفير الدعم اللوجستي للمشاريع, تنظيم معارض لعرض المشاريع, تدريب المعلمين على إدارة المشاريع'
                },
                'scientific-club': {
                    description: 'تم تنفيذ أنشطة النادي العلمي التي تهدف إلى تنمية الميول العلمية والبحثية لدى الطلاب، وتعزيز روح الاستكشاف والابتكار.',
                    procedures: 'تخطيط أنشطة النادي العلمي, تجهيز المعمل والأدوات, تنفيذ التجارب والبحوث, توثيق النتائج والملاحظات, عرض الإنجازات والابتكارات, تقييم فعالية الأنشطة',
                    results: 'تنمية التفكير العلمي, تشجيع الابتكار والاختراع, تحسين المهارات البحثية, زيادة الاهتمام بالعلوم, اكتشاف المواهب العلمية',
                    recommendations: 'توفير أدوات ومعدات علمية, تنظيم زيارات للمراكز العلمية, إشراك الطلاب في مسابقات علمية, توثيق إنجازات النادي العلمي'
                },
                'cultural-activity': {
                    description: 'تم تنفيذ نشاط ثقافي هادف يعزز الهوية الوطنية والثقافية، ويسهم في تنمية الوعي الثقافي والحضاري لدى الطلاب.',
                    procedures: 'تحديد الموضوع الثقافي, إعداد المواد والمحتوى الثقافي, تنظيم الفعاليات والأنشطة, إشراك الطلاب في العروض, تقييم الفعاليات الثقافية, توثيق الأنشطة',
                    results: 'تعزيز الانتماء الوطني, تنمية الوعي الثقافي, اكتشاف المواهب الثقافية, تعزيز قيم التسامح والتعايش, تنمية المهارات الإبداعية',
                    recommendations: 'تنويع الأنشطة الثقافية, إشراك المجتمع المحلي, توثيق التراث الثقافي, تنظيم معارض ثقافية دورية'
                },
                'sports-activity': {
                    description: 'تم تنفيذ نشاط رياضي يسهم في تنمية اللياقة البدنية والصحية للطلاب، وتعزيز القيم الرياضية والتنافس الشريف.',
                    procedures: 'تخطيط البرنامج الرياضي, تجهيز الملعب والأدوات, تنفيذ التدريبات والمسابقات, متابعة الأداء الرياضي, تقييم المستوى والتقدم, تنظيم المسابقات الرياضية',
                    results: 'تحسين اللياقة البدنية, تنمية الروح الرياضية, اكتشاف المواهب الرياضية, تعزيز العمل الجماعي, تحسين الصحة العامة',
                    recommendations: 'توفير مرافق رياضية مناسبة, تنظيم دوريات رياضية دورية, تدريب الكوادر الرياضية, تشجيع المشاركة في المنافسات'
                },
                'art-activity': {
                    description: 'تم تنفيذ نشاط فني إبداعي يهدف إلى تنمية المواهب الفنية والإبداعية لدى الطلاب، وتعزيز التذوق الفني والجمالي.',
                    procedures: 'تحديد المجال الفني, تجهيز المواد والأدوات الفنية, تقديم الإرشاد والتوجيه الفني, تنفيذ الأعمال الفنية, تقييم الإبداعات الفنية, عرض الأعمال الفنية',
                    results: 'تنمية المواهب الفنية, تحسين التذوق الجمالي, تشجيع الإبداع والتعبير, اكتشاف المواهب الفنية, تعزيز الثقة بالنفس',
                    recommendations: 'توفير أدوات ومواد فنية, تنظيم معارض فنية دورية, إشراك فنانين متخصصين, دمج الفن في المناهج الدراسية'
                },
                'technology-activity': {
                    description: 'تم تنفيذ نشاط تقني يهدف إلى تنمية مهارات الطلاب في مجال التكنولوجيا والابتكار الرقمي، وتعزيز الثقافة التقنية.',
                    procedures: 'تحديد المجال التقني, تجهيز الأجهزة والبرامج, تقديم التدريب التقني, تنفيذ المشاريع التقنية, تقييم المخرجات التقنية, عرض الإنجازات التقنية',
                    results: 'تحسين المهارات التقنية, تشجيع الابتكار الرقمي, اكتشاف المواهب التقنية, تعزيز الثقافة الرقمية, تطوير حلول تقنية مبتكرة',
                    recommendations: 'تحديث الأجهزة والبرامج, تنظيم ورش تقنية متخصصة, المشاركة في المسابقات التقنية, إنشاء نادي للتقنية والابتكار'
                }
            };
            
            function setupEventListeners() {
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
                
                scrollToTopBtn.addEventListener('click', function() {
                    window.scrollTo({ top: 0, behavior: 'smooth' });
                });
                
                window.addEventListener('scroll', function() {
                    if (window.scrollY > 300) {
                        scrollToTopBtn.classList.add('visible');
                    } else {
                        scrollToTopBtn.classList.remove('visible');
                    }
                });
                
                saveDraftBtn.addEventListener('click', saveAsDraft);
                previewReportBtn.addEventListener('click', previewReport);
                createReportBtn.addEventListener('click', createReport);
                
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
                
                closeExportModal.addEventListener('click', function() {
                    exportModal.style.display = 'none';
                });
                
                cancelExport.addEventListener('click', function() {
                    exportModal.style.display = 'none';
                });
                
                exportOptions.forEach(option => {
                    option.addEventListener('click', function() {
                        const format = this.dataset.format;
                        exportReport(format);
                    });
                });
                
                window.addEventListener('click', function(event) {
                    if (event.target === exportModal) {
                        exportModal.style.display = 'none';
                    }
                });
                
                closeSuccessMessage.addEventListener('click', function() {
                    successMessage.classList.remove('active');
                });
                
                autoFillBtn.addEventListener('click', autoFillFields);
                clearDescription.addEventListener('click', () => clearField('description'));
                clearProcedures.addEventListener('click', () => clearField('procedures'));
                clearResults.addEventListener('click', () => clearField('results'));
                clearRecommendations.addEventListener('click', () => clearField('recommendations'));
            }
            
            function handleImageUpload(files) {
                if (uploadedImages.length + files.length > 4) {
                    showError('يمكنك رفع 4 صور كحد أقصى فقط');
                    return;
                }
                
                for (let i = 0; i < files.length; i++) {
                    const file = files[i];
                    
                    if (!file.type.startsWith('image/')) {
                        showError('الرجاء رفع ملفات صور فقط (JPG, PNG, GIF)');
                        continue;
                    }
                    
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
                
                imageUpload.value = '';
            }
            
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
                
                document.querySelectorAll('.preview-remove').forEach(btn => {
                    btn.addEventListener('click', function() {
                        const index = parseInt(this.dataset.index);
                        uploadedImages.splice(index, 1);
                        updateImagePreview();
                    });
                });
            }
            
            function loadInitialData() {
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
            
            function loadDraftData(draftData) {
                document.getElementById('reportType').value = draftData.type || 'strategy';
                document.getElementById('reportTitle').value = draftData.title || 'تقرير تنفيذ استراتيجية تدريس';
                document.getElementById('curriculumRelated').value = draftData.curriculumRelated || 'نعم';
                document.getElementById('programDate').value = draftData.programDate || '1447-06-12';
                document.getElementById('location').value = draftData.location || '';
                document.getElementById('target').value = draftData.target || '';
                document.getElementById('beneficiaries').value = draftData.beneficiaries || '30';
                document.getElementById('description').value = draftData.description || '';
                document.getElementById('procedures').value = draftData.procedures ? (Array.isArray(draftData.procedures) ? draftData.procedures.join(', ') : draftData.procedures) : '';
                document.getElementById('results').value = draftData.results ? (Array.isArray(draftData.results) ? draftData.results.join(', ') : draftData.results) : '';
                document.getElementById('recommendations').value = draftData.recommendations || '';
                
                if (draftData.images && draftData.images.length > 0) {
                    uploadedImages = [...draftData.images];
                    updateImagePreview();
                }
                
                showSuccess('تم تحميل بيانات المسودة بنجاح');
            }
            
            function autoFillFields() {
                const reportType = document.getElementById('reportType').value;
                const reportTitle = document.getElementById('reportTitle').value;
                
                if (!reportType) {
                    showError('يرجى اختيار نوع التقرير أولاً');
                    return;
                }
                
                const template = reportTemplates[reportType];
                if (template) {
                    // تعبئة الحقول بالنصوص التلقائية
                    document.getElementById('description').value = template.description;
                    document.getElementById('procedures').value = template.procedures;
                    document.getElementById('results').value = template.results;
                    document.getElementById('recommendations').value = template.recommendations;
                    
                    // تحديث عنوان التقرير إذا لم يتم تعديله
                    if (!reportTitle || reportTitle === 'تقرير تنفيذ استراتيجية تدريس') {
                        const reportTypeText = document.getElementById('reportType').options[document.getElementById('reportType').selectedIndex].text;
                        document.getElementById('reportTitle').value = reportTypeText;
                    }
                    
                    showSuccess('تم تعبئة الحقول تلقائياً بنجاح. يمكنك تعديل النصوص حسب الحاجة.');
                } else {
                    showError('لا يوجد قالب لهذا النوع من التقارير');
                }
            }
            
            function clearField(fieldId) {
                document.getElementById(fieldId).value = '';
                showSuccess('تم حذف النص من الحقل');
            }
            
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
            
            function saveAsDraft() {
                if (!validateForm()) {
                    showError('يرجى ملء جميع الحقول المطلوبة قبل الحفظ');
                    return;
                }
                
                const reportData = collectReportData();
                reportData.status = 'draft';
                reportData.savedAt = new Date().toLocaleString('ar-SA');
                
                localStorage.setItem('reportDraft', JSON.stringify(reportData));
                
                showSuccess('تم حفظ التقرير كمسودة بنجاح!\n' + reportData.savedAt);
            }
            
            function previewReport() {
                if (!validateForm()) {
                    showError('يرجى ملء جميع الحقول المطلوبة قبل المعاينة');
                    return;
                }
                
                currentReportData = collectReportData();
                currentReportData.reportNumber = generateReportNumber();
                
                const previewWindow = window.open('', '_blank');
                previewWindow.document.write(generatePreviewHTML(currentReportData));
                previewWindow.document.close();
            }
            
            function createReport() {
                if (!validateForm()) {
                    showError('يرجى ملء جميع الحقول المطلوبة قبل الإنشاء');
                    return;
                }
                
                currentReportData = collectReportData();
                currentReportData.status = 'completed';
                currentReportData.submissionDate = new Date().toLocaleDateString('ar-SA');
                currentReportData.reportNumber = generateReportNumber();
                
                exportModal.style.display = 'flex';
            }
            
            async function exportReport(format) {
                if (!currentReportData) {
                    showError('لا توجد بيانات للتقرير');
                    return;
                }
                
                exportModal.style.display = 'none';
                
                switch(format) {
                    case 'word':
                        showLoading('جاري إنشاء ملف Word...');
                        try {
                            await exportToWord();
                            hideLoading();
                            showSuccess('تم إنشاء ملف Word بنجاح! يمكنك فتحه وطباعته مباشرة.');
                        } catch (error) {
                            hideLoading();
                            showError(`حدث خطأ أثناء إنشاء ملف Word: ${error.message}`);
                        }
                        break;
                        
                    case 'print':
                        showLoading('جاري تحضير التقرير للطباعة...');
                        setTimeout(() => {
                            printReport();
                            hideLoading();
                        }, 500);
                        break;
                        
                    case 'html':
                        showLoading('جاري إنشاء نسخة الويب...');
                        setTimeout(() => {
                            exportToHTML();
                            hideLoading();
                            showSuccess('تم إنشاء نسخة الويب بنجاح!');
                        }, 500);
                        break;
                }
            }
            
            async function exportToWord() {
                const docx = window.docx;
                const { AlignmentType, BorderStyle, WidthType, TableCell, TableRow } = docx;
                
                const children = [];
                
                // الهيدر الرئيسي
                children.push(
                    new docx.Paragraph({
                        children: [
                            new docx.TextRun({
                                text: "إدارة تعليم منطقة مكة المكرمة",
                                bold: true,
                                size: 36,
                                font: "Traditional Arabic",
                                color: "2c3e50"
                            })
                        ],
                        alignment: AlignmentType.CENTER,
                        spacing: { after: 200 }
                    }),
                    
                    new docx.Paragraph({
                        children: [
                            new docx.TextRun({
                                text: "مكتب التعليم بوسط مكة",
                                bold: true,
                                size: 28,
                                font: "Traditional Arabic",
                                color: "2c3e50"
                            })
                        ],
                        alignment: AlignmentType.CENTER,
                        spacing: { after: 400 }
                    }),
                    
                    new docx.Paragraph({
                        children: [
                            new docx.TextRun({
                                text: currentReportData.title,
                                bold: true,
                                size: 32,
                                font: "Traditional Arabic",
                                color: "000000"
                            })
                        ],
                        alignment: AlignmentType.CENTER,
                        border: {
                            bottom: {
                                color: "e74c3c",
                                size: 8,
                                space: 2,
                                style: BorderStyle.SINGLE
                            }
                        },
                        spacing: { after: 600 }
                    })
                );
                
                // معلومات التقرير
                const infoTable = new docx.Table({
                    rows: [
                        new TableRow({
                            children: [
                                new TableCell({
                                    children: [
                                        new docx.Paragraph({
                                            children: [
                                                new docx.TextRun({
                                                    text: `رقم التقرير: ${currentReportData.reportNumber}`,
                                                    size: 22,
                                                    font: "Traditional Arabic",
                                                    bold: true
                                                })
                                            ],
                                            alignment: AlignmentType.RIGHT
                                        })
                                    ],
                                    width: { size: 50, type: WidthType.PERCENTAGE }
                                }),
                                new TableCell({
                                    children: [
                                        new docx.Paragraph({
                                            children: [
                                                new docx.TextRun({
                                                    text: `التاريخ: ${currentReportData.programDate} هـ`,
                                                    size: 22,
                                                    font: "Traditional Arabic"
                                                })
                                            ],
                                            alignment: AlignmentType.RIGHT
                                        })
                                    ],
                                    width: { size: 50, type: WidthType.PERCENTAGE }
                                })
                            ]
                        })
                    ],
                    width: { size: 100, type: WidthType.PERCENTAGE }
                });
                
                children.push(infoTable);
                children.push(new docx.Paragraph({ text: "", spacing: { after: 400 } }));
                
                // جدول البيانات الأساسية
                children.push(
                    new docx.Paragraph({
                        children: [
                            new docx.TextRun({
                                text: "البيانات الأساسية",
                                bold: true,
                                size: 28,
                                font: "Traditional Arabic",
                                color: "2c3e50"
                            })
                        ],
                        alignment: AlignmentType.RIGHT,
                        spacing: { before: 200, after: 300 }
                    })
                );
                
                const basicInfoRows = [
                    { label: "المدرسة", value: currentReportData.school },
                    { label: "مدير المدرسة", value: currentReportData.principal },
                    { label: "معد التقرير", value: currentReportData.reporter },
                    { label: "مكان التنفيذ", value: currentReportData.location },
                    { label: "المستهدفون", value: currentReportData.target },
                    { label: "عدد المستفيدين", value: currentReportData.beneficiaries },
                    { label: "تابع للمناهج", value: currentReportData.curriculumRelated }
                ];
                
                const basicInfoTableRows = basicInfoRows.map(item => 
                    new TableRow({
                        children: [
                            new TableCell({
                                children: [
                                    new docx.Paragraph({
                                        children: [
                                            new docx.TextRun({
                                                text: item.value,
                                                size: 24,
                                                font: "Traditional Arabic"
                                            })
                                        ],
                                        alignment: AlignmentType.RIGHT
                                    })
                                ],
                                width: { size: 60, type: WidthType.PERCENTAGE }
                            }),
                            new TableCell({
                                children: [
                                    new docx.Paragraph({
                                        children: [
                                            new docx.TextRun({
                                                text: item.label,
                                                bold: true,
                                                size: 24,
                                                font: "Traditional Arabic"
                                            })
                                        ],
                                        alignment: AlignmentType.RIGHT
                                    })
                                ],
                                shading: { fill: "f8f9fa" },
                                width: { size: 40, type: WidthType.PERCENTAGE }
                            })
                        ]
                    })
                );
                
                children.push(
                    new docx.Table({
                        rows: basicInfoTableRows,
                        width: { size: 100, type: WidthType.PERCENTAGE },
                        borders: {
                            top: { style: BorderStyle.SINGLE, size: 1, color: "bdc3c7" },
                            bottom: { style: BorderStyle.SINGLE, size: 1, color: "bdc3c7" },
                            left: { style: BorderStyle.SINGLE, size: 1, color: "bdc3c7" },
                            right: { style: BorderStyle.SINGLE, size: 1, color: "bdc3c7" },
                            insideHorizontal: { style: BorderStyle.SINGLE, size: 1, color: "bdc3c7" },
                            insideVertical: { style: BorderStyle.SINGLE, size: 1, color: "bdc3c7" }
                        }
                    })
                );
                
                // وصف النشاط
                children.push(
                    new docx.Paragraph({
                        children: [
                            new docx.TextRun({
                                text: "وصف مختصر لما تم تنفيذه",
                                bold: true,
                                size: 28,
                                font: "Traditional Arabic",
                                color: "2c3e50"
                            })
                        ],
                        alignment: AlignmentType.RIGHT,
                        spacing: { before: 600, after: 300 }
                    }),
                    
                    new docx.Paragraph({
                        children: [
                            new docx.TextRun({
                                text: currentReportData.description,
                                size: 24,
                                font: "Traditional Arabic"
                            })
                        ],
                        alignment: AlignmentType.RIGHT,
                        spacing: { after: 400 }
                    })
                );
                
                // إجراءات التنفيذ
                if (currentReportData.procedures && currentReportData.procedures.length > 0) {
                    children.push(
                        new docx.Paragraph({
                            children: [
                                new docx.TextRun({
                                    text: "إجراءات التنفيذ",
                                    bold: true,
                                    size: 28,
                                    font: "Traditional Arabic",
                                    color: "2c3e50"
                                })
                            ],
                            alignment: AlignmentType.RIGHT,
                            spacing: { before: 400, after: 300 }
                        })
                    );
                    
                    currentReportData.procedures.forEach((procedure, index) => {
                        children.push(
                            new docx.Paragraph({
                                children: [
                                    new docx.TextRun({
                                        text: `${index + 1}. ${procedure}`,
                                        size: 24,
                                        font: "Traditional Arabic"
                                    })
                                ],
                                alignment: AlignmentType.RIGHT,
                                spacing: { after: 150 }
                            })
                        );
                    });
                }
                
                // النتائج
                if (currentReportData.results && currentReportData.results.length > 0) {
                    children.push(
                        new docx.Paragraph({
                            children: [
                                new docx.TextRun({
                                    text: "النتائج",
                                    bold: true,
                                    size: 28,
                                    font: "Traditional Arabic",
                                    color: "2c3e50"
                                })
                            ],
                            alignment: AlignmentType.RIGHT,
                            spacing: { before: 600, after: 300 }
                        })
                    );
                    
                    currentReportData.results.forEach((result, index) => {
                        children.push(
                            new docx.Paragraph({
                                children: [
                                    new docx.TextRun({
                                        text: `${index + 1}. ${result}`,
                                        size: 24,
                                        font: "Traditional Arabic"
                                    })
                                ],
                                alignment: AlignmentType.RIGHT,
                                spacing: { after: 150 }
                            })
                        );
                    });
                }
                
                // التوصيات
                children.push(
                    new docx.Paragraph({
                        children: [
                            new docx.TextRun({
                                text: "التوصيات",
                                bold: true,
                                size: 28,
                                font: "Traditional Arabic",
                                color: "2c3e50"
                            })
                        ],
                        alignment: AlignmentType.RIGHT,
                        spacing: { before: 600, after: 300 }
                    }),
                    
                    new docx.Paragraph({
                        children: [
                            new docx.TextRun({
                                text: currentReportData.recommendations,
                                size: 24,
                                font: "Traditional Arabic"
                            })
                        ],
                        alignment: AlignmentType.RIGHT,
                        spacing: { after: 600 }
                    })
                );
                
                // التوقيعات
                children.push(
                    new docx.Paragraph({
                        children: [
                            new docx.TextRun({
                                text: "التوقيعات",
                                bold: true,
                                size: 28,
                                font: "Traditional Arabic",
                                color: "2c3e50"
                            })
                        ],
                        alignment: AlignmentType.CENTER,
                        spacing: { before: 800, after: 400 }
                    }),
                    
                    new docx.Table({
                        rows: [
                            new TableRow({
                                children: [
                                    new TableCell({
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
                                                alignment: AlignmentType.CENTER
                                            }),
                                            new docx.Paragraph({
                                                children: [
                                                    new docx.TextRun({
                                                        text: currentReportData.principal,
                                                        size: 22,
                                                        font: "Traditional Arabic"
                                                    })
                                                ],
                                                alignment: AlignmentType.CENTER
                                            }),
                                            new docx.Paragraph({
                                                children: [
                                                    new docx.TextRun({
                                                        text: ".........................",
                                                        size: 24,
                                                        font: "Traditional Arabic"
                                                    })
                                                ],
                                                alignment: AlignmentType.CENTER
                                            })
                                        ],
                                        margins: { top: 200, bottom: 200 }
                                    }),
                                    new TableCell({
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
                                                alignment: AlignmentType.CENTER
                                            }),
                                            new docx.Paragraph({
                                                children: [
                                                    new docx.TextRun({
                                                        text: currentReportData.reporter,
                                                        size: 22,
                                                        font: "Traditional Arabic"
                                                    })
                                                ],
                                                alignment: AlignmentType.CENTER
                                            }),
                                            new docx.Paragraph({
                                                children: [
                                                    new docx.TextRun({
                                                        text: ".........................",
                                                        size: 24,
                                                        font: "Traditional Arabic"
                                                    })
                                                ],
                                                alignment: AlignmentType.CENTER
                                            })
                                        ],
                                        margins: { top: 200, bottom: 200 }
                                    })
                                ]
                            })
                        ],
                        width: { size: 100, type: WidthType.PERCENTAGE }
                    })
                );
                
                // تذييل الصفحة
                children.push(
                    new docx.Paragraph({
                        children: [
                            new docx.TextRun({
                                text: `تم إنشاء هذا التقرير بواسطة النظام الإلكتروني لإعداد التقارير التربوية`,
                                size: 18,
                                font: "Traditional Arabic",
                                color: "7f8c8d",
                                italics: true
                            })
                        ],
                        alignment: AlignmentType.CENTER,
                        spacing: { before: 800 }
                    }),
                    
                    new docx.Paragraph({
                        children: [
                            new docx.TextRun({
                                text: `${new Date().toLocaleDateString('ar-SA', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })}`,
                                size: 16,
                                font: "Traditional Arabic",
                                color: "7f8c8d"
                            })
                        ],
                        alignment: AlignmentType.CENTER
                    })
                );
                
                // إنشاء الوثيقة
                const doc = new docx.Document({
                    creator: "النظام الإلكتروني لإعداد التقارير التربوية",
                    title: currentReportData.title,
                    description: "تقرير تربوي - إدارة تعليم مكة المكرمة",
                    sections: [{
                        properties: {
                            page: {
                                margin: {
                                    top: 1417,    // 2.5 سم
                                    right: 1417,  // 2.5 سم (اليمين)
                                    bottom: 1417, // 2.5 سم
                                    left: 1417    // 2.5 سم (اليسار)
                                }
                            }
                        },
                        children: children
                    }]
                });
                
                const buffer = await docx.Packer.toBlob(doc);
                saveAs(buffer, `تقرير_${currentReportData.reportNumber}.docx`);
            }
            
            function printReport() {
                const printWindow = window.open('', '_blank');
                const printHTML = generatePrintHTML();
                printWindow.document.write(printHTML);
                printWindow.document.close();
                
                setTimeout(() => {
                    printWindow.print();
                    setTimeout(() => {
                        printWindow.close();
                    }, 1000);
                }, 500);
            }
            
            function exportToHTML() {
                const htmlContent = generateProfessionalHTML();
                const blob = new Blob([htmlContent], { type: 'text/html;charset=utf-8' });
                saveAs(blob, `تقرير_${currentReportData.reportNumber}.html`);
            }
            
            function generatePrintHTML() {
                return `
<!DOCTYPE html>
<html dir="rtl" lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>${currentReportData.title} - طباعة</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700;800&display=swap');
        
        * { margin: 0; padding: 0; box-sizing: border-box; }
        
        body {
            font-family: 'Cairo', 'Traditional Arabic', sans-serif;
            line-height: 1.8;
            color: #000;
            direction: rtl;
            background: white;
            padding: 20mm;
            font-size: 14pt;
        }
        
        .print-container {
            width: 100%;
            max-width: 210mm;
            margin: 0 auto;
        }
        
        .print-header {
            text-align: center;
            margin-bottom: 30px;
            border-bottom: 3px solid #2c3e50;
            padding-bottom: 20px;
        }
        
        .print-title {
            color: #2c3e50;
            font-size: 24pt;
            margin-bottom: 15px;
            font-weight: 800;
        }
        
        .print-subtitle {
            color: #e74c3c;
            font-size: 18pt;
            margin-bottom: 10px;
            font-weight: 600;
        }
        
        .print-info {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 8px;
            margin: 20px 0;
            border-right: 4px solid #2c3e50;
        }
        
        .print-section {
            margin: 30px 0;
            page-break-inside: avoid;
        }
        
        .print-section-title {
            color: #2c3e50;
            font-size: 20pt;
            margin-bottom: 20px;
            border-right: 4px solid #e74c3c;
            padding-right: 15px;
            font-weight: 700;
        }
        
        .print-content {
            font-size: 14pt;
            line-height: 1.8;
            text-align: justify;
        }
        
        .print-table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
            font-size: 12pt;
        }
        
        .print-table th {
            background-color: #2c3e50;
            color: white;
            padding: 12px;
            text-align: right;
            font-weight: bold;
            border: 1px solid #1a252f;
        }
        
        .print-table td {
            padding: 10px 12px;
            border: 1px solid #bdc3c7;
            text-align: right;
        }
        
        .print-table tr:nth-child(even) {
            background-color: #f8f9fa;
        }
        
        .print-list {
            padding-right: 25px;
            margin: 15px 0;
        }
        
        .print-list-item {
            margin-bottom: 10px;
            padding-right: 15px;
            position: relative;
        }
        
        .print-list-item::before {
            content: "•";
            color: #e74c3c;
            font-size: 20pt;
            position: absolute;
            right: -20px;
        }
        
        .print-signatures {
            display: flex;
            justify-content: space-around;
            margin-top: 80px;
            padding-top: 40px;
            border-top: 2px solid #2c3e50;
            flex-wrap: wrap;
            page-break-inside: avoid;
        }
        
        .print-signature {
            text-align: center;
            min-width: 250px;
            margin-bottom: 30px;
        }
        
        .print-signature-title {
            font-size: 16pt;
            font-weight: bold;
            margin-bottom: 20px;
            color: #2c3e50;
        }
        
        .print-signature-name {
            font-size: 14pt;
            margin: 25px 0;
            font-weight: 600;
        }
        
        .print-signature-line {
            width: 200px;
            height: 1px;
            background: #333;
            margin: 30px auto;
            border-top: 2px solid #333;
        }
        
        .print-footer {
            text-align: center;
            margin-top: 50px;
            padding-top: 30px;
            border-top: 1px dashed #bdc3c7;
            color: #7f8c8d;
            font-size: 11pt;
        }
        
        @page {
            size: A4;
            margin: 20mm;
        }
        
        @media print {
            body {
                padding: 0;
            }
            
            .print-container {
                width: 100%;
                margin: 0;
            }
        }
    </style>
</head>
<body>
    <div class="print-container">
        <div class="print-header">
            <h1 class="print-title">إدارة تعليم منطقة مكة المكرمة</h1>
            <div class="print-subtitle">مكتب التعليم بوسط مكة</div>
            <h2 style="color: #2c3e50; font-size: 22pt; margin: 20px 0;">${currentReportData.title}</h2>
            <div class="print-info">
                <strong>رقم التقرير:</strong> ${currentReportData.reportNumber} | 
                <strong>تاريخ البرنامج:</strong> ${currentReportData.programDate} هـ
            </div>
        </div>
        
        <div class="print-section">
            <h3 class="print-section-title">البيانات الأساسية</h3>
            <table class="print-table">
                ${[
                    { label: 'المدرسة', value: currentReportData.school },
                    { label: 'مدير المدرسة', value: currentReportData.principal },
                    { label: 'معد التقرير', value: currentReportData.reporter },
                    { label: 'مكان التنفيذ', value: currentReportData.location },
                    { label: 'المستهدفون', value: currentReportData.target },
                    { label: 'عدد المستفيدين', value: currentReportData.beneficiaries },
                    { label: 'تابع للمناهج', value: currentReportData.curriculumRelated }
                ].map(item => `
                <tr>
                    <td>${item.value}</td>
                    <th>${item.label}</th>
                </tr>
                `).join('')}
            </table>
        </div>
        
        <div class="print-section">
            <h3 class="print-section-title">وصف مختصر لما تم تنفيذه</h3>
            <div class="print-content">
                <p>${currentReportData.description}</p>
            </div>
        </div>
        
        ${currentReportData.procedures && currentReportData.procedures.length > 0 ? `
        <div class="print-section">
            <h3 class="print-section-title">إجراءات التنفيذ</h3>
            <div class="print-list">
                ${currentReportData.procedures.map((procedure, index) => `
                <div class="print-list-item">${procedure}</div>
                `).join('')}
            </div>
        </div>` : ''}
        
        ${currentReportData.results && currentReportData.results.length > 0 ? `
        <div class="print-section">
            <h3 class="print-section-title">النتائج</h3>
            <div class="print-list">
                ${currentReportData.results.map((result, index) => `
                <div class="print-list-item">${result}</div>
                `).join('')}
            </div>
        </div>` : ''}
        
        <div class="print-section">
            <h3 class="print-section-title">التوصيات</h3>
            <div class="print-content">
                <p>${currentReportData.recommendations}</p>
            </div>
        </div>
        
        <div class="print-signatures">
            <div class="print-signature">
                <div class="print-signature-title">مدير المدرسة</div>
                <div class="print-signature-name">${currentReportData.principal}</div>
                <div class="print-signature-line"></div>
                <div>التوقيع</div>
            </div>
            <div class="print-signature">
                <div class="print-signature-title">معد التقرير</div>
                <div class="print-signature-name">${currentReportData.reporter}</div>
                <div class="print-signature-line"></div>
                <div>التوقيع</div>
            </div>
        </div>
        
        <div class="print-footer">
            <p>تم إنشاء هذا التقرير بواسطة النظام الإلكتروني لإعداد التقارير التربوية</p>
            <p>${new Date().toLocaleDateString('ar-SA', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })}</p>
        </div>
    </div>
</body>
</html>`;
            }
            
            function generateProfessionalHTML() {
                const currentDate = new Date().toLocaleDateString('ar-SA', {
                    weekday: 'long',
                    year: 'numeric',
                    month: 'long',
                    day: 'numeric'
                });
                
                return `<!DOCTYPE html>
<html dir="rtl" lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>${currentReportData.title}</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700;800&display=swap');
        
        * { margin: 0; padding: 0; box-sizing: border-box; }
        
        body {
            font-family: 'Cairo', sans-serif;
            line-height: 1.8; color: #333;
            background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
            min-height: 100vh; padding: 40px 20px; direction: rtl;
        }
        
        .report-container {
            max-width: 1000px; margin: 0 auto; background: white; padding: 50px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.15); border-radius: 12px;
            position: relative; overflow: hidden; border: 1px solid rgba(255,255,255,0.3);
        }
        
        .report-container::before {
            content: ''; position: absolute; top: 0; right: 0; width: 100%; height: 8px;
            background: linear-gradient(90deg, #2c3e50 0%, #3498db 100%);
        }
        
        .header { text-align: center; margin-bottom: 60px; position: relative; padding-bottom: 30px; }
        .header::after {
            content: ''; position: absolute; bottom: 0; right: 50%; transform: translateX(50%);
            width: 200px; height: 4px; background: linear-gradient(90deg, #2c3e50 0%, #e74c3c 100%); border-radius: 2px;
        }
        
        h1 { color: #2c3e50; font-size: 36px; margin-bottom: 15px; font-weight: 800; }
        h2 { color: #e74c3c; font-size: 24px; margin-bottom: 10px; font-weight: 600; }
        
        .report-info { display: flex; justify-content: center; gap: 30px; margin-top: 25px; flex-wrap: wrap; }
        .info-item {
            background: #f8f9fa; padding: 15px 25px; border-radius: 8px; font-size: 16px;
            display: flex; align-items: center; gap: 10px; box-shadow: 0 4px 12px rgba(0,0,0,0.08);
            border-right: 3px solid #3498db;
        }
        
        .section {
            margin-bottom: 50px; padding: 30px; background: #f8f9fa; border-radius: 12px;
            border-right: 5px solid #2c3e50; box-shadow: 0 6px 20px rgba(0,0,0,0.05);
            position: relative; overflow: hidden;
        }
        
        .section-title {
            color: #2c3e50; font-size: 28px; margin-bottom: 25px; font-weight: 700;
            display: flex; align-items: center; gap: 15px;
        }
        
        .basic-info-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 25px; margin-bottom: 30px; }
        .info-card {
            background: white; padding: 25px; border-radius: 10px; box-shadow: 0 4px 15px rgba(0,0,0,0.05);
            border: 1px solid #e9ecef; transition: transform 0.3s ease;
        }
        .info-card:hover { transform: translateY(-5px); box-shadow: 0 8px 25px rgba(0,0,0,0.1); }
        
        .info-label {
            color: #2c3e50; font-weight: 600; font-size: 16px; margin-bottom: 10px;
            display: flex; align-items: center; gap: 10px;
        }
        .info-value { color: #333; font-size: 18px; font-weight: 500; padding-right: 10px; }
        
        .content-box {
            background: white; padding: 25px; border-radius: 10px; margin-bottom: 20px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05); border: 1px solid #e9ecef;
        }
        .content-box p { font-size: 18px; line-height: 1.8; color: #444; text-align: justify; }
        
        .list-container { padding-right: 20px; }
        .list-item {
            display: flex; align-items: flex-start; gap: 15px; margin-bottom: 15px; padding: 15px;
            background: white; border-radius: 8px; border-right: 4px solid #3498db;
            box-shadow: 0 3px 10px rgba(0,0,0,0.05);
        }
        
        .list-number {
            background: #2c3e50; color: white; width: 35px; height: 35px; border-radius: 50%;
            display: flex; align-items: center; justify-content: center; font-weight: bold; font-size: 16px; flex-shrink: 0;
        }
        .list-text { font-size: 16px; color: #444; flex: 1; }
        
        .signatures {
            display: flex; justify-content: space-around; margin-top: 80px; padding-top: 40px;
            border-top: 3px solid #2c3e50; flex-wrap: wrap; gap: 40px;
        }
        .signature-box {
            text-align: center; width: 300px; padding: 30px; background: #f8f9fa;
            border-radius: 12px; box-shadow: 0 8px 25px rgba(0,0,0,0.08); position: relative;
        }
        .signature-title { color: #2c3e50; font-size: 22px; font-weight: 700; margin-bottom: 15px; }
        .signature-name { font-size: 20px; color: #333; margin-bottom: 30px; font-weight: 600; }
        .signature-line { width: 200px; height: 2px; background: #333; margin: 30px auto 15px; border-top: 2px dashed #333; }
        
        .footer {
            text-align: center; margin-top: 60px; padding-top: 30px; border-top: 2px dashed #bdc3c7;
            color: #7f8c8d; font-size: 16px;
        }
        
        @media (max-width: 768px) {
            .report-container { padding: 30px 20px; }
            h1 { font-size: 28px; } h2 { font-size: 20px; }
            .section-title { font-size: 24px; }
            .basic-info-grid { grid-template-columns: 1fr; }
            .signatures { flex-direction: column; align-items: center; }
            .signature-box { width: 100%; max-width: 300px; }
            .info-item { padding: 12px 20px; font-size: 14px; }
        }
    </style>
</head>
<body>
    <div class="report-container">
        <div class="header">
            <h1>إدارة تعليم منطقة مكة المكرمة</h1>
            <h2>${currentReportData.title}</h2>
            
            <div class="report-info">
                <div class="info-item"><i class="fas fa-hashtag"></i><span>رقم التقرير: ${currentReportData.reportNumber}</span></div>
                <div class="info-item"><i class="fas fa-calendar"></i><span>تاريخ البرنامج: ${currentReportData.programDate} هـ</span></div>
            </div>
        </div>
        
        <div class="section">
            <h3 class="section-title"><i class="fas fa-database"></i>البيانات الأساسية</h3>
            <div class="basic-info-grid">
                <div class="info-card"><div class="info-label"><i class="fas fa-school"></i>المدرسة</div><div class="info-value">${currentReportData.school}</div></div>
                <div class="info-card"><div class="info-label"><i class="fas fa-user-tie"></i>مدير المدرسة</div><div class="info-value">${currentReportData.principal}</div></div>
                <div class="info-card"><div class="info-label"><i class="fas fa-user-edit"></i>معد التقرير</div><div class="info-value">${currentReportData.reporter}</div></div>
                <div class="info-card"><div class="info-label"><i class="fas fa-map-marker"></i>مكان التنفيذ</div><div class="info-value">${currentReportData.location}</div></div>
                <div class="info-card"><div class="info-label"><i class="fas fa-users"></i>المستهدفون</div><div class="info-value">${currentReportData.target}</div></div>
                <div class="info-card"><div class="info-label"><i class="fas fa-user-check"></i>عدد المستفيدين</div><div class="info-value">${currentReportData.beneficiaries}</div></div>
                <div class="info-card"><div class="info-label"><i class="fas fa-book"></i>تابع للمناهج</div><div class="info-value">${currentReportData.curriculumRelated}</div></div>
            </div>
        </div>
        
        <div class="section">
            <h3 class="section-title"><i class="fas fa-clipboard-list"></i>وصف مختصر لما تم تنفيذه</h3>
            <div class="content-box"><p>${currentReportData.description}</p></div>
        </div>
        
        ${currentReportData.procedures && currentReportData.procedures.length > 0 ? `
        <div class="section">
            <h3 class="section-title"><i class="fas fa-tasks"></i>إجراءات التنفيذ</h3>
            <div class="list-container">
                ${currentReportData.procedures.map((procedure, index) => `
                <div class="list-item"><div class="list-number">${index + 1}</div><div class="list-text">${procedure}</div></div>
                `).join('')}
            </div>
        </div>` : ''}
        
        ${currentReportData.results && currentReportData.results.length > 0 ? `
        <div class="section">
            <h3 class="section-title"><i class="fas fa-chart-line"></i>النتائج</h3>
            <div class="list-container">
                ${currentReportData.results.map((result, index) => `
                <div class="list-item"><div class="list-number">${index + 1}</div><div class="list-text">${result}</div></div>
                `).join('')}
            </div>
        </div>` : ''}
        
        <div class="section">
            <h3 class="section-title"><i class="fas fa-lightbulb"></i>التوصيات</h3>
            <div class="content-box"><p>${currentReportData.recommendations}</p></div>
        </div>
        
        <div class="signatures">
            <div class="signature-box">
                <div class="signature-title">مدير المدرسة</div>
                <div class="signature-name">${currentReportData.principal}</div>
                <div class="signature-line"></div>
                <div>التوقيع</div>
            </div>
            <div class="signature-box">
                <div class="signature-title">معد التقرير</div>
                <div class="signature-name">${currentReportData.reporter}</div>
                <div class="signature-line"></div>
                <div>التوقيع</div>
            </div>
        </div>
        
        <div class="footer">
            <p>تم إنشاء هذا التقرير بواسطة النظام الإلكتروني لإعداد التقارير التربوية</p>
            <p>${currentDate}</p>
        </div>
    </div>
</body>
</html>`;
            }
            
            function generatePreviewHTML(reportData) {
                return `<!DOCTYPE html>
<html dir="rtl" lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>معاينة: ${reportData.title}</title>
    <style>
        body { font-family: 'Cairo', sans-serif; direction: rtl; padding: 20px; background: #f5f5f5; }
        .report { background: white; padding: 40px; max-width: 1000px; margin: 0 auto; box-shadow: 0 0 20px rgba(0,0,0,0.1); border-radius: 10px; }
        .header { text-align: center; border-bottom: 3px solid #2c3e50; padding-bottom: 20px; margin-bottom: 30px; }
        h1 { color: #2c3e50; margin-bottom: 10px; }
        .info-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 15px; margin: 20px 0; }
        .info-item { background: #f8f9fa; padding: 15px; border-radius: 8px; border-right: 4px solid #2c3e50; }
        .info-label { color: #2c3e50; font-weight: bold; }
        .section { margin: 30px 0; padding: 20px; background: #f8f9fa; border-radius: 8px; }
        .section h3 { color: #2c3e50; border-bottom: 2px solid #2c3e50; padding-bottom: 10px; margin-bottom: 15px; }
        .signatures { display: flex; justify-content: space-around; margin-top: 50px; padding-top: 30px; border-top: 2px solid #2c3e50; }
        .signature { text-align: center; }
        @media print { body { padding: 0; } .report { box-shadow: none; } }
    </style>
</head>
<body>
    <div class="report">
        <div class="header">
            <h1>${reportData.title}</h1>
            <div>إدارة تعليم منطقة مكة المكرمة</div>
            <div style="margin-top: 15px; color: #666;">
                <strong>رقم التقرير:</strong> ${reportData.reportNumber} | 
                <strong>تاريخ البرنامج:</strong> ${reportData.programDate}
            </div>
        </div>
        
        <div class="info-grid">
            <div class="info-item"><span class="info-label">المدرسة:</span><br>${reportData.school}</div>
            <div class="info-item"><span class="info-label">مدير المدرسة:</span><br>${reportData.principal}</div>
            <div class="info-item"><span class="info-label">معد التقرير:</span><br>${reportData.reporter}</div>
            <div class="info-item"><span class="info-label">مكان التنفيذ:</span><br>${reportData.location}</div>
            <div class="info-item"><span class="info-label">المستهدفون:</span><br>${reportData.target}</div>
            <div class="info-item"><span class="info-label">عدد المستفيدين:</span><br>${reportData.beneficiaries}</div>
            <div class="info-item"><span class="info-label">تابع للمناهج:</span><br>${reportData.curriculumRelated}</div>
        </div>
        
        <div class="section">
            <h3>وصف مختصر لما تم تنفيذه</h3>
            <p>${reportData.description}</p>
        </div>
        
        ${reportData.procedures && reportData.procedures.length > 0 ? `
        <div class="section">
            <h3>إجراءات التنفيذ</h3>
            <ol>${reportData.procedures.map(p => `<li>${p}</li>`).join('')}</ol>
        </div>` : ''}
        
        ${reportData.results && reportData.results.length > 0 ? `
        <div class="section">
            <h3>النتائج</h3>
            <ul>${reportData.results.map(r => `<li>${r}</li>`).join('')}</ul>
        </div>` : ''}
        
        <div class="section">
            <h3>التوصيات</h3>
            <p>${reportData.recommendations}</p>
        </div>
        
        <div class="signatures">
            <div class="signature">
                <div style="font-weight: bold; margin-bottom: 10px;">مدير المدرسة</div>
                <div>${reportData.principal}</div>
                <div style="margin-top: 20px; border-top: 1px solid #000; width: 150px; margin: 20px auto 0; padding-top: 5px;">التوقيع</div>
            </div>
            <div class="signature">
                <div style="font-weight: bold; margin-bottom: 10px;">معد التقرير</div>
                <div>${reportData.reporter}</div>
                <div style="margin-top: 20px; border-top: 1px solid #000; width: 150px; margin: 20px auto 0; padding-top: 5px;">التوقيع</div>
            </div>
        </div>
        
        <div style="text-align: center; margin-top: 50px; color: #666; font-size: 14px; border-top: 1px dashed #ddd; padding-top: 20px;">
            تم إنشاء هذا التقرير بواسطة النظام الإلكتروني لإعداد التقارير التربوية - ${new Date().toLocaleDateString('ar-SA')}
        </div>
    </div>
</body>
</html>`;
            }
            
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
            
            function generateReportNumber() {
                const prefix = 'TRB';
                const year = new Date().getFullYear();
                const month = (new Date().getMonth() + 1).toString().padStart(2, '0');
                const random = Math.floor(Math.random() * 10000).toString().padStart(4, '0');
                return `${prefix}-${year}${month}-${random}`;
            }
            
            function resetForm() {
                document.getElementById('programDate').value = '1447-06-12';
                document.getElementById('location').value = '';
                document.getElementById('target').value = '';
                document.getElementById('beneficiaries').value = '30';
                document.getElementById('description').value = '';
                document.getElementById('procedures').value = '';
                document.getElementById('results').value = '';
                document.getElementById('recommendations').value = '';
                
                uploadedImages = [];
                imagePreview.innerHTML = '';
                
                localStorage.removeItem('reportDraft');
                
                window.scrollTo({ top: 0, behavior: 'smooth' });
            }
            
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
            
            setupEventListeners();
            loadInitialData();
            
            // الحفظ التلقائي كل 30 ثانية
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