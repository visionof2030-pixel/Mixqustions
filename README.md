<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>لوحة تحكم الإدارة - ناصر AI</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        html, body {
            font-family: 'Cairo', sans-serif;
            background: linear-gradient(135deg, #0a1929 0%, #132f4c 100%);
            color: #ffffff;
            direction: rtl;
            height: 100%;
            overflow-x: hidden;
            -webkit-text-size-adjust: 100%;
            -moz-text-size-adjust: 100%;
            -ms-text-size-adjust: 100%;
            text-size-adjust: 100%;
            touch-action: manipulation;
        }

        /* منع التكبير التلقائي */
        input, select, textarea {
            font-size: 16px !important;
            max-height: 44px;
        }

        @media screen and (max-width: 768px) {
            input, select, textarea {
                font-size: 16px !important;
            }
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        /* الهيدر */
        .header {
            background: linear-gradient(135deg, #022e22 0%, #044a35 100%);
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 30px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.1);
            position: relative;
            overflow: hidden;
        }

        .header::before {
            content: '';
            position: absolute;
            top: 0;
            right: 0;
            width: 200px;
            height: 200px;
            background: linear-gradient(45deg, rgba(255, 209, 102, 0.1), transparent);
            border-radius: 50%;
        }

        .header h1 {
            font-size: 28px;
            font-weight: 900;
            margin-bottom: 10px;
            color: #ffd166;
            text-shadow: 0 2px 10px rgba(255, 209, 102, 0.3);
        }

        .header p {
            font-size: 14px;
            opacity: 0.9;
        }

        .header-stats {
            display: flex;
            gap: 20px;
            margin-top: 20px;
            flex-wrap: wrap;
        }

        .stat-box {
            background: rgba(255, 255, 255, 0.1);
            padding: 15px;
            border-radius: 10px;
            flex: 1;
            min-width: 150px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .stat-box .stat-value {
            font-size: 24px;
            font-weight: 700;
            color: #4d96ff;
        }

        .stat-box .stat-label {
            font-size: 12px;
            opacity: 0.8;
            margin-top: 5px;
        }

        /* التنقل */
        .tabs {
            display: flex;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 12px;
            padding: 5px;
            margin-bottom: 30px;
            overflow-x: auto;
            -webkit-overflow-scrolling: touch;
        }

        .tab {
            flex: 1;
            padding: 15px;
            text-align: center;
            cursor: pointer;
            border-radius: 8px;
            transition: all 0.3s;
            white-space: nowrap;
            min-width: 120px;
        }

        .tab:hover {
            background: rgba(255, 255, 255, 0.1);
        }

        .tab.active {
            background: linear-gradient(135deg, #066d4d 0%, #044a35 100%);
            box-shadow: 0 4px 15px rgba(6, 109, 77, 0.3);
        }

        .tab i {
            margin-left: 8px;
            font-size: 18px;
        }

        /* المحتوى */
        .content {
            display: none;
        }

        .content.active {
            display: block;
            animation: fadeIn 0.5s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* الكروت */
        .card {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 25px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);
            backdrop-filter: blur(10px);
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }

        .card-title {
            font-size: 20px;
            font-weight: 700;
            color: #ffd166;
        }

        .card-subtitle {
            font-size: 14px;
            opacity: 0.8;
            margin-top: 5px;
        }

        /* الأزرار */
        .btn {
            background: linear-gradient(135deg, #066d4d 0%, #044a35 100%);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 10px;
            font-size: 14px;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            min-height: 44px;
            width: 100%;
            margin-bottom: 10px;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(6, 109, 77, 0.4);
        }

        .btn:active {
            transform: translateY(0);
        }

        .btn-secondary {
            background: linear-gradient(135deg, #5a67d8 0%, #4c51bf 100%);
        }

        .btn-danger {
            background: linear-gradient(135deg, #d9534f 0%, #c9302c 100%);
        }

        .btn-success {
            background: linear-gradient(135deg, #25D366 0%, #128C7E 100%);
        }

        .btn-warning {
            background: linear-gradient(135deg, #ffd166 0%, #f0ad4e 100%);
        }

        .btn-small {
            padding: 8px 15px;
            font-size: 12px;
            min-height: 36px;
            width: auto;
        }

        /* نموذج الإدخال */
        .form-group {
            margin-bottom: 20px;
        }

        .form-label {
            display: block;
            font-size: 14px;
            font-weight: 600;
            margin-bottom: 8px;
            color: #4d96ff;
        }

        .form-control {
            width: 100%;
            padding: 12px 15px;
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 10px;
            color: white;
            font-size: 16px;
            transition: all 0.3s;
            min-height: 44px;
        }

        .form-control:focus {
            outline: none;
            border-color: #4d96ff;
            box-shadow: 0 0 0 3px rgba(77, 150, 255, 0.2);
        }

        .form-control::placeholder {
            color: rgba(255, 255, 255, 0.5);
        }

        select.form-control {
            appearance: none;
            background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' fill='white' viewBox='0 0 16 16'%3E%3Cpath d='M7.247 11.14 2.451 5.658C1.885 5.013 2.345 4 3.204 4h9.592a1 1 0 0 1 .753 1.659l-4.796 5.48a1 1 0 0 1-1.506 0z'/%3E%3C/svg%3E");
            background-repeat: no-repeat;
            background-position: left 15px center;
            background-size: 12px;
            padding-left: 40px;
        }

        .form-row {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }

        /* الجدول */
        .table-container {
            overflow-x: auto;
            -webkit-overflow-scrolling: touch;
            border-radius: 10px;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        table {
            width: 100%;
            border-collapse: collapse;
            min-width: 600px;
        }

        th {
            background: rgba(255, 255, 255, 0.1);
            padding: 15px;
            text-align: right;
            font-weight: 600;
            color: #ffd166;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }

        td {
            padding: 15px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.05);
        }

        tr:hover {
            background: rgba(255, 255, 255, 0.02);
        }

        .badge {
            display: inline-block;
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 600;
        }

        .badge-success {
            background: rgba(37, 211, 102, 0.2);
            color: #25D366;
        }

        .badge-warning {
            background: rgba(255, 209, 102, 0.2);
            color: #ffd166;
        }

        .badge-danger {
            background: rgba(217, 83, 79, 0.2);
            color: #d9534f;
        }

        .badge-info {
            background: rgba(77, 150, 255, 0.2);
            color: #4d96ff;
        }

        /* الإشعارات */
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            left: 20px;
            background: linear-gradient(135deg, #066d4d 0%, #044a35 100%);
            color: white;
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
            z-index: 1000;
            display: flex;
            align-items: center;
            justify-content: space-between;
            transform: translateX(150%);
            transition: transform 0.4s cubic-bezier(0.68, -0.55, 0.27, 1.55);
            max-width: 500px;
            margin: 0 auto;
        }

        .notification.show {
            transform: translateX(0);
        }

        .notification-content {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .notification-close {
            background: none;
            border: none;
            color: white;
            cursor: pointer;
            font-size: 18px;
            padding: 0;
            width: 30px;
            height: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 50%;
            transition: background 0.3s;
        }

        .notification-close:hover {
            background: rgba(255, 255, 255, 0.1);
        }

        /* تحسينات للهواتف */
        @media (max-width: 768px) {
            .container {
                padding: 15px;
            }

            .header h1 {
                font-size: 24px;
            }

            .header-stats {
                gap: 10px;
            }

            .stat-box {
                min-width: calc(50% - 5px);
                padding: 12px;
            }

            .stat-box .stat-value {
                font-size: 20px;
            }

            .tabs {
                flex-wrap: nowrap;
                overflow-x: auto;
                padding: 3px;
            }

            .tab {
                min-width: 100px;
                padding: 12px 8px;
                font-size: 13px;
            }

            .card {
                padding: 20px;
            }

            .card-title {
                font-size: 18px;
            }

            .form-row {
                grid-template-columns: 1fr;
                gap: 10px;
            }

            .btn {
                padding: 10px 20px;
                font-size: 13px;
            }

            th, td {
                padding: 12px 8px;
                font-size: 13px;
            }

            .badge {
                padding: 3px 8px;
                font-size: 11px;
            }
        }

        @media (max-width: 480px) {
            .container {
                padding: 10px;
            }

            .header {
                padding: 15px;
            }

            .header h1 {
                font-size: 20px;
            }

            .stat-box {
                min-width: 100%;
            }

            .tab {
                min-width: 90px;
                padding: 10px 5px;
                font-size: 12px;
            }

            .card {
                padding: 15px;
            }

            .notification {
                top: 10px;
                right: 10px;
                left: 10px;
                padding: 12px;
            }
        }

        /* إصلاحات للـ Web in App */
        @supports (padding-bottom: env(safe-area-inset-bottom)) {
            .container {
                padding-bottom: env(safe-area-inset-bottom);
            }
        }

        /* تخصيص شريط التمرير */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }

        ::-webkit-scrollbar-track {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 4px;
        }

        ::-webkit-scrollbar-thumb {
            background: rgba(255, 255, 255, 0.2);
            border-radius: 4px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: rgba(255, 255, 255, 0.3);
        }

        /* تأثيرات التحميل */
        .loading {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top-color: #4d96ff;
            animation: spin 1s ease-in-out infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        /* علامات المدة الزمنية */
        .duration-tags {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-top: 10px;
        }

        .duration-tag {
            background: rgba(77, 150, 255, 0.1);
            border: 1px solid rgba(77, 150, 255, 0.3);
            padding: 6px 12px;
            border-radius: 20px;
            font-size: 12px;
            cursor: pointer;
            transition: all 0.3s;
        }

        .duration-tag:hover {
            background: rgba(77, 150, 255, 0.2);
        }

        .duration-tag.active {
            background: linear-gradient(135deg, #4d96ff 0%, #2d7dfd 100%);
            color: white;
            border-color: #4d96ff;
        }

        /* شريط البحث */
        .search-box {
            position: relative;
            margin-bottom: 20px;
        }

        .search-box input {
            width: 100%;
            padding: 12px 45px 12px 15px;
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 10px;
            color: white;
            font-size: 16px;
        }

        .search-box i {
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: rgba(255, 255, 255, 0.5);
        }

        /* فلاتر */
        .filters {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .filter-select {
            flex: 1;
            min-width: 150px;
        }

        /* تفاصيل المستخدم */
        .user-details {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 10px;
            padding: 20px;
            margin-top: 20px;
        }

        .user-detail {
            display: flex;
            justify-content: space-between;
            padding: 10px 0;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }

        .user-detail:last-child {
            border-bottom: none;
        }

        .user-detail-label {
            font-weight: 600;
            color: #ffd166;
        }

        .user-detail-value {
            text-align: left;
        }

        /* إحصائيات متقدمة */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }

        .stat-item {
            background: rgba(255, 255, 255, 0.05);
            padding: 15px;
            border-radius: 10px;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .stat-item-value {
            font-size: 28px;
            font-weight: 700;
            color: #4d96ff;
            margin-bottom: 5px;
        }

        .stat-item-label {
            font-size: 12px;
            opacity: 0.8;
        }

        /* تحسينات للوضع الليلي */
        @media (prefers-color-scheme: light) {
            body {
                background: linear-gradient(135deg, #f0f9f6 0%, #e8f4f0 100%);
                color: #044a35;
            }

            .card, .stat-box, .table-container {
                background: rgba(255, 255, 255, 0.9);
                border-color: rgba(4, 74, 53, 0.1);
            }

            .form-control {
                background: white;
                border-color: #d4ebe2;
                color: #044a35;
            }

            .form-control::placeholder {
                color: #666;
            }

            th {
                color: #066d4d;
                background: rgba(6, 109, 77, 0.1);
            }

            .notification {
                background: linear-gradient(135deg, #066d4d 0%, #044a35 100%);
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- الهيدر -->
        <div class="header">
            <h1><i class="fas fa-user-shield"></i> لوحة تحكم الإدارة - ناصر AI</h1>
            <p>إدارة النظام وتوليد أكواد التفعيل والتحكم بالمستخدمين</p>
            
            <div class="header-stats">
                <div class="stat-box">
                    <div class="stat-value" id="totalCodes">0</div>
                    <div class="stat-label">الأكواد النشطة</div>
                </div>
                <div class="stat-box">
                    <div class="stat-value" id="activeUsers">0</div>
                    <div class="stat-label">المستخدمين النشطين</div>
                </div>
                <div class="stat-box">
                    <div class="stat-value" id="totalRevenue">0 ر.س</div>
                    <div class="stat-label">إجمالي الإيرادات</div>
                </div>
                <div class="stat-box">
                    <div class="stat-value" id="todayCodes">0</div>
                    <div class="stat-label">أكواد اليوم</div>
                </div>
            </div>
        </div>

        <!-- أشرطة التنقل -->
        <div class="tabs">
            <div class="tab active" onclick="showTab('generate')">
                <i class="fas fa-key"></i>
                <span>توليد أكواد</span>
            </div>
            <div class="tab" onclick="showTab('codes')">
                <i class="fas fa-list"></i>
                <span>الأكواد النشطة</span>
            </div>
            <div class="tab" onclick="showTab('users')">
                <i class="fas fa-users"></i>
                <span>المستخدمين</span>
            </div>
            <div class="tab" onclick="showTab('reports')">
                <i class="fas fa-chart-bar"></i>
                <span>التقارير</span>
            </div>
            <div class="tab" onclick="showTab('settings')">
                <i class="fas fa-cog"></i>
                <span>الإعدادات</span>
            </div>
        </div>

        <!-- محتوى التبويب: توليد أكواد -->
        <div id="generate" class="content active">
            <div class="card">
                <div class="card-header">
                    <div>
                        <div class="card-title">توليد كود تفعيل جديد</div>
                        <div class="card-subtitle">اختر المدة الزمنية وانقر على توليد</div>
                    </div>
                    <i class="fas fa-key fa-2x" style="color: #ffd166;"></i>
                </div>

                <div class="form-group">
                    <label class="form-label">مدة التفعيل</label>
                    <div class="duration-tags" id="durationTags">
                        <span class="duration-tag" data-duration="5m">5 دقائق</span>
                        <span class="duration-tag" data-duration="30m">30 دقيقة</span>
                        <span class="duration-tag" data-duration="1h">1 ساعة</span>
                        <span class="duration-tag" data-duration="3h">3 ساعات</span>
                        <span class="duration-tag active" data-duration="1d">1 يوم</span>
                        <span class="duration-tag" data-duration="3d">3 أيام</span>
                        <span class="duration-tag" data-duration="7d">أسبوع</span>
                        <span class="duration-tag" data-duration="30d">شهر</span>
                        <span class="duration-tag" data-duration="90d">3 أشهر</span>
                        <span class="duration-tag" data-duration="150d">5 أشهر</span>
                    </div>
                </div>

                <div class="form-group">
                    <label class="form-label">عدد الأكواد</label>
                    <select class="form-control" id="codeCount">
                        <option value="1">1 كود</option>
                        <option value="5">5 أكواد</option>
                        <option value="10">10 أكواد</option>
                        <option value="20">20 كود</option>
                        <option value="50">50 كود</option>
                    </select>
                </div>

                <div class="form-group">
                    <label class="form-label">كود الأمان (ADMIN_TOKEN)</label>
                    <input type="password" class="form-control" id="adminToken" placeholder="أدخل كود الأمان">
                </div>

                <div class="form-group">
                    <label class="form-label">السعر (اختياري)</label>
                    <input type="number" class="form-control" id="price" placeholder="أدخل السعر بالريال">
                </div>

                <button class="btn btn-success" onclick="generateCodes()">
                    <i class="fas fa-bolt"></i>
                    توليد الأكواد
                </button>
            </div>

            <div class="card" id="generatedCodesCard" style="display: none;">
                <div class="card-header">
                    <div>
                        <div class="card-title">الأكواد المولدة</div>
                        <div class="card-subtitle">انسخ الأكواد أو أرسلها مباشرة</div>
                    </div>
                    <i class="fas fa-copy fa-2x" style="color: #4d96ff;"></i>
                </div>

                <div class="form-group">
                    <label class="form-label">الأكواد المولدة:</label>
                    <textarea class="form-control" id="generatedCodes" rows="6" readonly style="font-family: monospace;"></textarea>
                </div>

                <div class="form-row">
                    <button class="btn btn-secondary" onclick="copyCodes()">
                        <i class="fas fa-copy"></i>
                        نسخ الأكواد
                    </button>
                    <button class="btn btn-warning" onclick="shareCodes()">
                        <i class="fas fa-share-alt"></i>
                        مشاركة
                    </button>
                </div>
            </div>
        </div>

        <!-- محتوى التبويب: الأكواد النشطة -->
        <div id="codes" class="content">
            <div class="card">
                <div class="card-header">
                    <div>
                        <div class="card-title">الأكواد النشطة</div>
                        <div class="card-subtitle">إدارة وتتبع جميع أكواد التفعيل</div>
                    </div>
                    <div class="search-box">
                        <input type="text" id="searchCodes" placeholder="ابحث في الأكواد..." oninput="searchCodes()">
                        <i class="fas fa-search"></i>
                    </div>
                </div>

                <div class="table-container">
                    <table>
                        <thead>
                            <tr>
                                <th>الكود</th>
                                <th>المدة</th>
                                <th>الحالة</th>
                                <th>تاريخ الإنشاء</th>
                                <th>تاريخ الانتهاء</th>
                                <th>الإجراءات</th>
                            </tr>
                        </thead>
                        <tbody id="codesTable">
                            <!-- سيتم ملؤه ديناميكياً -->
                        </tbody>
                    </table>
                </div>

                <div style="text-align: center; padding: 20px; color: rgba(255, 255, 255, 0.5);">
                    <i class="fas fa-sync-alt loading"></i>
                    <span>جاري تحميل البيانات...</span>
                </div>
            </div>
        </div>

        <!-- محتوى التبويب: المستخدمين -->
        <div id="users" class="content">
            <div class="card">
                <div class="card-header">
                    <div>
                        <div class="card-title">المستخدمين النشطين</div>
                        <div class="card-subtitle">عرض وإدارة حسابات المستخدمين</div>
                    </div>
                    <div class="filters">
                        <select class="form-control filter-select" onchange="filterUsers()">
                            <option value="">جميع المستخدمين</option>
                            <option value="active">النشطين فقط</option>
                            <option value="expired">المنتهية صلاحيتهم</option>
                        </select>
                    </div>
                </div>

                <div class="table-container">
                    <table>
                        <thead>
                            <tr>
                                <th>المستخدم</th>
                                <th>البريد</th>
                                <th>الحالة</th>
                                <th>تاريخ التسجيل</th>
                                <th>تاريخ الانتهاء</th>
                                <th>الإجراءات</th>
                            </tr>
                        </thead>
                        <tbody id="usersTable">
                            <!-- سيتم ملؤه ديناميكياً -->
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

        <!-- محتوى التبويب: التقارير -->
        <div id="reports" class="content">
            <div class="card">
                <div class="card-header">
                    <div>
                        <div class="card-title">تقارير النظام</div>
                        <div class="card-subtitle">إحصائيات وأداء النظام</div>
                    </div>
                    <i class="fas fa-chart-line fa-2x" style="color: #25D366;"></i>
                </div>

                <div class="stats-grid">
                    <div class="stat-item">
                        <div class="stat-item-value" id="totalGenerated">0</div>
                        <div class="stat-item-label">إجمالي الأكواد المولدة</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-item-value" id="totalUsed">0</div>
                        <div class="stat-item-label">الأكواد المستخدمة</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-item-value" id="avgDuration">0 يوم</div>
                        <div class="stat-item-label">متوسط المدة</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-item-value" id="successRate">0%</div>
                        <div class="stat-item-label">معدل النجاح</div>
                    </div>
                </div>
            </div>

            <div class="card">
                <div class="card-header">
                    <div class="card-title">إحصائيات زمنية</div>
                    <div class="card-subtitle">توزيع الأكواد حسب المدة</div>
                </div>

                <div id="durationChart" style="padding: 20px; min-height: 300px;">
                    <!-- مخطط بياني سيتم إنشاؤه ديناميكياً -->
                </div>
            </div>
        </div>

        <!-- محتوى التبويب: الإعدادات -->
        <div id="settings" class="content">
            <div class="card">
                <div class="card-header">
                    <div>
                        <div class="card-title">إعدادات النظام</div>
                        <div class="card-subtitle">تخصيص وتكوين النظام</div>
                    </div>
                    <i class="fas fa-sliders-h fa-2x" style="color: #5a67d8;"></i>
                </div>

                <div class="form-group">
                    <label class="form-label">عنوان الـ API</label>
                    <input type="text" class="form-control" id="apiUrl" value="https://tarafbackend.onrender.com" readonly>
                    <small style="display: block; margin-top: 5px; opacity: 0.7;">عنوان خادم الباك إند</small>
                </div>

                <div class="form-group">
                    <label class="form-label">كود الأمان الافتراضي</label>
                    <input type="password" class="form-control" id="defaultToken" placeholder="أدخل كود الأمان الافتراضي">
                </div>

                <div class="form-group">
                    <label class="form-label">السعر الافتراضي</label>
                    <input type="number" class="form-control" id="defaultPrice" placeholder="السعر الافتراضي بالريال">
                </div>

                <div class="form-group">
                    <label class="form-label">تحديث البيانات تلقائياً</label>
                    <select class="form-control" id="autoRefresh">
                        <option value="30">كل 30 ثانية</option>
                        <option value="60">كل دقيقة</option>
                        <option value="300">كل 5 دقائق</option>
                        <option value="0">غير مفعل</option>
                    </select>
                </div>

                <div class="form-row">
                    <button class="btn btn-success" onclick="saveSettings()">
                        <i class="fas fa-save"></i>
                        حفظ الإعدادات
                    </button>
                    <button class="btn btn-secondary" onclick="resetSettings()">
                        <i class="fas fa-undo"></i>
                        إعادة تعيين
                    </button>
                </div>
            </div>

            <div class="card">
                <div class="card-header">
                    <div class="card-title">معلومات النظام</div>
                </div>

                <div class="user-details">
                    <div class="user-detail">
                        <span class="user-detail-label">إصدار النظام:</span>
                        <span class="user-detail-value">v2.6.0</span>
                    </div>
                    <div class="user-detail">
                        <span class="user-detail-label">تاريخ التحديث:</span>
                        <span class="user-detail-value">2026-02-07</span>
                    </div>
                    <div class="user-detail">
                        <span class="user-detail-label">المطور:</span>
                        <span class="user-detail-value">فهد الخالدي</span>
                    </div>
                    <div class="user-detail">
                        <span class="user-detail-label">الدعم:</span>
                        <span class="user-detail-value">iFahadenglish@gmail.com</span>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- إشعارات -->
    <div class="notification" id="notification">
        <div class="notification-content">
            <i class="fas fa-check-circle"></i>
            <span id="notificationMessage">تمت العملية بنجاح</span>
        </div>
        <button class="notification-close" onclick="hideNotification()">×</button>
    </div>

    <script>
        // ==================== التكوين ====================
        const API_BASE_URL = "https://tarafbackend.onrender.com";
        let currentDuration = "1d";
        let autoRefreshInterval = null;

        // ==================== تهيئة الصفحة ====================
        document.addEventListener('DOMContentLoaded', function() {
            // تحميل الإعدادات المحفوظة
            loadSettings();
            
            // إعداد علامات المدة
            setupDurationTags();
            
            // تحميل البيانات الأولية
            loadDashboardStats();
            loadActiveCodes();
            
            // إعداد التحديث التلقائي
            setupAutoRefresh();
            
            // منع التكبير التلقائي على الهواتف
            preventZoom();
        });

        // ==================== وظائف التنقل ====================
        function showTab(tabId) {
            // إخفاء جميع المحتويات
            document.querySelectorAll('.content').forEach(content => {
                content.classList.remove('active');
            });
            
            // إلغاء تفعيل جميع الألسنة
            document.querySelectorAll('.tab').forEach(tab => {
                tab.classList.remove('active');
            });
            
            // إظهار المحتوى المطلوب
            document.getElementById(tabId).classList.add('active');
            
            // تفعيل اللسان المطلوب
            document.querySelector(`[onclick="showTab('${tabId}')"]`).classList.add('active');
            
            // تحميل البيانات الخاصة بالتبويب
            switch(tabId) {
                case 'generate':
                    break;
                case 'codes':
                    loadActiveCodes();
                    break;
                case 'users':
                    loadUsers();
                    break;
                case 'reports':
                    loadReports();
                    break;
                case 'settings':
                    break;
            }
        }

        // ==================== إعداد المدة ====================
        function setupDurationTags() {
            const tags = document.querySelectorAll('.duration-tag');
            tags.forEach(tag => {
                tag.addEventListener('click', function() {
                    tags.forEach(t => t.classList.remove('active'));
                    this.classList.add('active');
                    currentDuration = this.dataset.duration;
                });
            });
        }

        // ==================== توليد الأكواد ====================
        async function generateCodes() {
            const adminToken = document.getElementById('adminToken').value;
            const codeCount = parseInt(document.getElementById('codeCount').value);
            const price = document.getElementById('price').value;
            
            if (!adminToken) {
                showNotification('يرجى إدخال كود الأمان', 'error');
                return;
            }
            
            // عرض حالة التحميل
            const generateBtn = document.querySelector('.btn-success');
            const originalText = generateBtn.innerHTML;
            generateBtn.innerHTML = '<i class="fas fa-spinner fa-spin"></i> جاري التوليد...';
            generateBtn.disabled = true;
            
            try {
                const codes = [];
                
                // توليد أكواد متعددة
                for (let i = 0; i < codeCount; i++) {
                    const response = await fetch(`${API_BASE_URL}/generate-code?key=${encodeURIComponent(adminToken)}&duration=${currentDuration}`);
                    
                    if (!response.ok) {
                        throw new Error(`خطأ في توليد الكود: ${response.status}`);
                    }
                    
                    const data = await response.json();
                    codes.push({
                        code: data.activation_code,
                        duration: currentDuration,
                        expires_at: data.expires_at,
                        price: price || 'غير محدد'
                    });
                    
                    // تأخير بسيط بين كل طلب
                    await new Promise(resolve => setTimeout(resolve, 100));
                }
                
                // عرض الأكواد المولدة
                displayGeneratedCodes(codes);
                showNotification(`تم توليد ${codes.length} كود بنجاح`, 'success');
                
                // تحديث الإحصائيات
                loadDashboardStats();
                
            } catch (error) {
                console.error('خطأ في توليد الأكواد:', error);
                showNotification(`خطأ: ${error.message}`, 'error');
            } finally {
                // استعادة حالة الزر
                generateBtn.innerHTML = originalText;
                generateBtn.disabled = false;
            }
        }

        function displayGeneratedCodes(codes) {
            const codesText = codes.map(c => 
                `الكود: ${c.code}\nالمدة: ${getDurationText(c.duration)}\nالسعر: ${c.price} ر.س\nتاريخ الانتهاء: ${formatDate(c.expires_at)}\n────────────────────`
            ).join('\n\n');
            
            document.getElementById('generatedCodes').value = codesText;
            document.getElementById('generatedCodesCard').style.display = 'block';
        }

        function getDurationText(duration) {
            const durations = {
                '5m': '5 دقائق',
                '30m': '30 دقيقة',
                '1h': 'ساعة واحدة',
                '3h': '3 ساعات',
                '1d': 'يوم واحد',
                '3d': '3 أيام',
                '7d': 'أسبوع',
                '30d': 'شهر',
                '90d': '3 أشهر',
                '150d': '5 أشهر'
            };
            return durations[duration] || duration;
        }

        function copyCodes() {
            const textarea = document.getElementById('generatedCodes');
            textarea.select();
            document.execCommand('copy');
            showNotification('تم نسخ الأكواد إلى الحافظة', 'success');
        }

        function shareCodes() {
            const codes = document.getElementById('generatedCodes').value;
            const text = `أكواد تفعيل ناصر AI:\n\n${codes}\n\nتم إنشاؤها عبر لوحة التحكم`;
            
            if (navigator.share) {
                navigator.share({
                    title: 'أكواد تفعيل ناصر AI',
                    text: text
                });
            } else {
                const whatsappUrl = `https://wa.me/?text=${encodeURIComponent(text)}`;
                window.open(whatsappUrl, '_blank');
            }
        }

        // ==================== تحميل الأكواد النشطة ====================
        async function loadActiveCodes() {
            const tbody = document.getElementById('codesTable');
            tbody.innerHTML = `
                <tr>
                    <td colspan="6" style="text-align: center; padding: 20px;">
                        <i class="fas fa-sync-alt loading"></i>
                        <span>جاري تحميل البيانات...</span>
                    </td>
                </tr>
            `;
            
            try {
                // في الواقع، سنحتاج إلى إنشاء endpoint جديد في الباك إند
                // لهذه الأغراض، سنستخدم تخزين مؤقت
                const codes = JSON.parse(localStorage.getItem('generated_codes') || '[]');
                
                if (codes.length === 0) {
                    tbody.innerHTML = `
                        <tr>
                            <td colspan="6" style="text-align: center; padding: 20px; color: rgba(255,255,255,0.5);">
                                <i class="fas fa-inbox"></i>
                                <br>
                                <span>لا توجد أكواد نشطة</span>
                            </td>
                        </tr>
                    `;
                    return;
                }
                
                tbody.innerHTML = '';
                codes.forEach((code, index) => {
                    const row = document.createElement('tr');
                    const status = getCodeStatus(code.expires_at);
                    
                    row.innerHTML = `
                        <td><code style="background: rgba(255,255,255,0.1); padding: 5px 10px; border-radius: 5px; font-family: monospace;">${code.code}</code></td>
                        <td>${getDurationText(code.duration)}</td>
                        <td><span class="badge ${status.class}">${status.text}</span></td>
                        <td>${formatDate(new Date().toISOString())}</td>
                        <td>${formatDate(code.expires_at)}</td>
                        <td>
                            <button class="btn btn-small btn-secondary" onclick="copyCode('${code.code}')" title="نسخ">
                                <i class="fas fa-copy"></i>
                            </button>
                            <button class="btn btn-small btn-danger" onclick="deleteCode(${index})" title="حذف">
                                <i class="fas fa-trash"></i>
                            </button>
                        </td>
                    `;
                    tbody.appendChild(row);
                });
                
            } catch (error) {
                console.error('خطأ في تحميل الأكواد:', error);
                tbody.innerHTML = `
                    <tr>
                        <td colspan="6" style="text-align: center; padding: 20px; color: #d9534f;">
                            <i class="fas fa-exclamation-triangle"></i>
                            <br>
                            <span>خطأ في تحميل البيانات</span>
                        </td>
                    </tr>
                `;
            }
        }

        function getCodeStatus(expiresAt) {
            const now = new Date();
            const expiry = new Date(expiresAt);
            
            if (expiry > now) {
                const diff = expiry - now;
                const days = Math.floor(diff / (1000 * 60 * 60 * 24));
                
                if (days > 30) {
                    return { class: 'badge-success', text: 'نشط' };
                } else if (days > 7) {
                    return { class: 'badge-info', text: 'متبقي: ' + days + ' يوم' };
                } else if (days > 1) {
                    return { class: 'badge-warning', text: 'ينتهي قريباً' };
                } else {
                    return { class: 'badge-danger', text: 'ينتهي اليوم' };
                }
            } else {
                return { class: 'badge-danger', text: 'منتهي' };
            }
        }

        function copyCode(code) {
            navigator.clipboard.writeText(code);
            showNotification('تم نسخ الكود إلى الحافظة', 'success');
        }

        function deleteCode(index) {
            if (confirm('هل أنت متأكد من حذف هذا الكود؟')) {
                const codes = JSON.parse(localStorage.getItem('generated_codes') || '[]');
                codes.splice(index, 1);
                localStorage.setItem('generated_codes', JSON.stringify(codes));
                loadActiveCodes();
                showNotification('تم حذف الكود بنجاح', 'success');
            }
        }

        function searchCodes() {
            const searchTerm = document.getElementById('searchCodes').value.toLowerCase();
            const rows = document.querySelectorAll('#codesTable tr');
            
            rows.forEach(row => {
                const text = row.textContent.toLowerCase();
                row.style.display = text.includes(searchTerm) ? '' : 'none';
            });
        }

        // ==================== إدارة المستخدمين ====================
        async function loadUsers() {
            // هذه دالة تجريبية - في الواقع ستستدعي API المستخدمين
            const users = [
                { name: 'أحمد محمد', email: 'ahmed@example.com', status: 'active', registered: '2026-01-15', expires: '2026-04-15' },
                { name: 'سارة علي', email: 'sara@example.com', status: 'active', registered: '2026-01-20', expires: '2026-02-20' },
                { name: 'خالد حسن', email: 'khaled@example.com', status: 'expired', registered: '2025-12-01', expires: '2026-01-01' },
                { name: 'فاطمة أحمد', email: 'fatima@example.com', status: 'active', registered: '2026-02-01', expires: '2026-05-01' }
            ];
            
            const tbody = document.getElementById('usersTable');
            tbody.innerHTML = '';
            
            users.forEach(user => {
                const row = document.createElement('tr');
                const statusClass = user.status === 'active' ? 'badge-success' : 'badge-danger';
                const statusText = user.status === 'active' ? 'نشط' : 'منتهي';
                
                row.innerHTML = `
                    <td>${user.name}</td>
                    <td>${user.email}</td>
                    <td><span class="badge ${statusClass}">${statusText}</span></td>
                    <td>${formatDate(user.registered)}</td>
                    <td>${formatDate(user.expires)}</td>
                    <td>
                        <button class="btn btn-small btn-secondary" title="عرض التفاصيل">
                            <i class="fas fa-eye"></i>
                        </button>
                        <button class="btn btn-small btn-warning" title="تجديد الاشتراك">
                            <i class="fas fa-redo"></i>
                        </button>
                    </td>
                `;
                tbody.appendChild(row);
            });
        }

        function filterUsers() {
            const filter = document.querySelector('#users select').value;
            const rows = document.querySelectorAll('#usersTable tr');
            
            rows.forEach(row => {
                const statusBadge = row.querySelector('.badge').textContent;
                const show = !filter || 
                    (filter === 'active' && statusBadge === 'نشط') ||
                    (filter === 'expired' && statusBadge === 'منتهي');
                
                row.style.display = show ? '' : 'none';
            });
        }

        // ==================== التقارير والإحصائيات ====================
        async function loadDashboardStats() {
            // تحميل الإحصائيات
            const codes = JSON.parse(localStorage.getItem('generated_codes') || '[]');
            
            document.getElementById('totalCodes').textContent = codes.length;
            document.getElementById('activeUsers').textContent = Math.floor(codes.length * 0.7); // تقدير تجريبي
            document.getElementById('todayCodes').textContent = getTodayCodesCount(codes);
            document.getElementById('totalRevenue').textContent = calculateTotalRevenue(codes);
        }

        async function loadReports() {
            const codes = JSON.parse(localStorage.getItem('generated_codes') || '[]');
            
            // إحصائيات عامة
            document.getElementById('totalGenerated').textContent = codes.length;
            document.getElementById('totalUsed').textContent = Math.floor(codes.length * 0.65);
            document.getElementById('avgDuration').textContent = calculateAverageDuration(codes);
            document.getElementById('successRate').textContent = calculateSuccessRate(codes);
            
            // إنشاء مخطط بياني بسيط
            createDurationChart(codes);
        }

        function getTodayCodesCount(codes) {
            const today = new Date().toDateString();
            return codes.filter(code => {
                const codeDate = new Date(code.created_at || new Date()).toDateString();
                return codeDate === today;
            }).length;
        }

        function calculateTotalRevenue(codes) {
            const total = codes.reduce((sum, code) => {
                return sum + (parseFloat(code.price) || 0);
            }, 0);
            return total.toFixed(0) + ' ر.س';
        }

        function calculateAverageDuration(codes) {
            if (codes.length === 0) return '0 يوم';
            
            const durationMap = {
                '5m': 5/(60*24), // أيام
                '30m': 30/(60*24),
                '1h': 1/24,
                '3h': 3/24,
                '1d': 1,
                '3d': 3,
                '7d': 7,
                '30d': 30,
                '90d': 90,
                '150d': 150
            };
            
            const total = codes.reduce((sum, code) => {
                return sum + (durationMap[code.duration] || 0);
            }, 0);
            
            const avg = total / codes.length;
            return avg >= 1 ? avg.toFixed(1) + ' يوم' : (avg * 24).toFixed(0) + ' ساعة';
        }

        function calculateSuccessRate(codes) {
            if (codes.length === 0) return '0%';
            const used = Math.floor(codes.length * 0.65);
            return ((used / codes.length) * 100).toFixed(1) + '%';
        }

        function createDurationChart(codes) {
            const durationMap = {
                '5m': '5 دقائق',
                '30m': '30 دقيقة',
                '1h': 'ساعة',
                '3h': '3 ساعات',
                '1d': 'يوم',
                '3d': '3 أيام',
                '7d': 'أسبوع',
                '30d': 'شهر',
                '90d': '3 أشهر',
                '150d': '5 أشهر'
            };
            
            const counts = {};
            codes.forEach(code => {
                counts[code.duration] = (counts[code.duration] || 0) + 1;
            });
            
            const chartContainer = document.getElementById('durationChart');
            let chartHTML = '<div style="max-width: 600px; margin: 0 auto;">';
            
            Object.entries(durationMap).forEach(([key, label]) => {
                const count = counts[key] || 0;
                const percentage = codes.length > 0 ? (count / codes.length * 100) : 0;
                
                chartHTML += `
                    <div style="margin-bottom: 15px;">
                        <div style="display: flex; justify-content: space-between; margin-bottom: 5px;">
                            <span>${label}</span>
                            <span>${count} (${percentage.toFixed(1)}%)</span>
                        </div>
                        <div style="background: rgba(255,255,255,0.1); height: 20px; border-radius: 10px; overflow: hidden;">
                            <div style="background: linear-gradient(90deg, #4d96ff, #2d7dfd); width: ${percentage}%; height: 100%; border-radius: 10px;"></div>
                        </div>
                    </div>
                `;
            });
            
            chartHTML += '</div>';
            chartContainer.innerHTML = chartHTML;
        }

        // ==================== الإعدادات ====================
        function loadSettings() {
            const settings = JSON.parse(localStorage.getItem('admin_settings') || '{}');
            
            if (settings.apiUrl) document.getElementById('apiUrl').value = settings.apiUrl;
            if (settings.defaultToken) document.getElementById('defaultToken').value = settings.defaultToken;
            if (settings.defaultPrice) document.getElementById('defaultPrice').value = settings.defaultPrice;
            if (settings.autoRefresh) document.getElementById('autoRefresh').value = settings.autoRefresh;
            
            // ملء كود الأمان تلقائياً إذا كان محفوظاً
            if (settings.defaultToken) {
                document.getElementById('adminToken').value = settings.defaultToken;
            }
        }

        function saveSettings() {
            const settings = {
                apiUrl: document.getElementById('apiUrl').value,
                defaultToken: document.getElementById('defaultToken').value,
                defaultPrice: document.getElementById('defaultPrice').value,
                autoRefresh: document.getElementById('autoRefresh').value
            };
            
            localStorage.setItem('admin_settings', JSON.stringify(settings));
            showNotification('تم حفظ الإعدادات بنجاح', 'success');
            
            // إعادة إعداد التحديث التلقائي
            setupAutoRefresh();
            
            // ملء كود الأمان تلقائياً
            if (settings.defaultToken) {
                document.getElementById('adminToken').value = settings.defaultToken;
            }
        }

        function resetSettings() {
            if (confirm('هل أنت متأكد من إعادة تعيين جميع الإعدادات؟')) {
                localStorage.removeItem('admin_settings');
                loadSettings();
                showNotification('تم إعادة تعيين الإعدادات', 'success');
            }
        }

        function setupAutoRefresh() {
            const settings = JSON.parse(localStorage.getItem('admin_settings') || '{}');
            const interval = parseInt(settings.autoRefresh || '60');
            
            // إلغاء أي فاصل زمني سابق
            if (autoRefreshInterval) {
                clearInterval(autoRefreshInterval);
            }
            
            // إعداد فاصل زمني جديد إذا كان مفعلاً
            if (interval > 0) {
                autoRefreshInterval = setInterval(() => {
                    const activeTab = document.querySelector('.content.active').id;
                    
                    switch(activeTab) {
                        case 'codes':
                            loadActiveCodes();
                            break;
                        case 'users':
                            loadUsers();
                            break;
                        case 'reports':
                            loadReports();
                            break;
                        default:
                            loadDashboardStats();
                    }
                    
                    console.log('تم تحديث البيانات تلقائياً');
                }, interval * 1000);
            }
        }

        // ==================== أدوات مساعدة ====================
        function formatDate(dateString) {
            if (!dateString) return 'غير محدد';
            const date = new Date(dateString);
            return date.toLocaleDateString('ar-SA', {
                year: 'numeric',
                month: 'long',
                day: 'numeric',
                hour: '2-digit',
                minute: '2-digit'
            });
        }

        function showNotification(message, type = 'success') {
            const notification = document.getElementById('notification');
            const messageEl = document.getElementById('notificationMessage');
            const icon = notification.querySelector('i');
            
            // تغيير الأيقونة حسب النوع
            icon.className = type === 'success' ? 'fas fa-check-circle' :
                            type === 'error' ? 'fas fa-exclamation-circle' :
                            'fas fa-info-circle';
            
            // تغيير اللون حسب النوع
            notification.style.background = type === 'success' ? 
                'linear-gradient(135deg, #066d4d 0%, #044a35 100%)' :
                type === 'error' ?
                'linear-gradient(135deg, #d9534f 0%, #c9302c 100%)' :
                'linear-gradient(135deg, #5a67d8 0%, #4c51bf 100%)';
            
            messageEl.textContent = message;
            notification.classList.add('show');
            
            // إخفاء التلقائي بعد 5 ثواني
            setTimeout(() => {
                hideNotification();
            }, 5000);
        }

        function hideNotification() {
            document.getElementById('notification').classList.remove('show');
        }

        function preventZoom() {
            document.addEventListener('touchstart', function(event) {
                if (event.touches.length > 1) {
                    event.preventDefault();
                }
            }, { passive: false });

            let lastTouchEnd = 0;
            document.addEventListener('touchend', function(event) {
                const now = Date.now();
                if (now - lastTouchEnd <= 300) {
                    event.preventDefault();
                }
                lastTouchEnd = now;
            }, { passive: false });
        }

        // ==================== Web in App Optimization ====================
        if (window.matchMedia('(display-mode: standalone)').matches) {
            // إذا كان التطبيق يعمل في وضع standalone
            document.body.style.paddingTop = 'env(safe-area-inset-top)';
            document.body.style.paddingBottom = 'env(safe-area-inset-bottom)';
        }

        // حفظ الأكواد المولدة في localStorage (للتوضيح فقط)
        // في الواقع، سيتم حفظها في قاعدة بيانات عبر API
        function saveGeneratedCodes(codes) {
            const existing = JSON.parse(localStorage.getItem('generated_codes') || '[]');
            const newCodes = codes.map(code => ({
                ...code,
                created_at: new Date().toISOString(),
                used: false
            }));
            
            localStorage.setItem('generated_codes', JSON.stringify([...existing, ...newCodes]));
        }

        // تعديل دالة generateCodes لحفظ الأكواد
        async function generateCodesEnhanced() {
            const adminToken = document.getElementById('adminToken').value;
            const codeCount = parseInt(document.getElementById('codeCount').value);
            const price = document.getElementById('price').value;
            
            if (!adminToken) {
                showNotification('يرجى إدخال كود الأمان', 'error');
                return;
            }
            
            const generateBtn = document.querySelector('.btn-success');
            const originalText = generateBtn.innerHTML;
            generateBtn.innerHTML = '<i class="fas fa-spinner fa-spin"></i> جاري التوليد...';
            generateBtn.disabled = true;
            
            try {
                const codes = [];
                
                for (let i = 0; i < codeCount; i++) {
                    const response = await fetch(`${API_BASE_URL}/generate-code?key=${encodeURIComponent(adminToken)}&duration=${currentDuration}`);
                    
                    if (!response.ok) {
                        throw new Error(`خطأ في توليد الكود: ${response.status}`);
                    }
                    
                    const data = await response.json();
                    codes.push({
                        code: data.activation_code,
                        duration: currentDuration,
                        expires_at: data.expires_at,
                        price: price || 'غير محدد'
                    });
                    
                    await new Promise(resolve => setTimeout(resolve, 100));
                }
                
                // حفظ الأكواد في localStorage
                saveGeneratedCodes(codes);
                
                displayGeneratedCodes(codes);
                showNotification(`تم توليد ${codes.length} كود بنجاح`, 'success');
                
                loadDashboardStats();
                
            } catch (error) {
                console.error('خطأ في توليد الأكواد:', error);
                showNotification(`خطأ: ${error.message}`, 'error');
            } finally {
                generateBtn.innerHTML = originalText;
                generateBtn.disabled = false;
            }
        }

        // استبدال دالة generateCodes بالنسخة المحسنة
        window.generateCodes = generateCodesEnhanced;
    </script>
</body>
</html>