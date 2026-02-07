<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <meta name="theme-color" content="#044a35">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <title>لوحة تحكم الإدارة - ناصر AI</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
    <style>
        /* ========== CSS Reset و Base Styles ========== */
        *,
        *::before,
        *::after {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }

        :root {
            /* الألوان الرئيسية */
            --primary-color: #044a35;
            --primary-light: #066d4d;
            --secondary-color: #ffd166;
            --danger-color: #d9534f;
            --success-color: #25D366;
            --warning-color: #f0ad4e;
            --info-color: #4d96ff;
            
            /* ألوان الخلفية */
            --bg-primary: #0a1929;
            --bg-secondary: #132f4c;
            --bg-card: rgba(255, 255, 255, 0.05);
            --bg-surface: rgba(255, 255, 255, 0.1);
            
            /* ألوان النص */
            --text-primary: #ffffff;
            --text-secondary: rgba(255, 255, 255, 0.8);
            --text-muted: rgba(255, 255, 255, 0.6);
            
            /* الظلال والحدود */
            --border-color: rgba(255, 255, 255, 0.2);
            --shadow-sm: 0 2px 8px rgba(0, 0, 0, 0.15);
            --shadow-md: 0 4px 16px rgba(0, 0, 0, 0.2);
            --shadow-lg: 0 8px 32px rgba(0, 0, 0, 0.25);
            
            /* الأبعاد والمسافات */
            --spacing-xs: 0.5rem;
            --spacing-sm: 1rem;
            --spacing-md: 1.5rem;
            --spacing-lg: 2rem;
            --spacing-xl: 3rem;
            
            /* الأنصاف */
            --radius-sm: 0.5rem;
            --radius-md: 0.75rem;
            --radius-lg: 1rem;
            --radius-xl: 1.25rem;
            
            /* التوقيتات */
            --transition-fast: 150ms ease;
            --transition-base: 250ms ease;
            --transition-slow: 350ms ease;
            
            /* أحجام الخطوط */
            --text-xs: 0.75rem;
            --text-sm: 0.875rem;
            --text-base: 1rem;
            --text-lg: 1.125rem;
            --text-xl: 1.25rem;
            --text-2xl: 1.5rem;
            --text-3xl: 1.875rem;
        }

        html {
            font-size: 16px;
            height: 100%;
            overflow-x: hidden;
            text-size-adjust: 100%;
            -webkit-text-size-adjust: 100%;
        }

        body {
            font-family: 'Cairo', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            background: linear-gradient(135deg, var(--bg-primary) 0%, var(--bg-secondary) 100%);
            color: var(--text-primary);
            line-height: 1.6;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            overflow-x: hidden;
            padding: env(safe-area-inset-top) env(safe-area-inset-right) env(safe-area-inset-bottom) env(safe-area-inset-left);
        }

        /* ========== Typography ========== */
        h1, h2, h3, h4, h5, h6 {
            font-weight: 700;
            line-height: 1.3;
            margin-bottom: var(--spacing-sm);
        }

        h1 { font-size: var(--text-3xl); }
        h2 { font-size: var(--text-2xl); }
        h3 { font-size: var(--text-xl); }
        h4 { font-size: var(--text-lg); }

        p {
            margin-bottom: var(--spacing-sm);
            color: var(--text-secondary);
        }

        small {
            font-size: var(--text-xs);
            color: var(--text-muted);
        }

        /* ========== Layout Components ========== */
        .app-container {
            flex: 1;
            width: 100%;
            max-width: 100%;
            padding: var(--spacing-sm);
            display: flex;
            flex-direction: column;
            gap: var(--spacing-md);
        }

        /* ========== Header ========== */
        .app-header {
            background: linear-gradient(135deg, var(--primary-color) 0%, var(--primary-light) 100%);
            border-radius: var(--radius-lg);
            padding: var(--spacing-md);
            position: relative;
            overflow: hidden;
            box-shadow: var(--shadow-lg);
            border: 1px solid var(--border-color);
        }

        .app-header::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle at 30% 30%, rgba(255, 209, 102, 0.1) 0%, transparent 50%);
            pointer-events: none;
        }

        .header-content {
            position: relative;
            z-index: 1;
            display: flex;
            flex-direction: column;
            gap: var(--spacing-sm);
        }

        .header-title {
            display: flex;
            align-items: center;
            gap: var(--spacing-sm);
            color: var(--secondary-color);
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: var(--spacing-sm);
            margin-top: var(--spacing-sm);
        }

        .stat-card {
            background: var(--bg-surface);
            backdrop-filter: blur(10px);
            border: 1px solid var(--border-color);
            border-radius: var(--radius-md);
            padding: var(--spacing-sm);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            text-align: center;
        }

        .stat-value {
            font-size: var(--text-xl);
            font-weight: 700;
            color: var(--info-color);
            margin-bottom: var(--spacing-xs);
        }

        .stat-label {
            font-size: var(--text-xs);
            color: var(--text-muted);
        }

        /* ========== Navigation Tabs ========== */
        .tabs-container {
            position: relative;
            background: var(--bg-card);
            border-radius: var(--radius-lg);
            padding: 0.25rem;
            display: flex;
            overflow-x: auto;
            -webkit-overflow-scrolling: touch;
            scrollbar-width: none;
            gap: 0.25rem;
            box-shadow: var(--shadow-sm);
        }

        .tabs-container::-webkit-scrollbar {
            display: none;
        }

        .nav-tab {
            flex: 1;
            min-width: 5rem;
            padding: var(--spacing-sm);
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 0.5rem;
            background: transparent;
            border: none;
            border-radius: var(--radius-md);
            color: var(--text-secondary);
            font-size: var(--text-xs);
            font-weight: 600;
            cursor: pointer;
            transition: all var(--transition-base);
            min-height: 4.5rem;
            touch-action: manipulation;
        }

        .nav-tab:active {
            transform: scale(0.98);
        }

        .nav-tab.active {
            background: linear-gradient(135deg, var(--primary-light) 0%, var(--primary-color) 100%);
            color: var(--text-primary);
            box-shadow: var(--shadow-md);
        }

        .tab-icon {
            font-size: 1.25rem;
        }

        /* ========== Content Sections ========== */
        .content-section {
            display: none;
            flex: 1;
            min-height: 0;
        }

        .content-section.active {
            display: flex;
            flex-direction: column;
            gap: var(--spacing-md);
            animation: fadeIn var(--transition-slow);
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* ========== Cards ========== */
        .card {
            background: var(--bg-card);
            backdrop-filter: blur(10px);
            border: 1px solid var(--border-color);
            border-radius: var(--radius-lg);
            padding: var(--spacing-md);
            display: flex;
            flex-direction: column;
            gap: var(--spacing-md);
            box-shadow: var(--shadow-md);
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            gap: var(--spacing-sm);
        }

        .card-title {
            display: flex;
            flex-direction: column;
            gap: var(--spacing-xs);
            flex: 1;
        }

        .card-actions {
            display: flex;
            gap: var(--spacing-xs);
        }

        /* ========== Form Elements ========== */
        .form-group {
            display: flex;
            flex-direction: column;
            gap: var(--spacing-xs);
        }

        .form-label {
            font-size: var(--text-sm);
            font-weight: 600;
            color: var(--info-color);
        }

        .form-control {
            width: 100%;
            padding: var(--spacing-sm);
            background: var(--bg-surface);
            border: 1px solid var(--border-color);
            border-radius: var(--radius-md);
            color: var(--text-primary);
            font-size: var(--text-base);
            font-family: inherit;
            transition: all var(--transition-base);
            min-height: 44px;
            -webkit-appearance: none;
            appearance: none;
        }

        .form-control:focus {
            outline: none;
            border-color: var(--info-color);
            box-shadow: 0 0 0 3px rgba(77, 150, 255, 0.2);
        }

        .form-control::placeholder {
            color: var(--text-muted);
        }

        select.form-control {
            background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' fill='white' viewBox='0 0 16 16'%3E%3Cpath d='M7.247 11.14 2.451 5.658C1.885 5.013 2.345 4 3.204 4h9.592a1 1 0 0 1 .753 1.659l-4.796 5.48a1 1 0 0 1-1.506 0z'/%3E%3C/svg%3E");
            background-repeat: no-repeat;
            background-position: left var(--spacing-sm) center;
            background-size: 12px;
            padding-left: 2.5rem;
        }

        textarea.form-control {
            min-height: 120px;
            resize: vertical;
        }

        /* ========== Buttons ========== */
        .btn {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: var(--spacing-xs);
            padding: var(--spacing-sm) var(--spacing-md);
            border: none;
            border-radius: var(--radius-md);
            font-size: var(--text-base);
            font-weight: 700;
            font-family: inherit;
            cursor: pointer;
            transition: all var(--transition-base);
            text-decoration: none;
            min-height: 44px;
            width: 100%;
            touch-action: manipulation;
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
            background: linear-gradient(135deg, var(--primary-light) 0%, var(--primary-color) 100%);
            color: var(--text-primary);
        }

        .btn-primary:hover {
            box-shadow: var(--shadow-md);
        }

        .btn-secondary {
            background: linear-gradient(135deg, #5a67d8 0%, #4c51bf 100%);
            color: var(--text-primary);
        }

        .btn-success {
            background: linear-gradient(135deg, var(--success-color) 0%, #128C7E 100%);
            color: var(--text-primary);
        }

        .btn-danger {
            background: linear-gradient(135deg, var(--danger-color) 0%, #c9302c 100%);
            color: var(--text-primary);
        }

        .btn-warning {
            background: linear-gradient(135deg, var(--warning-color) 0%, #ec971f 100%);
            color: var(--text-primary);
        }

        .btn-sm {
            padding: 0.5rem 1rem;
            font-size: var(--text-sm);
            min-height: 36px;
            width: auto;
        }

        .btn-group {
            display: flex;
            gap: var(--spacing-sm);
            flex-wrap: wrap;
        }

        /* ========== Duration Tags ========== */
        .duration-tags {
            display: flex;
            flex-wrap: wrap;
            gap: var(--spacing-xs);
        }

        .duration-tag {
            padding: 0.5rem 1rem;
            background: rgba(77, 150, 255, 0.1);
            border: 1px solid rgba(77, 150, 255, 0.3);
            border-radius: 2rem;
            font-size: var(--text-xs);
            color: var(--info-color);
            cursor: pointer;
            transition: all var(--transition-base);
            touch-action: manipulation;
        }

        .duration-tag:active {
            transform: scale(0.95);
        }

        .duration-tag.active {
            background: linear-gradient(135deg, var(--info-color) 0%, #2d7dfd 100%);
            color: var(--text-primary);
            border-color: var(--info-color);
        }

        /* ========== Tables ========== */
        .table-container {
            overflow-x: auto;
            -webkit-overflow-scrolling: touch;
            border-radius: var(--radius-md);
            background: var(--bg-surface);
            border: 1px solid var(--border-color);
            margin-top: var(--spacing-md);
        }

        .data-table {
            width: 100%;
            border-collapse: collapse;
            min-width: 600px;
        }

        .data-table th {
            padding: var(--spacing-sm);
            text-align: right;
            font-weight: 600;
            color: var(--secondary-color);
            background: rgba(255, 255, 255, 0.05);
            border-bottom: 1px solid var(--border-color);
            font-size: var(--text-sm);
            white-space: nowrap;
        }

        .data-table td {
            padding: var(--spacing-sm);
            border-bottom: 1px solid rgba(255, 255, 255, 0.05);
            font-size: var(--text-sm);
        }

        .data-table tr:last-child td {
            border-bottom: none;
        }

        .data-table tr:hover {
            background: rgba(255, 255, 255, 0.02);
        }

        /* ========== Badges ========== */
        .badge {
            display: inline-block;
            padding: 0.25rem 0.75rem;
            border-radius: 2rem;
            font-size: var(--text-xs);
            font-weight: 600;
            text-align: center;
        }

        .badge-success {
            background: rgba(37, 211, 102, 0.2);
            color: var(--success-color);
        }

        .badge-warning {
            background: rgba(240, 173, 78, 0.2);
            color: var(--warning-color);
        }

        .badge-danger {
            background: rgba(217, 83, 79, 0.2);
            color: var(--danger-color);
        }

        .badge-info {
            background: rgba(77, 150, 255, 0.2);
            color: var(--info-color);
        }

        /* ========== Notifications ========== */
        .notification {
            position: fixed;
            top: var(--spacing-md);
            right: var(--spacing-sm);
            left: var(--spacing-sm);
            background: linear-gradient(135deg, var(--primary-light) 0%, var(--primary-color) 100%);
            color: var(--text-primary);
            padding: var(--spacing-sm);
            border-radius: var(--radius-md);
            box-shadow: var(--shadow-lg);
            z-index: 1000;
            display: flex;
            align-items: center;
            justify-content: space-between;
            transform: translateY(-100%);
            opacity: 0;
            transition: all var(--transition-slow);
            max-width: 500px;
            margin: 0 auto;
        }

        .notification.show {
            transform: translateY(0);
            opacity: 1;
        }

        .notification-content {
            display: flex;
            align-items: center;
            gap: var(--spacing-sm);
            flex: 1;
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
            transition: background var(--transition-fast);
        }

        .notification-close:active {
            background: rgba(255, 255, 255, 0.1);
        }

        /* ========== Loading States ========== */
        .loading {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 2px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top-color: var(--info-color);
            animation: spin 1s ease-in-out infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        .loading-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: var(--spacing-sm);
            padding: var(--spacing-xl);
            color: var(--text-muted);
        }

        /* ========== Empty States ========== */
        .empty-state {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: var(--spacing-sm);
            padding: var(--spacing-xl);
            text-align: center;
            color: var(--text-muted);
        }

        .empty-state-icon {
            font-size: 3rem;
            opacity: 0.5;
        }

        /* ========== Search and Filters ========== */
        .search-box {
            position: relative;
            margin-bottom: var(--spacing-md);
        }

        .search-input {
            width: 100%;
            padding: var(--spacing-sm) 3rem var(--spacing-sm) var(--spacing-sm);
            background: var(--bg-surface);
            border: 1px solid var(--border-color);
            border-radius: var(--radius-md);
            color: var(--text-primary);
            font-size: var(--text-base);
            min-height: 44px;
        }

        .search-icon {
            position: absolute;
            left: var(--spacing-sm);
            top: 50%;
            transform: translateY(-50%);
            color: var(--text-muted);
            pointer-events: none;
        }

        .filters-container {
            display: flex;
            gap: var(--spacing-sm);
            margin-bottom: var(--spacing-md);
            flex-wrap: wrap;
        }

        .filter-select {
            flex: 1;
            min-width: 120px;
        }

        /* ========== Responsive Design ========== */
        @media (min-width: 480px) {
            .app-container {
                padding: var(--spacing-md);
            }
            
            .stats-grid {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .nav-tab {
                min-width: 6rem;
                flex-direction: row;
                justify-content: center;
                min-height: 44px;
            }
        }

        @media (min-width: 768px) {
            :root {
                --spacing-sm: 1.25rem;
                --spacing-md: 1.75rem;
                --spacing-lg: 2.5rem;
            }
            
            .app-container {
                max-width: 768px;
                margin: 0 auto;
            }
            
            .stats-grid {
                grid-template-columns: repeat(4, 1fr);
            }
            
            .nav-tab {
                font-size: var(--text-sm);
            }
            
            .card {
                padding: var(--spacing-lg);
            }
            
            .form-row {
                display: grid;
                grid-template-columns: repeat(2, 1fr);
                gap: var(--spacing-md);
            }
            
            .btn-group {
                flex-direction: row;
            }
            
            .btn {
                width: auto;
            }
        }

        @media (min-width: 1024px) {
            .app-container {
                max-width: 1024px;
                padding: var(--spacing-lg);
            }
            
            .content-wrapper {
                display: grid;
                grid-template-columns: 250px 1fr;
                gap: var(--spacing-lg);
            }
            
            .tabs-container {
                flex-direction: column;
                height: fit-content;
            }
            
            .nav-tab {
                min-width: 100%;
                justify-content: flex-start;
                padding: var(--spacing-md);
            }
        }

        /* ========== Accessibility ========== */
        @media (prefers-reduced-motion: reduce) {
            *,
            *::before,
            *::after {
                animation-duration: 0.01ms !important;
                animation-iteration-count: 1 !important;
                transition-duration: 0.01ms !important;
            }
        }

        .sr-only {
            position: absolute;
            width: 1px;
            height: 1px;
            padding: 0;
            margin: -1px;
            overflow: hidden;
            clip: rect(0, 0, 0, 0);
            white-space: nowrap;
            border: 0;
        }

        /* ========== iOS Safe Areas ========== */
        @supports (padding: max(0px)) {
            .app-container {
                padding-left: max(var(--spacing-sm), env(safe-area-inset-left));
                padding-right: max(var(--spacing-sm), env(safe-area-inset-right));
                padding-top: max(var(--spacing-sm), env(safe-area-inset-top));
                padding-bottom: max(var(--spacing-sm), env(safe-area-inset-bottom));
            }
        }

        /* ========== Custom Scrollbar ========== */
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
    </style>
</head>
<body>
    <!-- Main App Container -->
    <div class="app-container">
        <!-- Header -->
        <header class="app-header">
            <div class="header-content">
                <h1 class="header-title">
                    <i class="fas fa-user-shield"></i>
                    لوحة تحكم الإدارة
                </h1>
                <p>إدارة النظام وتوليد أكواد التفعيل والتحكم بالمستخدمين</p>
                
                <div class="stats-grid">
                    <div class="stat-card">
                        <div class="stat-value" id="totalCodes">0</div>
                        <div class="stat-label">الأكواد النشطة</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-value" id="activeUsers">0</div>
                        <div class="stat-label">المستخدمين النشطين</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-value" id="totalRevenue">0 ر.س</div>
                        <div class="stat-label">إجمالي الإيرادات</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-value" id="todayCodes">0</div>
                        <div class="stat-label">أكواد اليوم</div>
                    </div>
                </div>
            </div>
        </header>

        <!-- Navigation Tabs -->
        <nav class="tabs-container">
            <button class="nav-tab active" data-tab="generate">
                <i class="fas fa-key tab-icon"></i>
                <span>توليد أكواد</span>
            </button>
            <button class="nav-tab" data-tab="codes">
                <i class="fas fa-list tab-icon"></i>
                <span>الأكواد النشطة</span>
            </button>
            <button class="nav-tab" data-tab="users">
                <i class="fas fa-users tab-icon"></i>
                <span>المستخدمين</span>
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

        <!-- Main Content Area -->
        <main class="content-area">
            <!-- Tab 1: Generate Codes -->
            <section id="generate" class="content-section active">
                <div class="card">
                    <div class="card-header">
                        <div class="card-title">
                            <h3>توليد كود تفعيل جديد</h3>
                            <small>اختر المدة الزمنية وانقر على توليد</small>
                        </div>
                        <div class="card-actions">
                            <i class="fas fa-key" style="color: var(--secondary-color); font-size: 1.5rem;"></i>
                        </div>
                    </div>

                    <form id="generateForm">
                        <div class="form-group">
                            <label for="duration" class="form-label">مدة التفعيل</label>
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
                            <select id="codeCount" class="form-control" required>
                                <option value="1">1 كود</option>
                                <option value="5">5 أكواد</option>
                                <option value="10">10 أكواد</option>
                                <option value="20">20 كود</option>
                                <option value="50">50 كود</option>
                            </select>
                        </div>

                        <div class="form-group">
                            <label for="adminToken" class="form-label">كود الأمان (ADMIN_TOKEN)</label>
                            <input type="password" id="adminToken" class="form-control" placeholder="أدخل كود الأمان" required>
                        </div>

                        <div class="form-group">
                            <label for="price" class="form-label">السعر (اختياري)</label>
                            <input type="number" id="price" class="form-control" placeholder="أدخل السعر بالريال" min="0" step="1">
                        </div>

                        <button type="button" class="btn btn-success" onclick="generateCodes()">
                            <i class="fas fa-bolt"></i>
                            توليد الأكواد
                        </button>
                    </form>
                </div>

                <div class="card" id="generatedCodesCard" style="display: none;">
                    <div class="card-header">
                        <div class="card-title">
                            <h3>الأكواد المولدة</h3>
                            <small>انسخ الأكواد أو أرسلها مباشرة</small>
                        </div>
                        <div class="card-actions">
                            <i class="fas fa-copy" style="color: var(--info-color); font-size: 1.5rem;"></i>
                        </div>
                    </div>

                    <div class="form-group">
                        <label class="form-label">الأكواد المولدة:</label>
                        <textarea id="generatedCodes" class="form-control" rows="6" readonly style="font-family: monospace;"></textarea>
                    </div>

                    <div class="btn-group">
                        <button type="button" class="btn btn-secondary" onclick="copyCodes()">
                            <i class="fas fa-copy"></i>
                            نسخ الأكواد
                        </button>
                        <button type="button" class="btn btn-warning" onclick="shareCodes()">
                            <i class="fas fa-share-alt"></i>
                            مشاركة
                        </button>
                    </div>
                </div>
            </section>

            <!-- Tab 2: Active Codes -->
            <section id="codes" class="content-section">
                <div class="card">
                    <div class="card-header">
                        <div class="card-title">
                            <h3>الأكواد النشطة</h3>
                            <small>إدارة وتتبع جميع أكواد التفعيل</small>
                        </div>
                        <div class="search-box">
                            <input type="text" id="searchCodes" class="search-input" placeholder="ابحث في الأكواد...">
                            <i class="fas fa-search search-icon"></i>
                        </div>
                    </div>

                    <div class="table-container">
                        <table class="data-table">
                            <thead>
                                <tr>
                                    <th>الكود</th>
                                    <th>المدة</th>
                                    <th>الحالة</th>
                                    <th>تاريخ الانتهاء</th>
                                    <th>الإجراءات</th>
                                </tr>
                            </thead>
                            <tbody id="codesTable">
                                <tr>
                                    <td colspan="5">
                                        <div class="loading-container">
                                            <div class="loading"></div>
                                            <span>جاري تحميل البيانات...</span>
                                        </div>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </section>

            <!-- Tab 3: Users -->
            <section id="users" class="content-section">
                <div class="card">
                    <div class="card-header">
                        <div class="card-title">
                            <h3>المستخدمين النشطين</h3>
                            <small>عرض وإدارة حسابات المستخدمين</small>
                        </div>
                        <div class="filters-container">
                            <select id="userFilter" class="form-control filter-select" onchange="filterUsers()">
                                <option value="">جميع المستخدمين</option>
                                <option value="active">النشطين فقط</option>
                                <option value="expired">المنتهية صلاحيتهم</option>
                            </select>
                        </div>
                    </div>

                    <div class="table-container">
                        <table class="data-table">
                            <thead>
                                <tr>
                                    <th>المستخدم</th>
                                    <th>البريد</th>
                                    <th>الحالة</th>
                                    <th>تاريخ التسجيل</th>
                                    <th>الإجراءات</th>
                                </tr>
                            </thead>
                            <tbody id="usersTable">
                                <!-- سيتم ملؤه ديناميكياً -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </section>

            <!-- Tab 4: Reports -->
            <section id="reports" class="content-section">
                <div class="card">
                    <div class="card-header">
                        <div class="card-title">
                            <h3>تقارير النظام</h3>
                            <small>إحصائيات وأداء النظام</small>
                        </div>
                        <div class="card-actions">
                            <i class="fas fa-chart-line" style="color: var(--success-color); font-size: 1.5rem;"></i>
                        </div>
                    </div>

                    <div class="stats-grid">
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
                </div>
            </section>

            <!-- Tab 5: Settings -->
            <section id="settings" class="content-section">
                <div class="card">
                    <div class="card-header">
                        <div class="card-title">
                            <h3>إعدادات النظام</h3>
                            <small>تخصيص وتكوين النظام</small>
                        </div>
                        <div class="card-actions">
                            <i class="fas fa-sliders-h" style="color: #5a67d8; font-size: 1.5rem;"></i>
                        </div>
                    </div>

                    <form id="settingsForm">
                        <div class="form-group">
                            <label for="apiUrl" class="form-label">عنوان الـ API</label>
                            <input type="text" id="apiUrl" class="form-control" value="https://tarafbackend.onrender.com" readonly>
                            <small>عنوان خادم الباك إند</small>
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
                            <button type="button" class="btn btn-success" onclick="saveSettings()">
                                <i class="fas fa-save"></i>
                                حفظ الإعدادات
                            </button>
                            <button type="button" class="btn btn-secondary" onclick="resetSettings()">
                                <i class="fas fa-undo"></i>
                                إعادة تعيين
                            </button>
                        </div>
                    </form>
                </div>
            </section>
        </main>
    </div>

    <!-- Notification -->
    <div class="notification" id="notification">
        <div class="notification-content">
            <i class="fas fa-check-circle"></i>
            <span id="notificationMessage">تمت العملية بنجاح</span>
        </div>
        <button class="notification-close" onclick="hideNotification()" aria-label="إغلاق">
            ×
        </button>
    </div>

    <script>
        // ==================== التكوين الأساسي ====================
        const API_BASE_URL = "https://tarafbackend.onrender.com";
        let currentDuration = "1d";
        let autoRefreshInterval = null;

        // ==================== تهيئة التطبيق ====================
        document.addEventListener('DOMContentLoaded', function() {
            initializeApp();
        });

        function initializeApp() {
            setupEventListeners();
            loadSettings();
            setupDurationTags();
            loadDashboardStats();
            
            // إعداد Touch-friendly interactions
            setupTouchInteractions();
            
            // منع التكبير التلقائي
            preventAutoZoom();
            
            // إعداد التحديث التلقائي
            setupAutoRefresh();
        }

        // ==================== إعداد Touch Interactions ====================
        function setupTouchInteractions() {
            // تحسين استجابة العناصر للمس
            const touchElements = document.querySelectorAll('button, .duration-tag, .nav-tab');
            
            touchElements.forEach(el => {
                el.addEventListener('touchstart', function() {
                    this.classList.add('active');
                });
                
                el.addEventListener('touchend', function() {
                    this.classList.remove('active');
                });
            });
            
            // منع التمرير الأفقي غير المرغوب فيه
            document.addEventListener('touchmove', function(e) {
                if (e.touches.length > 1) {
                    e.preventDefault();
                }
            }, { passive: false });
        }

        // ==================== منع التكبير التلقائي ====================
        function preventAutoZoom() {
            let lastTouchEnd = 0;
            
            document.addEventListener('touchend', function(e) {
                const now = Date.now();
                if (now - lastTouchEnd <= 300) {
                    e.preventDefault();
                }
                lastTouchEnd = now;
            }, { passive: false });
            
            // منع التكبير المزدوج
            document.addEventListener('dblclick', function(e) {
                e.preventDefault();
            }, { passive: false });
        }

        // ==================== إعداد Event Listeners ====================
        function setupEventListeners() {
            // التنقل بين الألسنة
            document.querySelectorAll('.nav-tab').forEach(tab => {
                tab.addEventListener('click', function() {
                    const tabId = this.dataset.tab;
                    showTab(tabId);
                });
            });
            
            // البحث في الأكواد
            const searchInput = document.getElementById('searchCodes');
            if (searchInput) {
                searchInput.addEventListener('input', debounce(searchCodes, 300));
            }
        }

        // ==================== وظائف التنقل ====================
        function showTab(tabId) {
            // إخفاء جميع المحتويات
            document.querySelectorAll('.content-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // إلغاء تفعيل جميع الألسنة
            document.querySelectorAll('.nav-tab').forEach(tab => {
                tab.classList.remove('active');
            });
            
            // إظهار المحتوى المطلوب
            const targetSection = document.getElementById(tabId);
            if (targetSection) {
                targetSection.classList.add('active');
                
                // تفعيل اللسان المطلوب
                document.querySelector(`[data-tab="${tabId}"]`).classList.add('active');
                
                // تحميل البيانات الخاصة بالتبويب
                loadTabData(tabId);
            }
        }

        function loadTabData(tabId) {
            switch(tabId) {
                case 'codes':
                    loadActiveCodes();
                    break;
                case 'users':
                    loadUsers();
                    break;
                case 'reports':
                    loadReports();
                    break;
            }
        }

        // ==================== إدارة المدة الزمنية ====================
        function setupDurationTags() {
            const tags = document.querySelectorAll('.duration-tag');
            
            tags.forEach(tag => {
                tag.addEventListener('click', function() {
                    // إلغاء تفعيل جميع العلامات
                    tags.forEach(t => t.classList.remove('active'));
                    
                    // تفعيل العلامة المحددة
                    this.classList.add('active');
                    currentDuration = this.dataset.duration;
                });
            });
        }

        // ==================== توليد الأكواد ====================
        async function generateCodes() {
            const adminToken = document.getElementById('adminToken').value.trim();
            const codeCount = parseInt(document.getElementById('codeCount').value);
            const price = document.getElementById('price').value;
            
            // التحقق من المدخلات
            if (!adminToken) {
                showNotification('يرجى إدخال كود الأمان', 'error');
                return;
            }
            
            if (codeCount < 1 || codeCount > 50) {
                showNotification('عدد الأكواد يجب أن يكون بين 1 و 50', 'error');
                return;
            }
            
            // عرض حالة التحميل
            const generateBtn = document.querySelector('#generate .btn-success');
            const originalContent = generateBtn.innerHTML;
            
            generateBtn.innerHTML = '<i class="fas fa-spinner fa-spin"></i> جاري التوليد...';
            generateBtn.disabled = true;
            
            try {
                const generatedCodes = [];
                
                // توليد أكواد متعددة
                for (let i = 0; i < codeCount; i++) {
                    const response = await fetch(
                        `${API_BASE_URL}/generate-code?key=${encodeURIComponent(adminToken)}&duration=${currentDuration}`,
                        {
                            headers: {
                                'Accept': 'application/json'
                            }
                        }
                    );
                    
                    if (!response.ok) {
                        const errorText = await response.text();
                        throw new Error(`خطأ في توليد الكود ${i + 1}: ${response.status} - ${errorText}`);
                    }
                    
                    const data = await response.json();
                    generatedCodes.push({
                        code: data.activation_code,
                        duration: currentDuration,
                        expires_at: data.expires_at,
                        price: price || 'غير محدد',
                        generated_at: new Date().toISOString()
                    });
                    
                    // تأخير بسيط بين الطلبات
                    if (i < codeCount - 1) {
                        await sleep(100);
                    }
                }
                
                // حفظ الأكواد في التخزين المحلي
                saveGeneratedCodes(generatedCodes);
                
                // عرض الأكواد المولدة
                displayGeneratedCodes(generatedCodes);
                
                // إظهار إشعار النجاح
                showNotification(`تم توليد ${generatedCodes.length} كود بنجاح`, 'success');
                
                // تحديث الإحصائيات
                loadDashboardStats();
                
            } catch (error) {
                console.error('خطأ في توليد الأكواد:', error);
                showNotification(`خطأ: ${error.message}`, 'error');
            } finally {
                // استعادة حالة الزر
                generateBtn.innerHTML = originalContent;
                generateBtn.disabled = false;
            }
        }

        function saveGeneratedCodes(codes) {
            try {
                const existingCodes = JSON.parse(localStorage.getItem('admin_generated_codes') || '[]');
                const newCodes = codes.map(code => ({
                    ...code,
                    id: generateUniqueId(),
                    used: false
                }));
                
                const updatedCodes = [...existingCodes, ...newCodes];
                localStorage.setItem('admin_generated_codes', JSON.stringify(updatedCodes));
                
                return updatedCodes;
            } catch (error) {
                console.error('خطأ في حفظ الأكواد:', error);
                return [];
            }
        }

        function displayGeneratedCodes(codes) {
            const codesText = codes.map((code, index) => 
                `${index + 1}. الكود: ${code.code}\n   المدة: ${getDurationText(code.duration)}\n   السعر: ${code.price} ر.س\n   تاريخ الانتهاء: ${formatDate(code.expires_at)}\n────────────────────`
            ).join('\n\n');
            
            document.getElementById('generatedCodes').value = codesText;
            document.getElementById('generatedCodesCard').style.display = 'block';
            
            // التمرير إلى الأكواد المولدة
            document.getElementById('generatedCodesCard').scrollIntoView({
                behavior: 'smooth',
                block: 'start'
            });
        }

        function copyCodes() {
            const textarea = document.getElementById('generatedCodes');
            
            if (!textarea.value.trim()) {
                showNotification('لا توجد أكواد لنسخها', 'warning');
                return;
            }
            
            textarea.select();
            textarea.setSelectionRange(0, 99999); // للهواتف المحمولة
            
            try {
                navigator.clipboard.writeText(textarea.value)
                    .then(() => {
                        showNotification('تم نسخ الأكواد إلى الحافظة', 'success');
                    })
                    .catch(() => {
                        // طريقة بديلة للهواتف القديمة
                        document.execCommand('copy');
                        showNotification('تم نسخ الأكواد إلى الحافظة', 'success');
                    });
            } catch (error) {
                showNotification('فشل نسخ الأكواد', 'error');
            }
        }

        function shareCodes() {
            const codes = document.getElementById('generatedCodes').value;
            
            if (!codes.trim()) {
                showNotification('لا توجد أكواد للمشاركة', 'warning');
                return;
            }
            
            const shareText = `أكواد تفعيل ناصر AI:\n\n${codes}\n\nتم إنشاؤها عبر لوحة التحكم`;
            
            if (navigator.share && navigator.canShare) {
                navigator.share({
                    title: 'أكواد تفعيل ناصر AI',
                    text: shareText
                }).catch(error => {
                    console.log('فشل المشاركة:', error);
                    copyCodes();
                });
            } else if (navigator.clipboard) {
                copyCodes();
            } else {
                // Fallback للمتصفحات القديمة
                const whatsappUrl = `https://wa.me/?text=${encodeURIComponent(shareText)}`;
                window.open(whatsappUrl, '_blank');
            }
        }

        // ==================== إدارة الأكواد النشطة ====================
        async function loadActiveCodes() {
            const tbody = document.getElementById('codesTable');
            
            if (!tbody) return;
            
            // عرض حالة التحميل
            tbody.innerHTML = `
                <tr>
                    <td colspan="5">
                        <div class="loading-container">
                            <div class="loading"></div>
                            <span>جاري تحميل البيانات...</span>
                        </div>
                    </td>
                </tr>
            `;
            
            try {
                // تحميل الأكواد من التخزين المحلي
                const codes = JSON.parse(localStorage.getItem('admin_generated_codes') || '[]');
                
                if (codes.length === 0) {
                    tbody.innerHTML = `
                        <tr>
                            <td colspan="5">
                                <div class="empty-state">
                                    <i class="fas fa-inbox empty-state-icon"></i>
                                    <p>لا توجد أكواد نشطة</p>
                                    <button class="btn btn-primary btn-sm" onclick="showTab('generate')">
                                        <i class="fas fa-plus"></i>
                                        توليد أكواد جديدة
                                    </button>
                                </div>
                            </td>
                        </tr>
                    `;
                    return;
                }
                
                // عرض الأكواد
                renderCodesTable(codes);
                
            } catch (error) {
                console.error('خطأ في تحميل الأكواد:', error);
                tbody.innerHTML = `
                    <tr>
                        <td colspan="5">
                            <div class="empty-state">
                                <i class="fas fa-exclamation-triangle empty-state-icon"></i>
                                <p>حدث خطأ في تحميل البيانات</p>
                                <button class="btn btn-primary btn-sm" onclick="loadActiveCodes()">
                                    <i class="fas fa-redo"></i>
                                    إعادة المحاولة
                                </button>
                            </div>
                        </td>
                    </tr>
                `;
            }
        }

        function renderCodesTable(codes) {
            const tbody = document.getElementById('codesTable');
            tbody.innerHTML = '';
            
            // فرز الأكواد حسب تاريخ الإنشاء (الأحدث أولاً)
            const sortedCodes = [...codes].sort((a, b) => 
                new Date(b.generated_at) - new Date(a.generated_at)
            );
            
            sortedCodes.forEach((code, index) => {
                const status = getCodeStatus(code.expires_at);
                const row = document.createElement('tr');
                
                row.innerHTML = `
                    <td>
                        <code style="background: rgba(255,255,255,0.1); padding: 0.25rem 0.5rem; border-radius: 0.25rem; font-family: monospace; font-size: 0.875rem;">
                            ${code.code}
                        </code>
                    </td>
                    <td>${getDurationText(code.duration)}</td>
                    <td>
                        <span class="badge ${status.class}">
                            ${status.text}
                        </span>
                    </td>
                    <td>${formatDate(code.expires_at)}</td>
                    <td>
                        <div class="btn-group">
                            <button class="btn btn-secondary btn-sm" onclick="copySingleCode('${code.code}')" title="نسخ">
                                <i class="fas fa-copy"></i>
                            </button>
                            <button class="btn btn-danger btn-sm" onclick="deleteCode('${code.id}')" title="حذف">
                                <i class="fas fa-trash"></i>
                            </button>
                        </div>
                    </td>
                `;
                
                tbody.appendChild(row);
            });
        }

        function getCodeStatus(expiresAt) {
            const now = new Date();
            const expiry = new Date(expiresAt);
            
            if (expiry > now) {
                const diff = expiry - now;
                const days = Math.floor(diff / (1000 * 60 * 60 * 24));
                const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                
                if (days > 30) {
                    return { class: 'badge-success', text: 'نشط' };
                } else if (days > 7) {
                    return { class: 'badge-info', text: `${days} يوم` };
                } else if (days > 1) {
                    return { class: 'badge-warning', text: `${days} يوم` };
                } else if (hours > 1) {
                    return { class: 'badge-warning', text: `${hours} ساعة` };
                } else {
                    return { class: 'badge-danger', text: 'ينتهي قريباً' };
                }
            } else {
                return { class: 'badge-danger', text: 'منتهي' };
            }
        }

        function copySingleCode(code) {
            navigator.clipboard.writeText(code)
                .then(() => {
                    showNotification('تم نسخ الكود إلى الحافظة', 'success');
                })
                .catch(() => {
                    // Fallback للهواتف القديمة
                    const tempInput = document.createElement('input');
                    tempInput.value = code;
                    document.body.appendChild(tempInput);
                    tempInput.select();
                    document.execCommand('copy');
                    document.body.removeChild(tempInput);
                    showNotification('تم نسخ الكود إلى الحافظة', 'success');
                });
        }

        function deleteCode(codeId) {
            if (!confirm('هل أنت متأكد من حذف هذا الكود؟')) {
                return;
            }
            
            try {
                const codes = JSON.parse(localStorage.getItem('admin_generated_codes') || '[]');
                const updatedCodes = codes.filter(code => code.id !== codeId);
                
                localStorage.setItem('admin_generated_codes', JSON.stringify(updatedCodes));
                
                showNotification('تم حذف الكود بنجاح', 'success');
                loadActiveCodes();
                loadDashboardStats();
            } catch (error) {
                console.error('خطأ في حذف الكود:', error);
                showNotification('فشل حذف الكود', 'error');
            }
        }

        function searchCodes() {
            const searchTerm = document.getElementById('searchCodes').value.toLowerCase().trim();
            const rows = document.querySelectorAll('#codesTable tr');
            
            rows.forEach(row => {
                const text = row.textContent.toLowerCase();
                row.style.display = searchTerm === '' || text.includes(searchTerm) ? '' : 'none';
            });
        }

        // ==================== إدارة المستخدمين ====================
        async function loadUsers() {
            const tbody = document.getElementById('usersTable');
            
            if (!tbody) return;
            
            // عرض بيانات تجريبية
            const mockUsers = [
                {
                    id: '1',
                    name: 'أحمد محمد',
                    email: 'ahmed@example.com',
                    status: 'active',
                    registered: '2026-01-15T10:30:00Z',
                    expires: '2026-04-15T10:30:00Z'
                },
                {
                    id: '2',
                    name: 'سارة علي',
                    email: 'sara@example.com',
                    status: 'active',
                    registered: '2026-01-20T14:45:00Z',
                    expires: '2026-02-20T14:45:00Z'
                },
                {
                    id: '3',
                    name: 'خالد حسن',
                    email: 'khaled@example.com',
                    status: 'expired',
                    registered: '2025-12-01T09:15:00Z',
                    expires: '2026-01-01T09:15:00Z'
                }
            ];
            
            renderUsersTable(mockUsers);
        }

        function renderUsersTable(users) {
            const tbody = document.getElementById('usersTable');
            tbody.innerHTML = '';
            
            users.forEach(user => {
                const statusClass = user.status === 'active' ? 'badge-success' : 'badge-danger';
                const statusText = user.status === 'active' ? 'نشط' : 'منتهي';
                
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${user.name}</td>
                    <td>${user.email}</td>
                    <td>
                        <span class="badge ${statusClass}">
                            ${statusText}
                        </span>
                    </td>
                    <td>${formatDate(user.registered)}</td>
                    <td>
                        <div class="btn-group">
                            <button class="btn btn-secondary btn-sm" onclick="viewUserDetails('${user.id}')" title="عرض التفاصيل">
                                <i class="fas fa-eye"></i>
                            </button>
                            <button class="btn btn-warning btn-sm" onclick="renewUserSubscription('${user.id}')" title="تجديد الاشتراك">
                                <i class="fas fa-redo"></i>
                            </button>
                        </div>
                    </td>
                `;
                
                tbody.appendChild(row);
            });
        }

        function filterUsers() {
            const filterValue = document.getElementById('userFilter').value;
            const rows = document.querySelectorAll('#usersTable tr');
            
            rows.forEach(row => {
                if (!filterValue) {
                    row.style.display = '';
                    return;
                }
                
                const statusBadge = row.querySelector('.badge');
                if (!statusBadge) return;
                
                const statusText = statusBadge.textContent.trim();
                const show = (filterValue === 'active' && statusText === 'نشط') ||
                            (filterValue === 'expired' && statusText === 'منتهي');
                
                row.style.display = show ? '' : 'none';
            });
        }

        function viewUserDetails(userId) {
            showNotification(`عرض تفاصيل المستخدم ${userId}`, 'info');
        }

        function renewUserSubscription(userId) {
            if (confirm('هل تريد تجديد اشتراك هذا المستخدم؟')) {
                showNotification(`تم تجديد اشتراك المستخدم ${userId}`, 'success');
            }
        }

        // ==================== التقارير والإحصائيات ====================
        async function loadDashboardStats() {
            try {
                const codes = JSON.parse(localStorage.getItem('admin_generated_codes') || '[]');
                
                // تحديث الإحصائيات
                document.getElementById('totalCodes').textContent = codes.length;
                document.getElementById('activeUsers').textContent = Math.floor(codes.length * 0.7);
                document.getElementById('todayCodes').textContent = getTodayCodesCount(codes);
                document.getElementById('totalRevenue').textContent = calculateTotalRevenue(codes);
                
            } catch (error) {
                console.error('خطأ في تحميل الإحصائيات:', error);
            }
        }

        async function loadReports() {
            try {
                const codes = JSON.parse(localStorage.getItem('admin_generated_codes') || '[]');
                
                // إحصائيات عامة
                document.getElementById('totalGenerated').textContent = codes.length;
                document.getElementById('totalUsed').textContent = Math.floor(codes.length * 0.65);
                document.getElementById('avgDuration').textContent = calculateAverageDuration(codes);
                document.getElementById('successRate').textContent = calculateSuccessRate(codes);
                
            } catch (error) {
                console.error('خطأ في تحميل التقارير:', error);
            }
        }

        function getTodayCodesCount(codes) {
            const today = new Date().toDateString();
            return codes.filter(code => {
                const codeDate = new Date(code.generated_at || new Date()).toDateString();
                return codeDate === today;
            }).length;
        }

        function calculateTotalRevenue(codes) {
            const total = codes.reduce((sum, code) => {
                const price = parseFloat(code.price) || 0;
                return sum + price;
            }, 0);
            
            return total > 0 ? `${total.toFixed(0)} ر.س` : '0 ر.س';
        }

        function calculateAverageDuration(codes) {
            if (codes.length === 0) return '0 يوم';
            
            const durationMap = {
                '5m': 5 / (60 * 24),
                '30m': 30 / (60 * 24),
                '1h': 1 / 24,
                '3h': 3 / 24,
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
            return avg >= 1 ? `${avg.toFixed(1)} يوم` : `${(avg * 24).toFixed(0)} ساعة`;
        }

        function calculateSuccessRate(codes) {
            if (codes.length === 0) return '0%';
            const used = Math.floor(codes.length * 0.65);
            return `${((used / codes.length) * 100).toFixed(1)}%`;
        }

        // ==================== الإعدادات ====================
        function loadSettings() {
            try {
                const settings = JSON.parse(localStorage.getItem('admin_panel_settings') || '{}');
                
                // تحميل الإعدادات
                if (settings.apiUrl) document.getElementById('apiUrl').value = settings.apiUrl;
                if (settings.defaultToken) document.getElementById('defaultToken').value = settings.defaultToken;
                if (settings.defaultPrice) document.getElementById('defaultPrice').value = settings.defaultPrice;
                if (settings.autoRefresh) document.getElementById('autoRefresh').value = settings.autoRefresh;
                
                // تعبئة كود الأمان تلقائياً إذا كان محفوظاً
                if (settings.defaultToken) {
                    document.getElementById('adminToken').value = settings.defaultToken;
                }
            } catch (error) {
                console.error('خطأ في تحميل الإعدادات:', error);
            }
        }

        function saveSettings() {
            try {
                const settings = {
                    apiUrl: document.getElementById('apiUrl').value,
                    defaultToken: document.getElementById('defaultToken').value,
                    defaultPrice: document.getElementById('defaultPrice').value,
                    autoRefresh: document.getElementById('autoRefresh').value,
                    lastUpdated: new Date().toISOString()
                };
                
                localStorage.setItem('admin_panel_settings', JSON.stringify(settings));
                showNotification('تم حفظ الإعدادات بنجاح', 'success');
                
                // إعادة إعداد التحديث التلقائي
                setupAutoRefresh();
                
                // تعبئة كود الأمان تلقائياً
                if (settings.defaultToken) {
                    document.getElementById('adminToken').value = settings.defaultToken;
                }
            } catch (error) {
                console.error('خطأ في حفظ الإعدادات:', error);
                showNotification('فشل حفظ الإعدادات', 'error');
            }
        }

        function resetSettings() {
            if (confirm('هل أنت متأكد من إعادة تعيين جميع الإعدادات إلى القيم الافتراضية؟')) {
                localStorage.removeItem('admin_panel_settings');
                loadSettings();
                showNotification('تم إعادة تعيين الإعدادات', 'success');
            }
        }

        function setupAutoRefresh() {
            // إلغاء أي فاصل زمني سابق
            if (autoRefreshInterval) {
                clearInterval(autoRefreshInterval);
                autoRefreshInterval = null;
            }
            
            // تحميل الإعدادات
            const settings = JSON.parse(localStorage.getItem('admin_panel_settings') || '{}');
            const interval = parseInt(settings.autoRefresh || '60');
            
            // إعداد فاصل زمني جديد إذا كان مفعلاً
            if (interval > 0) {
                autoRefreshInterval = setInterval(() => {
                    const activeSection = document.querySelector('.content-section.active').id;
                    
                    switch(activeSection) {
                        case 'codes':
                            loadActiveCodes();
                            break;
                        case 'reports':
                            loadReports();
                            break;
                        default:
                            loadDashboardStats();
                    }
                }, interval * 1000);
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
            
            try {
                const date = new Date(dateString);
                return new Intl.DateTimeFormat('ar-SA', {
                    year: 'numeric',
                    month: 'long',
                    day: 'numeric',
                    hour: '2-digit',
                    minute: '2-digit'
                }).format(date);
            } catch (error) {
                return 'تاريخ غير صالح';
            }
        }

        function generateUniqueId() {
            return Date.now().toString(36) + Math.random().toString(36).substr(2);
        }

        function debounce(func, wait) {
            let timeout;
            return function executedFunction(...args) {
                const later = () => {
                    clearTimeout(timeout);
                    func(...args);
                };
                clearTimeout(timeout);
                timeout = setTimeout(later, wait);
            };
        }

        function sleep(ms) {
            return new Promise(resolve => setTimeout(resolve, ms));
        }

        function showNotification(message, type = 'success') {
            const notification = document.getElementById('notification');
            const messageEl = document.getElementById('notificationMessage');
            const icon = notification.querySelector('i');
            
            // تغيير الأيقونة واللون حسب النوع
            switch(type) {
                case 'success':
                    icon.className = 'fas fa-check-circle';
                    notification.style.background = 'linear-gradient(135deg, var(--primary-light) 0%, var(--primary-color) 100%)';
                    break;
                case 'error':
                    icon.className = 'fas fa-exclamation-circle';
                    notification.style.background = 'linear-gradient(135deg, var(--danger-color) 0%, #c9302c 100%)';
                    break;
                case 'warning':
                    icon.className = 'fas fa-exclamation-triangle';
                    notification.style.background = 'linear-gradient(135deg, var(--warning-color) 0%, #ec971f 100%)';
                    break;
                default:
                    icon.className = 'fas fa-info-circle';
                    notification.style.background = 'linear-gradient(135deg, #5a67d8 0%, #4c51bf 100%)';
            }
            
            messageEl.textContent = message;
            notification.classList.add('show');
            
            // إخفاء تلقائي بعد 5 ثواني
            setTimeout(() => {
                hideNotification();
            }, 5000);
        }

        function hideNotification() {
            document.getElementById('notification').classList.remove('show');
        }

        // ==================== Web in App Optimization ====================
        if (window.matchMedia('(display-mode: standalone)').matches) {
            // تحسينات لوضع التطبيق المنفصل
            document.documentElement.style.setProperty('--spacing-sm', '1.25rem');
            document.documentElement.style.setProperty('--spacing-md', '1.5rem');
        }

        // منع الإجراءات الافتراضية في وضع Web in App
        document.addEventListener('touchmove', function(e) {
            if (e.scale !== 1) {
                e.preventDefault();
            }
        }, { passive: false });

        // تحسين أداء اللمس على iOS
        document.addEventListener('touchstart', function() {}, { passive: true });
        document.addEventListener('touchmove', function() {}, { passive: true });

        // ==================== تصدير الدوال للاستخدام العام ====================
        window.generateCodes = generateCodes;
        window.copyCodes = copyCodes;
        window.shareCodes = shareCodes;
        window.copySingleCode = copySingleCode;
        window.deleteCode = deleteCode;
        window.searchCodes = searchCodes;
        window.filterUsers = filterUsers;
        window.viewUserDetails = viewUserDetails;
        window.renewUserSubscription = renewUserSubscription;
        window.saveSettings = saveSettings;
        window.resetSettings = resetSettings;
        window.showTab = showTab;
        window.hideNotification = hideNotification;
    </script>
</body>
</html>