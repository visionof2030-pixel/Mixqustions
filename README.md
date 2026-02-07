<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <meta name="theme-color" content="#044a35">
    <title>لوحة تحكم الإدارة - ناصر AI</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
    <style>
        /* ========== CSS Reset ========== */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        :root {
            /* الألوان */
            --primary: #044a35;
            --primary-light: #066d4d;
            --secondary: #ffd166;
            --danger: #d9534f;
            --success: #25D366;
            --warning: #f0ad4e;
            --info: #4d96ff;
            
            --bg-dark: #0a1929;
            --bg-card: rgba(255, 255, 255, 0.05);
            --bg-surface: rgba(255, 255, 255, 0.1);
            
            --text-primary: #ffffff;
            --text-secondary: rgba(255, 255, 255, 0.8);
            --border: rgba(255, 255, 255, 0.2);
            
            /* المسافات */
            --space-xs: 0.5rem;
            --space-sm: 1rem;
            --space-md: 1.5rem;
            --space-lg: 2rem;
            
            /* الأنصاف */
            --radius-sm: 0.5rem;
            --radius-md: 0.75rem;
            --radius-lg: 1rem;
        }

        html {
            font-size: 16px;
            height: 100%;
            overflow-x: hidden;
        }

        body {
            font-family: 'Cairo', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            background: linear-gradient(135deg, var(--bg-dark) 0%, #132f4c 100%);
            color: var(--text-primary);
            line-height: 1.6;
            min-height: 100vh;
            position: relative;
            overflow-x: hidden;
            overflow-y: auto;
        }

        /* ========== الحاوية الرئيسية ========== */
        .app-wrapper {
            width: 100%;
            max-width: 100vw;
            margin: 0 auto;
            padding: env(safe-area-inset-top) 16px env(safe-area-inset-bottom);
            overflow-x: hidden;
        }

        /* ========== الهيدر ========== */
        .app-header {
            background: linear-gradient(135deg, var(--primary) 0%, var(--primary-light) 100%);
            border-radius: var(--radius-lg);
            padding: var(--space-md);
            margin-bottom: var(--space-md);
            border: 1px solid var(--border);
            position: relative;
            overflow: hidden;
        }

        .app-header::before {
            content: '';
            position: absolute;
            top: 0;
            right: 0;
            width: 100px;
            height: 100px;
            background: radial-gradient(circle, rgba(255, 209, 102, 0.1) 0%, transparent 70%);
        }

        .header-title {
            display: flex;
            align-items: center;
            gap: var(--space-sm);
            margin-bottom: var(--space-sm);
            position: relative;
            z-index: 1;
        }

        .header-title h1 {
            font-size: 1.5rem;
            color: var(--secondary);
        }

        .header-stats {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: var(--space-sm);
            margin-top: var(--space-md);
            position: relative;
            z-index: 1;
        }

        .stat-card {
            background: var(--bg-surface);
            backdrop-filter: blur(10px);
            border: 1px solid var(--border);
            border-radius: var(--radius-md);
            padding: var(--space-sm);
            text-align: center;
        }

        .stat-value {
            font-size: 1.25rem;
            font-weight: 700;
            color: var(--info);
            margin-bottom: var(--space-xs);
        }

        .stat-label {
            font-size: 0.75rem;
            color: var(--text-secondary);
        }

        /* ========== التنقل ========== */
        .nav-tabs {
            display: flex;
            background: var(--bg-card);
            border-radius: var(--radius-md);
            padding: 4px;
            margin-bottom: var(--space-md);
            overflow-x: auto;
            -webkit-overflow-scrolling: touch;
            scrollbar-width: none;
            max-width: 100%;
        }

        .nav-tabs::-webkit-scrollbar {
            display: none;
        }

        .nav-tab {
            flex: 1;
            min-width: 80px;
            padding: var(--space-sm);
            border: none;
            background: transparent;
            color: var(--text-secondary);
            font-size: 0.75rem;
            font-weight: 600;
            cursor: pointer;
            border-radius: var(--radius-sm);
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 4px;
            transition: all 0.3s;
            min-height: 60px;
        }

        .nav-tab:active {
            transform: scale(0.98);
        }

        .nav-tab.active {
            background: linear-gradient(135deg, var(--primary-light) 0%, var(--primary) 100%);
            color: var(--text-primary);
        }

        .tab-icon {
            font-size: 1.125rem;
        }

        /* ========== المحتوى ========== */
        .tab-content {
            display: none;
            animation: fadeIn 0.3s ease;
        }

        .tab-content.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        /* ========== الكروت ========== */
        .card {
            background: var(--bg-card);
            backdrop-filter: blur(10px);
            border: 1px solid var(--border);
            border-radius: var(--radius-lg);
            padding: var(--space-md);
            margin-bottom: var(--space-md);
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: var(--space-md);
        }

        .card-title h3 {
            font-size: 1.125rem;
            color: var(--secondary);
            margin-bottom: var(--space-xs);
        }

        .card-title small {
            font-size: 0.75rem;
            color: var(--text-secondary);
        }

        /* ========== النماذج ========== */
        .form-group {
            margin-bottom: var(--space-md);
        }

        .form-label {
            display: block;
            font-size: 0.875rem;
            font-weight: 600;
            color: var(--info);
            margin-bottom: var(--space-xs);
        }

        .form-control {
            width: 100%;
            padding: 0.875rem;
            background: var(--bg-surface);
            border: 1px solid var(--border);
            border-radius: var(--radius-md);
            color: var(--text-primary);
            font-size: 1rem;
            font-family: inherit;
            min-height: 44px;
            -webkit-appearance: none;
            appearance: none;
        }

        .form-control:focus {
            outline: none;
            border-color: var(--info);
            box-shadow: 0 0 0 3px rgba(77, 150, 255, 0.2);
        }

        textarea.form-control {
            min-height: 100px;
            resize: vertical;
        }

        select.form-control {
            background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' fill='white' viewBox='0 0 16 16'%3E%3Cpath d='M7.247 11.14 2.451 5.658C1.885 5.013 2.345 4 3.204 4h9.592a1 1 0 0 1 .753 1.659l-4.796 5.48a1 1 0 0 1-1.506 0z'/%3E%3C/svg%3E");
            background-repeat: no-repeat;
            background-position: left 0.875rem center;
            background-size: 12px;
            padding-left: 2.5rem;
        }

        /* ========== زر التبديل (Toggle Switch) ========== */
        .toggle-group {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: var(--space-md);
            padding: var(--space-sm);
            background: var(--bg-surface);
            border-radius: var(--radius-md);
            border: 1px solid var(--border);
        }

        .toggle-label {
            font-size: 0.875rem;
            font-weight: 600;
            color: var(--text-primary);
        }

        .toggle-switch {
            position: relative;
            display: inline-block;
            width: 50px;
            height: 26px;
        }

        .toggle-switch input {
            opacity: 0;
            width: 0;
            height: 0;
        }

        .toggle-slider {
            position: absolute;
            cursor: pointer;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: rgba(255, 255, 255, 0.1);
            transition: .4s;
            border-radius: 34px;
        }

        .toggle-slider:before {
            position: absolute;
            content: "";
            height: 18px;
            width: 18px;
            left: 4px;
            bottom: 4px;
            background-color: white;
            transition: .4s;
            border-radius: 50%;
        }

        .toggle-switch input:checked + .toggle-slider {
            background-color: var(--success);
        }

        .toggle-switch input:checked + .toggle-slider:before {
            transform: translateX(24px);
        }

        /* ========== الأزرار ========== */
        .btn {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: var(--space-xs);
            padding: 0.875rem 1.25rem;
            border: none;
            border-radius: var(--radius-md);
            font-size: 1rem;
            font-weight: 700;
            font-family: inherit;
            cursor: pointer;
            transition: all 0.3s;
            text-decoration: none;
            min-height: 44px;
            width: 100%;
        }

        .btn:active {
            transform: scale(0.98);
        }

        .btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--primary-light) 0%, var(--primary) 100%);
            color: var(--text-primary);
        }

        .btn-secondary {
            background: linear-gradient(135deg, #5a67d8 0%, #4c51bf 100%);
            color: var(--text-primary);
        }

        .btn-success {
            background: linear-gradient(135deg, var(--success) 0%, #128C7E 100%);
            color: var(--text-primary);
        }

        .btn-danger {
            background: linear-gradient(135deg, var(--danger) 0%, #c9302c 100%);
            color: var(--text-primary);
        }

        .btn-sm {
            padding: 0.5rem 1rem;
            font-size: 0.875rem;
            min-height: 36px;
            width: auto;
        }

        .btn-group {
            display: flex;
            gap: var(--space-sm);
            margin-top: var(--space-md);
        }

        /* ========== علامات المدة ========== */
        .duration-tags {
            display: flex;
            flex-wrap: wrap;
            gap: var(--space-xs);
            margin-top: var(--space-xs);
        }

        .duration-tag {
            padding: 0.5rem 1rem;
            background: rgba(77, 150, 255, 0.1);
            border: 1px solid rgba(77, 150, 255, 0.3);
            border-radius: 2rem;
            font-size: 0.75rem;
            color: var(--info);
            cursor: pointer;
            transition: all 0.3s;
        }

        .duration-tag:active {
            transform: scale(0.95);
        }

        .duration-tag.active {
            background: linear-gradient(135deg, var(--info) 0%, #2d7dfd 100%);
            color: var(--text-primary);
            border-color: var(--info);
        }

        /* ========== إصلاح: وضوح جدول الأكواد في لوحة الأدمن ========== */
        .table-container {
            max-width: 100%;
            background: #0f2a3f;
            border-radius: 14px;
            overflow: hidden;
            border: 1px solid var(--border);
            margin-top: var(--space-md);
        }

        .table-responsive {
            width: 100%;
            overflow-x: auto;
            -webkit-overflow-scrolling: touch;
            background: #0f2a3f;
            border-radius: 14px;
        }

        .data-table {
            width: 100%;
            min-width: 0 !important;
            border-collapse: collapse;
        }

        .data-table th {
            background: #0b3a2c;
            color: #ffd166;
            font-weight: 800;
            font-size: 13px;
            padding: 12px;
            text-align: center;
            white-space: nowrap;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }

        .data-table td {
            background: #ffffff;
            color: #0a1929;
            font-weight: 700;
            font-size: 13px;
            padding: 12px;
            text-align: center;
            border-bottom: 1px solid #e5e7eb;
            white-space: nowrap;
        }

        .data-table td:first-child {
            font-family: "Courier New", monospace;
            letter-spacing: 1px;
            color: #0b5ed7 !important;
            font-weight: 800;
            direction: ltr;
        }

        .data-table td.expired {
            background: #fee2e2 !important;
            color: #dc2626 !important;
            font-weight: 700;
        }
        
        .data-table td.expired:first-child {
            color: #dc2626 !important;
        }

        .data-table td.expiring-soon {
            background: #fef3c7 !important;
            color: #d97706 !important;
            font-weight: 700;
        }
        
        .data-table td.expiring-soon:first-child {
            color: #d97706 !important;
        }

        .data-table td.active {
            background: #e0f2fe !important;
            color: #0369a1 !important;
            font-weight: 700;
        }
        
        .data-table td.active:first-child {
            color: #0369a1 !important;
        }

        .badge {
            font-weight: 800;
            padding: 4px 10px;
            border-radius: 999px;
            font-size: 12px;
            display: inline-block;
        }

        .badge-active {
            background: #e0f2fe !important;
            color: #0369a1 !important;
        }

        .badge-expiring {
            background: #fef3c7 !important;
            color: #d97706 !important;
        }

        .badge-expired {
            background: #fee2e2 !important;
            color: #dc2626 !important;
        }

        /* ========== حاوية معلومات المستخدم الاختيارية ========== */
        .user-info-container {
            background: rgba(255, 255, 255, 0.05);
            border-radius: var(--radius-md);
            padding: var(--space-md);
            margin-bottom: var(--space-md);
            border: 1px solid rgba(255, 255, 255, 0.1);
            display: none;
        }

        .user-info-container.show {
            display: block;
            animation: slideDown 0.3s ease;
        }

        @keyframes slideDown {
            from {
                opacity: 0;
                transform: translateY(-10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* ========== الإشعارات ========== */
        .notification {
            position: fixed;
            top: var(--space-md);
            right: 16px;
            left: 16px;
            background: linear-gradient(135deg, var(--primary-light) 0%, var(--primary) 100%);
            color: var(--text-primary);
            padding: var(--space-sm);
            border-radius: var(--radius-md);
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
            z-index: 1000;
            display: flex;
            align-items: center;
            justify-content: space-between;
            transform: translateY(-100px);
            opacity: 0;
            transition: all 0.3s;
            max-width: 500px;
            margin: 0 auto;
        }

        .notification.show {
            transform: translateY(0);
            opacity: 1;
        }

        .notification-close {
            background: none;
            border: none;
            color: inherit;
            font-size: 1.25rem;
            cursor: pointer;
            padding: 0.25rem;
            min-height: 32px;
            min-width: 32px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 50%;
        }

        /* ========== الحالات ========== */
        .loading {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 2px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top-color: var(--info);
            animation: spin 1s linear infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        .empty-state {
            text-align: center;
            padding: var(--space-lg);
            color: var(--text-secondary);
        }

        /* ========== Responsive ========== */
        @media (min-width: 768px) {
            .app-wrapper {
                max-width: 768px;
                padding: 20px 16px;
            }
            
            .header-stats {
                grid-template-columns: repeat(4, 1fr);
            }
            
            .nav-tabs {
                flex-wrap: nowrap;
            }
            
            .nav-tab {
                min-width: 100px;
                font-size: 0.875rem;
            }
            
            .btn-group {
                flex-direction: row;
            }
            
            .btn {
                width: auto;
            }
        }

        @media (min-width: 1024px) {
            .app-wrapper {
                max-width: 1024px;
            }
        }

        /* ========== تحسينات الجوال ========== */
        @media (max-width: 480px) {
            .data-table th,
            .data-table td {
                font-size: 12px;
                padding: 10px 8px;
            }
            
            .data-table td:first-child {
                font-size: 11px;
                letter-spacing: 0.5px;
            }
            
            .data-table .status,
            .badge {
                font-size: 11px;
                padding: 3px 8px;
            }
        }

        /* ========== تحسينات اللمس ========== */
        @media (hover: none) and (pointer: coarse) {
            .btn,
            .nav-tab,
            .duration-tag {
                min-height: 44px;
            }
            
            .form-control {
                font-size: 16px;
            }
        }

        /* ========== دعم safe-area ========== */
        @supports (padding: max(0px)) {
            .app-wrapper {
                padding-top: max(16px, env(safe-area-inset-top));
                padding-bottom: max(16px, env(safe-area-inset-bottom));
            }
        }
    </style>
</head>
<body>
    <div class="app-wrapper">
        <!-- الهيدر -->
        <header class="app-header">
            <div class="header-title">
                <i class="fas fa-user-shield"></i>
                <h1>لوحة تحكم الإدارة</h1>
            </div>
            <p>إدارة النظام وتوليد أكواد التفعيل والتحكم بالمستخدمين</p>
            
            <div class="header-stats">
                <div class="stat-card">
                    <div class="stat-value" id="totalCodes">0</div>
                    <div class="stat-label">الأكواد النشطة</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="expiringCodes">0</div>
                    <div class="stat-label">الأكواد ستنتهي قريباً</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="expiredCodes">0</div>
                    <div class="stat-label">الأكواد المنتهية</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="totalRevenue">0 ر.س</div>
                    <div class="stat-label">إجمالي الإيرادات</div>
                </div>
            </div>
        </header>

        <!-- التنقل -->
        <nav class="nav-tabs">
            <button class="nav-tab active" data-tab="generate">
                <i class="fas fa-key tab-icon"></i>
                <span>توليد أكواد</span>
            </button>
            <button class="nav-tab" data-tab="activeCodes">
                <i class="fas fa-check-circle tab-icon"></i>
                <span>الأكواد النشطة</span>
            </button>
            <button class="nav-tab" data-tab="expiredCodes">
                <i class="fas fa-times-circle tab-icon"></i>
                <span>الأكواد المنتهية</span>
            </button>
            <button class="nav-tab" data-tab="reports">
                <i class="fas fa-chart-bar tab-icon"></i>
                <span>التقارير</span>
            </button>
            <button class="nav-tab" data-tab="settings">
                <i class="fas fa-cog tab-icon"></i>
                <span>الإعدادات</span>
            </button>
        </nav>

        <!-- المحتوى -->
        <main>
            <!-- تبويب توليد الأكواد -->
            <section id="generate" class="tab-content active">
                <div class="card">
                    <div class="card-header">
                        <div class="card-title">
                            <h3>توليد كود تفعيل جديد</h3>
                            <small>اختر المدة الزمنية وانقر على توليد</small>
                        </div>
                        <i class="fas fa-key" style="color: var(--secondary);"></i>
                    </div>

                    <div class="form-group">
                        <label class="form-label">مدة التفعيل</label>
                        <div class="duration-tags" id="durationTags">
                            <span class="duration-tag" data-duration="5m">5 دقائق</span>
                            <span class="duration-tag" data-duration="30m">30 دقيقة</span>
                            <span class="duration-tag" data-duration="1h">ساعة واحدة</span>
                            <span class="duration-tag active" data-duration="1d">يوم واحد</span>
                            <span class="duration-tag" data-duration="3d">3 أيام</span>
                            <span class="duration-tag" data-duration="7d">أسبوع</span>
                            <span class="duration-tag" data-duration="30d">شهر</span>
                            <span class="duration-tag" data-duration="90d">3 أشهر</span>
                            <span class="duration-tag" data-duration="150d">5 أشهر</span>
                        </div>
                    </div>

                    <div class="form-group">
                        <label for="codeCount" class="form-label">عدد الأكواد</label>
                        <select id="codeCount" class="form-control">
                            <option value="1">1 كود</option>
                            <option value="5">5 أكواد</option>
                            <option value="10">10 أكواد</option>
                            <option value="20">20 كود</option>
                            <option value="50">50 كود</option>
                        </select>
                    </div>

                    <!-- زر التبديل لإضافة معلومات المستخدم -->
                    <div class="toggle-group">
                        <span class="toggle-label">إضافة معلومات المستخدم (اختياري)</span>
                        <label class="toggle-switch">
                            <input type="checkbox" id="userInfoToggle" onchange="toggleUserInfo()">
                            <span class="toggle-slider"></span>
                        </label>
                    </div>

                    <!-- معلومات المستخدم الاختيارية -->
                    <div class="user-info-container" id="userInfoContainer">
                        <div class="form-group">
                            <label for="userName" class="form-label">اسم المستخدم</label>
                            <input type="text" id="userName" class="form-control" placeholder="أدخل اسم المستخدم">
                        </div>

                        <div class="form-group">
                            <label for="userPhone" class="form-label">رقم الجوال</label>
                            <input type="tel" id="userPhone" class="form-control" placeholder="مثال: 05XXXXXXXX">
                        </div>
                    </div>

                    <div class="form-group">
                        <label for="adminToken" class="form-label">كود الأمان (ADMIN_TOKEN)</label>
                        <input type="password" id="adminToken" class="form-control" placeholder="أدخل كود الأمان">
                    </div>

                    <div class="form-group">
                        <label for="price" class="form-label">السعر (اختياري)</label>
                        <input type="number" id="price" class="form-control" placeholder="أدخل السعر بالريال">
                    </div>

                    <button class="btn btn-success" onclick="generateCodes()">
                        <i class="fas fa-bolt"></i>
                        توليد الأكواد
                    </button>
                </div>

                <div class="card" id="generatedCodesCard" style="display: none;">
                    <div class="card-header">
                        <div class="card-title">
                            <h3>الأكواد المولدة</h3>
                            <small>انسخ الأكواد أو أرسلها مباشرة</small>
                        </div>
                        <i class="fas fa-copy" style="color: var(--info);"></i>
                    </div>

                    <div class="form-group">
                        <label class="form-label">الأكواد المولدة:</label>
                        <textarea id="generatedCodes" class="form-control" rows="6" readonly></textarea>
                    </div>

                    <div class="btn-group">
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
            </section>

            <!-- تبويب الأكواد النشطة -->
            <section id="activeCodes" class="tab-content">
                <div class="card">
                    <div class="card-header">
                        <div class="card-title">
                            <h3>الأكواد النشطة</h3>
                            <small>يشمل الأكواد النشطة والأكواد التي ستنتهي قريباً</small>
                        </div>
                        <div style="position: relative; width: 100%; max-width: 300px;">
                            <input type="text" id="searchActiveCodes" class="form-control" placeholder="ابحث في الأكواد النشطة...">
                            <i class="fas fa-search" style="position: absolute; left: 12px; top: 50%; transform: translateY(-50%); color: var(--text-secondary);"></i>
                        </div>
                    </div>

                    <div class="table-container">
                        <div class="table-responsive">
                            <table class="data-table">
                                <thead>
                                    <tr>
                                        <th>الكود</th>
                                        <th>المدة</th>
                                        <th>اسم المستخدم</th>
                                        <th>الجوال</th>
                                        <th>الحالة</th>
                                        <th>الوقت المتبقي</th>
                                        <th>الإجراءات</th>
                                    </tr>
                                </thead>
                                <tbody id="activeCodesTable">
                                    <tr>
                                        <td colspan="7" style="text-align: center; padding: 40px; background: #0f2a3f;">
                                            <div class="loading"></div>
                                            <p style="margin-top: 10px; color: var(--text-secondary);">جاري تحميل البيانات...</p>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </section>

            <!-- تبويب الأكواد المنتهية -->
            <section id="expiredCodes" class="tab-content">
                <div class="card">
                    <div class="card-header">
                        <div class="card-title">
                            <h3>الأكواد المنتهية</h3>
                            <small>جميع الأكواد المنتهية المفعول</small>
                        </div>
                        <div style="position: relative; width: 100%; max-width: 300px;">
                            <input type="text" id="searchExpiredCodes" class="form-control" placeholder="ابحث في الأكواد المنتهية...">
                            <i class="fas fa-search" style="position: absolute; left: 12px; top: 50%; transform: translateY(-50%); color: var(--text-secondary);"></i>
                        </div>
                    </div>

                    <div class="table-container">
                        <div class="table-responsive">
                            <table class="data-table">
                                <thead>
                                    <tr>
                                        <th>الكود</th>
                                        <th>المدة</th>
                                        <th>اسم المستخدم</th>
                                        <th>الجوال</th>
                                        <th>الحالة</th>
                                        <th>تاريخ الانتهاء</th>
                                        <th>الإجراءات</th>
                                    </tr>
                                </thead>
                                <tbody id="expiredCodesTable">
                                    <tr>
                                        <td colspan="7" style="text-align: center; padding: 40px; background: #0f2a3f;">
                                            <div class="loading"></div>
                                            <p style="margin-top: 10px; color: var(--text-secondary);">جاري تحميل البيانات...</p>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </section>

            <!-- تبويب التقارير -->
            <section id="reports" class="tab-content">
                <div class="card">
                    <div class="card-header">
                        <div class="card-title">
                            <h3>تقارير النظام</h3>
                            <small>إحصائيات وأداء النظام</small>
                        </div>
                        <i class="fas fa-chart-line" style="color: var(--success);"></i>
                    </div>

                    <div class="header-stats">
                        <div class="stat-card">
                            <div class="stat-value" id="totalGenerated">0</div>
                            <div class="stat-label">إجمالي الأكواد المولدة</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-value" id="totalUsed">0</div>
                            <div class="stat-label">الأكواد المستخدمة</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-value" id="avgDuration">0 يوم</div>
                            <div class="stat-label">متوسط المدة</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-value" id="successRate">0%</div>
                            <div class="stat-label">معدل النجاح</div>
                        </div>
                    </div>

                    <div class="form-group">
                        <label for="reportPeriod" class="form-label">فترة التقرير</label>
                        <select id="reportPeriod" class="form-control" onchange="loadReports()">
                            <option value="today">اليوم</option>
                            <option value="week">الأسبوع الحالي</option>
                            <option value="month">الشهر الحالي</option>
                            <option value="year">السنة الحالية</option>
                            <option value="all">كل الفترات</option>
                        </select>
                    </div>
                </div>
            </section>

            <!-- تبويب الإعدادات -->
            <section id="settings" class="tab-content">
                <div class="card">
                    <div class="card-header">
                        <div class="card-title">
                            <h3>إعدادات النظام</h3>
                            <small>تخصيص وتكوين النظام</small>
                        </div>
                        <i class="fas fa-sliders-h" style="color: #5a67d8;"></i>
                    </div>

                    <div class="form-group">
                        <label for="apiUrl" class="form-label">عنوان الـ API</label>
                        <input type="text" id="apiUrl" class="form-control" value="https://tarafbackend.onrender.com" readonly>
                        <small style="display: block; margin-top: 4px; color: var(--text-secondary);">عنوان خادم الباك إند</small>
                    </div>

                    <div class="form-group">
                        <label for="defaultToken" class="form-label">كود الأمان الافتراضي</label>
                        <input type="password" id="defaultToken" class="form-control" placeholder="أدخل كود الأمان الافتراضي">
                    </div>

                    <div class="form-group">
                        <label for="defaultPrice" class="form-label">السعر الافتراضي</label>
                        <input type="number" id="defaultPrice" class="form-control" placeholder="السعر الافتراضي بالريال">
                    </div>

                    <div class="form-group">
                        <label for="autoRefresh" class="form-label">تحديث البيانات تلقائياً</label>
                        <select id="autoRefresh" class="form-control">
                            <option value="30">كل 30 ثانية</option>
                            <option value="60">كل دقيقة</option>
                            <option value="300">كل 5 دقائق</option>
                            <option value="0">غير مفعل</option>
                        </select>
                    </div>

                    <div class="btn-group">
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
            </section>
        </main>
    </div>

    <!-- إشعارات -->
    <div class="notification" id="notification">
        <div style="display: flex; align-items: center; gap: 10px;">
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
            // إعداد التنقل
            setupNavigation();
            
            // إعداد علامات المدة
            setupDurationTags();
            
            // تحميل الإعدادات
            loadSettings();
            
            // تحميل الإحصائيات
            loadDashboardStats();
            
            // منع التكبير التلقائي
            preventAutoZoom();
            
            // بدء التحديث التلقائي
            startAutoRefresh();
        });

        // ==================== التنقل ====================
        function setupNavigation() {
            document.querySelectorAll('.nav-tab').forEach(tab => {
                tab.addEventListener('click', function() {
                    const tabId = this.dataset.tab;
                    showTab(tabId);
                });
            });
        }

        function showTab(tabId) {
            // إخفاء جميع المحتويات
            document.querySelectorAll('.tab-content').forEach(content => {
                content.classList.remove('active');
            });
            
            // إلغاء تفعيل جميع الألسنة
            document.querySelectorAll('.nav-tab').forEach(tab => {
                tab.classList.remove('active');
            });
            
            // إظهار المحتوى المطلوب
            document.getElementById(tabId).classList.add('active');
            
            // تفعيل اللسان المطلوب
            document.querySelector(`[data-tab="${tabId}"]`).classList.add('active');
            
            // تحميل البيانات الخاصة بالتبويب
            switch(tabId) {
                case 'activeCodes':
                    loadActiveCodes();
                    break;
                case 'expiredCodes':
                    loadExpiredCodes();
                    break;
                case 'reports':
                    loadReports();
                    break;
            }
        }

        // ==================== تبديل معلومات المستخدم ====================
        function toggleUserInfo() {
            const container = document.getElementById('userInfoContainer');
            const toggle = document.getElementById('userInfoToggle');
            
            if (toggle.checked) {
                container.classList.add('show');
            } else {
                container.classList.remove('show');
                // مسح القيم عند الإخفاء
                document.getElementById('userName').value = '';
                document.getElementById('userPhone').value = '';
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
            const userInfoToggle = document.getElementById('userInfoToggle').checked;
            const userName = userInfoToggle ? document.getElementById('userName').value.trim() : '';
            const userPhone = userInfoToggle ? document.getElementById('userPhone').value.trim() : '';
            
            if (!adminToken) {
                showNotification('يرجى إدخال كود الأمان', 'error');
                return;
            }
            
            // التحقق من صحة رقم الجوال إذا تم إدخاله
            if (userInfoToggle && userPhone) {
                const phoneRegex = /^(05|5)(5|0|3|6|4|9|1|8|7)([0-9]{7})$/;
                if (!phoneRegex.test(userPhone)) {
                    showNotification('رقم الجوال غير صحيح. يجب أن يبدأ بـ 05 ويحتوي على 10 أرقام', 'error');
                    return;
                }
            }
            
            const btn = document.querySelector('#generate .btn-success');
            const originalText = btn.innerHTML;
            btn.innerHTML = '<i class="fas fa-spinner fa-spin"></i> جاري التوليد...';
            btn.disabled = true;
            
            try {
                const codes = [];
                
                for (let i = 0; i < codeCount; i++) {
                    const response = await fetch(
                        `${API_BASE_URL}/generate-code?duration=${currentDuration}`,
                        {
                            method: "POST",
                            headers: {
                                "X-Admin-Token": adminToken
                            }
                        }
                    );
                    
                    if (!response.ok) {
                        throw new Error(`خطأ في توليد الكود: ${response.status}`);
                    }
                    
                    const data = await response.json();
                    codes.push({
                        code: data.activation_code,
                        duration: currentDuration,
                        expires_at: data.expires_at,
                        price: price || 'غير محدد',
                        user_name: userName || 'غير محدد',
                        user_phone: userPhone || 'غير محدد',
                        created_at: new Date().toISOString(),
                        status: 'active'
                    });
                    
                    await new Promise(resolve => setTimeout(resolve, 100));
                }
                
                // حفظ الأكواد
                saveGeneratedCodes(codes);
                
                // عرض الأكواد
                displayGeneratedCodes(codes, userName, userPhone);
                showNotification(`تم توليد ${codes.length} كود بنجاح`, 'success');
                
                // إعادة تعيين الحقول
                if (userInfoToggle) {
                    document.getElementById('userName').value = '';
                    document.getElementById('userPhone').value = '';
                    document.getElementById('userInfoToggle').checked = false;
                    document.getElementById('userInfoContainer').classList.remove('show');
                }
                
                // تحديث الإحصائيات
                loadDashboardStats();
                
            } catch (error) {
                console.error('خطأ في توليد الأكواد:', error);
                showNotification(`خطأ: ${error.message}`, 'error');
            } finally {
                btn.innerHTML = originalText;
                btn.disabled = false;
            }
        }

        function saveGeneratedCodes(codes) {
            const existing = JSON.parse(localStorage.getItem('admin_codes') || '[]');
            const newCodes = codes.map(code => ({
                ...code,
                id: Date.now() + Math.random(),
                user_name: code.user_name,
                user_phone: code.user_phone,
                status: getCodeStatus(code.expires_at).type
            }));
            
            localStorage.setItem('admin_codes', JSON.stringify([...existing, ...newCodes]));
        }

        function displayGeneratedCodes(codes, userName, userPhone) {
            let codesText = '';
            
            codes.forEach((code, index) => {
                codesText += `الكود ${index + 1}: ${code.code}\n`;
                codesText += `المدة: ${getDurationText(code.duration)}\n`;
                codesText += `السعر: ${code.price} ر.س\n`;
                
                if (userName && userName !== 'غير محدد') {
                    codesText += `اسم المستخدم: ${userName}\n`;
                }
                
                if (userPhone && userPhone !== 'غير محدد') {
                    codesText += `رقم الجوال: ${userPhone}\n`;
                }
                
                codesText += `تاريخ الانتهاء: ${formatDate(code.expires_at)}\n`;
                codesText += `────────────────────\n\n`;
            });
            
            document.getElementById('generatedCodes').value = codesText;
            document.getElementById('generatedCodesCard').style.display = 'block';
            
            // تمرير إلى أسفل لعرض الأكواد المولدة
            setTimeout(() => {
                document.getElementById('generatedCodesCard').scrollIntoView({ behavior: 'smooth' });
            }, 300);
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
            const tbody = document.getElementById('activeCodesTable');
            
            try {
                const allCodes = JSON.parse(localStorage.getItem('admin_codes') || '[]');
                const now = new Date();
                
                // تصفية الأكواد النشطة فقط (غير منتهية)
                const activeCodes = allCodes.filter(code => {
                    const expiry = new Date(code.expires_at);
                    return expiry > now;
                });
                
                if (activeCodes.length === 0) {
                    tbody.innerHTML = `
                        <tr>
                            <td colspan="7" style="text-align: center; padding: 40px; background: #0f2a3f; color: var(--text-secondary);">
                                <i class="fas fa-inbox" style="font-size: 2rem; opacity: 0.5; margin-bottom: 10px;"></i>
                                <p>لا توجد أكواد نشطة</p>
                            </td>
                        </tr>
                    `;
                    return;
                }
                
                tbody.innerHTML = '';
                activeCodes.forEach((code, index) => {
                    const status = getCodeStatus(code.expires_at);
                    const statusClass = status.type === 'expiring' ? 'badge-expiring' : 'badge-active';
                    const statusElement = `<span class="badge ${statusClass}">${status.text}</span>`;
                    
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td class="${status.type}"><code>${code.code}</code></td>
                        <td class="${status.type}">${getDurationText(code.duration)}</td>
                        <td class="${status.type}">${code.user_name || 'غير محدد'}</td>
                        <td class="${status.type}">${code.user_phone || 'غير محدد'}</td>
                        <td class="${status.type}">${statusElement}</td>
                        <td class="${status.type}">${getTimeRemaining(code.expires_at)}</td>
                        <td>
                            <button class="btn btn-sm btn-secondary" onclick="copyCode('${code.code}')">
                                <i class="fas fa-copy"></i>
                            </button>
                            <button class="btn btn-sm btn-danger" onclick="deleteCode(${index})">
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
                        <td colspan="7" style="text-align: center; padding: 40px; color: #d9534f; background: #0f2a3f;">
                            <i class="fas fa-exclamation-triangle"></i>
                            <p>خطأ في تحميل البيانات</p>
                        </td>
                    </tr>
                `;
            }
        }

        // ==================== تحميل الأكواد المنتهية ====================
        async function loadExpiredCodes() {
            const tbody = document.getElementById('expiredCodesTable');
            
            try {
                const allCodes = JSON.parse(localStorage.getItem('admin_codes') || '[]');
                const now = new Date();
                
                // تصفية الأكواد المنتهية فقط
                const expiredCodes = allCodes.filter(code => {
                    const expiry = new Date(code.expires_at);
                    return expiry <= now;
                });
                
                if (expiredCodes.length === 0) {
                    tbody.innerHTML = `
                        <tr>
                            <td colspan="7" style="text-align: center; padding: 40px; background: #0f2a3f; color: var(--text-secondary);">
                                <i class="fas fa-inbox" style="font-size: 2rem; opacity: 0.5; margin-bottom: 10px;"></i>
                                <p>لا توجد أكواد منتهية</p>
                            </td>
                        </tr>
                    `;
                    return;
                }
                
                tbody.innerHTML = '';
                expiredCodes.forEach((code, index) => {
                    const statusElement = `<span class="badge badge-expired">منتهي</span>`;
                    
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td class="expired"><code>${code.code}</code></td>
                        <td class="expired">${getDurationText(code.duration)}</td>
                        <td class="expired">${code.user_name || 'غير محدد'}</td>
                        <td class="expired">${code.user_phone || 'غير محدد'}</td>
                        <td class="expired">${statusElement}</td>
                        <td class="expired">${formatDate(code.expires_at)}</td>
                        <td>
                            <button class="btn btn-sm btn-secondary" onclick="copyCode('${code.code}')">
                                <i class="fas fa-copy"></i>
                            </button>
                            <button class="btn btn-sm btn-danger" onclick="deleteExpiredCode(${index})">
                                <i class="fas fa-trash"></i>
                            </button>
                        </td>
                    `;
                    tbody.appendChild(row);
                });
                
            } catch (error) {
                console.error('خطأ في تحميل الأكواد المنتهية:', error);
                tbody.innerHTML = `
                    <tr>
                        <td colspan="7" style="text-align: center; padding: 40px; color: #d9534f; background: #0f2a3f;">
                            <i class="fas fa-exclamation-triangle"></i>
                            <p>خطأ في تحميل البيانات</p>
                        </td>
                    </tr>
                `;
            }
        }

        function getCodeStatus(expiresAt) {
            const now = new Date();
            const expiry = new Date(expiresAt);
            
            if (expiry <= now) {
                return { type: 'expired', text: 'منتهي', color: '#fee2e2' };
            }
            
            const diff = expiry - now;
            const hours = Math.floor(diff / (1000 * 60 * 60));
            const days = Math.floor(diff / (1000 * 60 * 60 * 24));
            
            // إذا كان أقل من 24 ساعة متبقة
            if (hours < 24) {
                return { type: 'expiring', text: 'ينتهي قريباً', color: '#fef3c7' };
            }
            
            // إذا كان أقل من 7 أيام متبقية
            if (days < 7) {
                return { type: 'expiring', text: days + ' يوم', color: '#fef3c7' };
            }
            
            return { type: 'active', text: 'نشط', color: '#e0f2fe' };
        }

        function getTimeRemaining(expiresAt) {
            const now = new Date();
            const expiry = new Date(expiresAt);
            
            if (expiry <= now) {
                return 'منتهي';
            }
            
            const diff = expiry - now;
            const days = Math.floor(diff / (1000 * 60 * 60 * 24));
            const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
            
            if (days > 0) {
                return `${days} يوم ${hours} ساعة`;
            } else if (hours > 0) {
                return `${hours} ساعة ${minutes} دقيقة`;
            } else {
                return `${minutes} دقيقة`;
            }
        }

        function copyCode(code) {
            navigator.clipboard.writeText(code);
            showNotification('تم نسخ الكود إلى الحافظة', 'success');
        }

        function deleteCode(index) {
            if (confirm('هل أنت متأكد من حذف هذا الكود؟')) {
                const codes = JSON.parse(localStorage.getItem('admin_codes') || '[]');
                
                // تأكد أن الكود غير منتهي
                const code = codes[index];
                const status = getCodeStatus(code.expires_at);
                
                if (status.type === 'expired') {
                    showNotification('لا يمكن حذف الأكواد المنتهية من هذا القسم، استخدم قسم الأكواد المنتهية', 'error');
                    return;
                }
                
                codes.splice(index, 1);
                localStorage.setItem('admin_codes', JSON.stringify(codes));
                loadActiveCodes();
                loadDashboardStats();
                showNotification('تم حذف الكود بنجاح', 'success');
            }
        }

        function deleteExpiredCode(index) {
            if (confirm('هل أنت متأكد من حذف هذا الكود المنتهي؟')) {
                const allCodes = JSON.parse(localStorage.getItem('admin_codes') || '[]');
                const now = new Date();
                
                // تصفية الأكواد المنتهية فقط
                const expiredCodes = allCodes.filter(code => {
                    const expiry = new Date(code.expires_at);
                    return expiry <= now;
                });
                
                // إزالة الكود من القائمة الكاملة
                const codeToDelete = expiredCodes[index];
                const codeIndex = allCodes.findIndex(c => c.code === codeToDelete.code);
                
                if (codeIndex !== -1) {
                    allCodes.splice(codeIndex, 1);
                    localStorage.setItem('admin_codes', JSON.stringify(allCodes));
                    loadExpiredCodes();
                    loadDashboardStats();
                    showNotification('تم حذف الكود المنتهي بنجاح', 'success');
                }
            }
        }

        // ==================== التقارير ====================
        async function loadDashboardStats() {
            const codes = JSON.parse(localStorage.getItem('admin_codes') || '[]');
            const now = new Date();
            
            // حساب الأكواد النشطة
            const activeCodes = codes.filter(code => {
                const expiry = new Date(code.expires_at);
                const status = getCodeStatus(code.expires_at);
                return expiry > now && status.type !== 'expiring';
            });
            
            // حساب الأكواد التي ستنتهي قريباً
            const expiringCodes = codes.filter(code => {
                const status = getCodeStatus(code.expires_at);
                return status.type === 'expiring';
            });
            
            // حساب الأكواد المنتهية
            const expiredCodes = codes.filter(code => {
                const expiry = new Date(code.expires_at);
                return expiry <= now;
            });
            
            document.getElementById('totalCodes').textContent = activeCodes.length;
            document.getElementById('expiringCodes').textContent = expiringCodes.length;
            document.getElementById('expiredCodes').textContent = expiredCodes.length;
            document.getElementById('totalRevenue').textContent = calculateTotalRevenue(codes);
        }

        async function loadReports() {
            const codes = JSON.parse(localStorage.getItem('admin_codes') || '[]');
            const period = document.getElementById('reportPeriod').value;
            const filteredCodes = filterCodesByPeriod(codes, period);
            
            document.getElementById('totalGenerated').textContent = filteredCodes.length;
            document.getElementById('totalUsed').textContent = calculateUsedCodes(filteredCodes);
            document.getElementById('avgDuration').textContent = calculateAverageDuration(filteredCodes);
            document.getElementById('successRate').textContent = calculateSuccessRate(filteredCodes);
        }

        function calculateTotalRevenue(codes) {
            const total = codes.reduce((sum, code) => {
                return sum + (parseFloat(code.price) || 0);
            }, 0);
            return total.toFixed(0) + ' ر.س';
        }

        function calculateUsedCodes(codes) {
            // يمكن تعديل هذه الدالة حسب البيانات الفعلية
            const now = new Date();
            const expiredCodes = codes.filter(code => {
                const expiry = new Date(code.expires_at);
                return expiry <= now;
            });
            
            return expiredCodes.length;
        }

        function calculateAverageDuration(codes) {
            if (codes.length === 0) return '0 يوم';
            
            const durationMap = {
                '5m': 5/(60*24),
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
            const used = calculateUsedCodes(codes);
            return ((used / codes.length) * 100).toFixed(1) + '%';
        }

        function filterCodesByPeriod(codes, period) {
            const now = new Date();
            let startDate;
            
            switch(period) {
                case 'today':
                    startDate = new Date(now.getFullYear(), now.getMonth(), now.getDate());
                    break;
                case 'week':
                    startDate = new Date(now);
                    startDate.setDate(now.getDate() - 7);
                    break;
                case 'month':
                    startDate = new Date(now.getFullYear(), now.getMonth() - 1, now.getDate());
                    break;
                case 'year':
                    startDate = new Date(now.getFullYear() - 1, now.getMonth(), now.getDate());
                    break;
                case 'all':
                default:
                    return codes;
            }
            
            return codes.filter(code => {
                const codeDate = new Date(code.created_at || new Date());
                return codeDate >= startDate;
            });
        }

        // ==================== الإعدادات ====================
        function loadSettings() {
            const settings = JSON.parse(localStorage.getItem('admin_settings') || '{}');
            
            if (settings.defaultToken) document.getElementById('defaultToken').value = settings.defaultToken;
            if (settings.defaultPrice) document.getElementById('defaultPrice').value = settings.defaultPrice;
            if (settings.autoRefresh) document.getElementById('autoRefresh').value = settings.autoRefresh;
            
            if (settings.defaultToken) {
                document.getElementById('adminToken').value = settings.defaultToken;
            }
        }

        function saveSettings() {
            const settings = {
                defaultToken: document.getElementById('defaultToken').value,
                defaultPrice: document.getElementById('defaultPrice').value,
                autoRefresh: document.getElementById('autoRefresh').value
            };
            
            localStorage.setItem('admin_settings', JSON.stringify(settings));
            showNotification('تم حفظ الإعدادات بنجاح', 'success');
            
            if (settings.defaultToken) {
                document.getElementById('adminToken').value = settings.defaultToken;
            }
            
            // إعادة تشغيل التحديث التلقائي
            startAutoRefresh();
        }

        function startAutoRefresh() {
            const settings = JSON.parse(localStorage.getItem('admin_settings') || '{}');
            const interval = parseInt(settings.autoRefresh || '0');
            
            // إيقاف أي توقيت سابق
            if (autoRefreshInterval) {
                clearInterval(autoRefreshInterval);
            }
            
            // بدء توقيت جديد إذا كان مخصصاً
            if (interval > 0) {
                autoRefreshInterval = setInterval(() => {
                    const activeTab = document.querySelector('.tab-content.active').id;
                    if (activeTab === 'activeCodes') loadActiveCodes();
                    if (activeTab === 'expiredCodes') loadExpiredCodes();
                    if (activeTab === 'reports') loadReports();
                    loadDashboardStats();
                }, interval * 1000);
            }
        }

        function resetSettings() {
            if (confirm('هل أنت متأكد من إعادة تعيين الإعدادات؟')) {
                localStorage.removeItem('admin_settings');
                loadSettings();
                showNotification('تم إعادة تعيين الإعدادات', 'success');
            }
        }

        // ==================== أدوات مساعدة ====================
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
            
            icon.className = type === 'success' ? 'fas fa-check-circle' :
                            type === 'error' ? 'fas fa-exclamation-circle' :
                            'fas fa-info-circle';
            
            notification.style.background = type === 'success' ? 
                'linear-gradient(135deg, var(--primary-light) 0%, var(--primary) 100%)' :
                type === 'error' ?
                'linear-gradient(135deg, var(--danger) 0%, #c9302c 100%)' :
                'linear-gradient(135deg, #5a67d8 0%, #4c51bf 100%)';
            
            messageEl.textContent = message;
            notification.classList.add('show');
            
            setTimeout(() => {
                hideNotification();
            }, 5000);
        }

        function hideNotification() {
            document.getElementById('notification').classList.remove('show');
        }

        function preventAutoZoom() {
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

        // ==================== التصدير ====================
        window.generateCodes = generateCodes;
        window.copyCodes = copyCodes;
        window.shareCodes = shareCodes;
        window.copyCode = copyCode;
        window.deleteCode = deleteCode;
        window.deleteExpiredCode = deleteExpiredCode;
        window.saveSettings = saveSettings;
        window.resetSettings = resetSettings;
        window.showTab = showTab;
        window.hideNotification = hideNotification;
        window.toggleUserInfo = toggleUserInfo;
        window.loadReports = loadReports;
    </script>
</body>
</html>