<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <meta name="theme-color" content="#044a35">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="format-detection" content="telephone=no">
    <title>لوحة تحكم الإدارة - ناصر AI</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
    <style>
        /* ========== CSS Reset شامل لجميع الأجهزة ========== */
        *, *::before, *::after {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
            -webkit-touch-callout: none;
            -webkit-user-select: none;
            user-select: none;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }

        :root {
            /* نظام الألوان */
            --primary-50: #e8f4f0;
            --primary-100: #d4ebe2;
            --primary-200: #a3d7c5;
            --primary-300: #72c3a8;
            --primary-400: #41af8b;
            --primary-500: #066d4d;
            --primary-600: #05553d;
            --primary-700: #044a35;
            --primary-800: #022e22;
            --primary-900: #011611;
            
            --secondary: #ffd166;
            --danger: #d9534f;
            --success: #25D366;
            --warning: #f0ad4e;
            --info: #4d96ff;
            --purple: #5a67d8;
            
            /* الخلفيات */
            --bg-body: #0a1929;
            --bg-card: rgba(255, 255, 255, 0.05);
            --bg-surface: rgba(255, 255, 255, 0.1);
            --bg-overlay: rgba(0, 0, 0, 0.7);
            
            /* النصوص */
            --text-primary: #ffffff;
            --text-secondary: rgba(255, 255, 255, 0.85);
            --text-muted: rgba(255, 255, 255, 0.6);
            --text-on-primary: #ffffff;
            
            /* الحدود */
            --border-light: rgba(255, 255, 255, 0.15);
            --border-medium: rgba(255, 255, 255, 0.25);
            --border-heavy: rgba(255, 255, 255, 0.35);
            
            /* الظلال */
            --shadow-sm: 0 1px 3px rgba(0, 0, 0, 0.12);
            --shadow-md: 0 4px 6px rgba(0, 0, 0, 0.15);
            --shadow-lg: 0 10px 25px rgba(0, 0, 0, 0.25);
            --shadow-xl: 0 20px 40px rgba(0, 0, 0, 0.3);
            
            /* المسافات (Systematic Spacing) */
            --space-0: 0;
            --space-1: 0.25rem;    /* 4px */
            --space-2: 0.5rem;     /* 8px */
            --space-3: 0.75rem;    /* 12px */
            --space-4: 1rem;       /* 16px */
            --space-5: 1.25rem;    /* 20px */
            --space-6: 1.5rem;     /* 24px */
            --space-8: 2rem;       /* 32px */
            --space-10: 2.5rem;    /* 40px */
            --space-12: 3rem;      /* 48px */
            --space-16: 4rem;      /* 64px */
            
            /* الأنصاف */
            --radius-xs: 0.25rem;  /* 4px */
            --radius-sm: 0.5rem;   /* 8px */
            --radius-md: 0.75rem;  /* 12px */
            --radius-lg: 1rem;     /* 16px */
            --radius-xl: 1.25rem;  /* 20px */
            --radius-2xl: 1.5rem;  /* 24px */
            --radius-3xl: 2rem;    /* 32px */
            --radius-full: 9999px;
            
            /* أحجام الخطوط (Fluid Typography) */
            --text-xs: clamp(0.75rem, 0.7rem + 0.25vw, 0.875rem);
            --text-sm: clamp(0.875rem, 0.825rem + 0.25vw, 1rem);
            --text-base: clamp(1rem, 0.95rem + 0.25vw, 1.125rem);
            --text-lg: clamp(1.125rem, 1.075rem + 0.25vw, 1.25rem);
            --text-xl: clamp(1.25rem, 1.2rem + 0.25vw, 1.5rem);
            --text-2xl: clamp(1.5rem, 1.4rem + 0.5vw, 1.875rem);
            --text-3xl: clamp(1.875rem, 1.775rem + 0.5vw, 2.25rem);
            --text-4xl: clamp(2.25rem, 2.15rem + 0.5vw, 2.5rem);
            
            /* التوقيتات */
            --duration-75: 75ms;
            --duration-100: 100ms;
            --duration-150: 150ms;
            --duration-200: 200ms;
            --duration-300: 300ms;
            --duration-500: 500ms;
            --duration-700: 700ms;
            
            /* الزوايا الآمنة للشاشات المختلفة */
            --safe-top: env(safe-area-inset-top);
            --safe-right: env(safe-area-inset-right);
            --safe-bottom: env(safe-area-inset-bottom);
            --safe-left: env(safe-area-inset-left);
        }

        /* ========== تحسينات عامة لجميع الأجهزة ========== */
        html {
            font-size: 100%;
            height: 100%;
            overflow-x: hidden;
            text-size-adjust: 100%;
            -webkit-text-size-adjust: 100%;
            -moz-text-size-adjust: 100%;
        }

        body {
            font-family: 'Cairo', -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Helvetica Neue', Arial, sans-serif;
            background: var(--bg-body);
            color: var(--text-primary);
            line-height: 1.5;
            min-height: 100vh;
            min-height: -webkit-fill-available;
            display: flex;
            flex-direction: column;
            overflow-x: hidden;
            position: relative;
        }

        /* إصلاح لحلقة التمرير المطاطية في iOS */
        body.ios-scroll-fix {
            position: fixed;
            width: 100%;
        }

        /* تحسينات اللمس للأندرويد */
        .android-touch-fix {
            -webkit-tap-highlight-color: rgba(0, 0, 0, 0.1);
        }

        /* ========== تحسينات خاصة لكل جهاز ========== */
        /* iPhone Notch Support */
        .iphone-notch {
            padding-top: constant(safe-area-inset-top);
            padding-top: env(safe-area-inset-top);
            padding-bottom: constant(safe-area-inset-bottom);
            padding-bottom: env(safe-area-inset-bottom);
        }

        /* iPhone SE و الأجهزة الصغيرة */
        @media only screen 
            and (device-width: 375px) 
            and (device-height: 667px) 
            and (-webkit-device-pixel-ratio: 2) {
            :root {
                --text-base: 15px;
            }
        }

        /* iPhone 12/13/14 Mini */
        @media only screen 
            and (device-width: 360px) 
            and (device-height: 780px) 
            and (-webkit-device-pixel-ratio: 3) {
            :root {
                --text-base: 15px;
            }
        }

        /* iPhone 13/14/15 Pro/Pro Max */
        @media only screen 
            and (device-width: 393px) 
            and (device-height: 852px) 
            and (-webkit-device-pixel-ratio: 3) {
            :root {
                --space-4: 1.125rem;
            }
        }

        /* iPhone 16/17 (توقع) */
        @media only screen 
            and (device-width: 430px) 
            and (device-height: 932px) 
            and (-webkit-device-pixel-ratio: 3) {
            :root {
                --space-4: 1.25rem;
            }
        }

        /* Samsung Galaxy S系列 */
        @media only screen 
            and (min-device-width: 360px) 
            and (max-device-width: 412px) {
            .android-optimize {
                -webkit-tap-highlight-color: rgba(255, 255, 255, 0.1);
            }
        }

        /* Samsung Galaxy Fold */
        @media only screen 
            and (device-width: 280px) 
            and (device-height: 653px) {
            :root {
                --text-base: 14px;
                --space-4: 0.875rem;
            }
        }

        /* Huawei و Xiaomi */
        @media only screen 
            and (-webkit-min-device-pixel-ratio: 3) 
            and (max-device-width: 480px) {
            .huawei-fix {
                font-weight: 500;
            }
        }

        /* OnePlus و Oppo */
        @media only screen 
            and (device-width: 412px) 
            and (device-height: 892px) {
            :root {
                --text-base: 15.5px;
            }
        }

        /* ========== Layout Principal ========== */
        .app-wrapper {
            flex: 1;
            width: 100%;
            max-width: 100%;
            margin: 0 auto;
            display: flex;
            flex-direction: column;
            position: relative;
            padding: 
                max(var(--space-4), var(--safe-top))
                max(var(--space-4), var(--safe-right))
                max(var(--space-4), var(--safe-bottom))
                max(var(--space-4), var(--safe-left));
        }

        /* ========== Header متكيف مع جميع الشاشات ========== */
        .app-header {
            background: linear-gradient(135deg, var(--primary-800) 0%, var(--primary-600) 100%);
            border-radius: var(--radius-xl);
            padding: var(--space-4);
            margin-bottom: var(--space-4);
            position: relative;
            overflow: hidden;
            border: 1px solid var(--border-light);
            box-shadow: var(--shadow-lg);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
        }

        .header-decoration {
            position: absolute;
            top: 0;
            right: 0;
            width: 150px;
            height: 150px;
            background: radial-gradient(circle at 30% 30%, var(--secondary) 0%, transparent 70%);
            opacity: 0.1;
            pointer-events: none;
        }

        .header-content {
            position: relative;
            z-index: 1;
            display: flex;
            flex-direction: column;
            gap: var(--space-3);
        }

        .header-title {
            display: flex;
            align-items: center;
            gap: var(--space-3);
            color: var(--secondary);
            font-size: var(--text-xl);
            font-weight: 800;
        }

        .header-subtitle {
            color: var(--text-secondary);
            font-size: var(--text-sm);
            line-height: 1.6;
        }

        .stats-container {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: var(--space-3);
            margin-top: var(--space-3);
        }

        .stat-item {
            background: var(--bg-surface);
            backdrop-filter: blur(10px);
            border: 1px solid var(--border-light);
            border-radius: var(--radius-lg);
            padding: var(--space-3);
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
            min-height: 80px;
            justify-content: center;
        }

        .stat-value {
            font-size: var(--text-xl);
            font-weight: 800;
            color: var(--info);
            margin-bottom: var(--space-1);
            line-height: 1.2;
        }

        .stat-label {
            font-size: var(--text-xs);
            color: var(--text-muted);
            line-height: 1.4;
        }

        /* ========== Navigation متجاوب للغاية ========== */
        .nav-scroll-wrapper {
            position: relative;
            width: 100%;
            overflow-x: auto;
            -webkit-overflow-scrolling: touch;
            scrollbar-width: none;
            margin-bottom: var(--space-4);
            padding: 0 var(--space-2);
        }

        .nav-scroll-wrapper::-webkit-scrollbar {
            display: none;
        }

        .nav-container {
            display: inline-flex;
            gap: var(--space-2);
            padding: var(--space-2);
            background: var(--bg-card);
            border-radius: var(--radius-xl);
            border: 1px solid var(--border-light);
            min-width: 100%;
            box-shadow: var(--shadow-sm);
        }

        .nav-button {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: var(--space-2);
            padding: var(--space-3) var(--space-4);
            background: transparent;
            border: none;
            border-radius: var(--radius-lg);
            color: var(--text-secondary);
            font-size: var(--text-xs);
            font-weight: 600;
            cursor: pointer;
            transition: all var(--duration-300) ease;
            min-width: 80px;
            min-height: 70px;
            flex-shrink: 0;
            touch-action: manipulation;
            -webkit-touch-callout: none;
        }

        .nav-button:active {
            transform: scale(0.95);
        }

        .nav-button.active {
            background: linear-gradient(135deg, var(--primary-500) 0%, var(--primary-700) 100%);
            color: var(--text-primary);
            box-shadow: var(--shadow-md);
            border: 1px solid var(--border-medium);
        }

        .nav-icon {
            font-size: 1.25rem;
            width: 24px;
            height: 24px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        /* ========== Content Sections ========== */
        .content-area {
            flex: 1;
            display: flex;
            flex-direction: column;
            gap: var(--space-4);
            overflow-y: auto;
            -webkit-overflow-scrolling: touch;
            padding-bottom: var(--space-6);
        }

        .content-section {
            display: none;
            flex-direction: column;
            gap: var(--space-4);
            animation: slideIn var(--duration-500) ease;
        }

        .content-section.active {
            display: flex;
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* ========== Cards متجاوبة مع جميع الأحجام ========== */
        .app-card {
            background: var(--bg-card);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid var(--border-light);
            border-radius: var(--radius-xl);
            padding: var(--space-4);
            display: flex;
            flex-direction: column;
            gap: var(--space-4);
            box-shadow: var(--shadow-lg);
            position: relative;
            overflow: hidden;
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            gap: var(--space-3);
            padding-bottom: var(--space-3);
            border-bottom: 1px solid var(--border-light);
        }

        .card-title {
            flex: 1;
            display: flex;
            flex-direction: column;
            gap: var(--space-1);
        }

        .card-heading {
            font-size: var(--text-lg);
            font-weight: 700;
            color: var(--secondary);
            line-height: 1.3;
        }

        .card-subheading {
            font-size: var(--text-sm);
            color: var(--text-muted);
            line-height: 1.5;
        }

        .card-icon {
            font-size: 1.5rem;
            color: var(--secondary);
            flex-shrink: 0;
        }

        /* ========== Form Elements بلمسات محسنة ========== */
        .form-group {
            display: flex;
            flex-direction: column;
            gap: var(--space-2);
        }

        .form-label {
            font-size: var(--text-sm);
            font-weight: 600;
            color: var(--info);
            display: flex;
            align-items: center;
            gap: var(--space-2);
        }

        .form-control {
            width: 100%;
            padding: var(--space-3) var(--space-4);
            background: var(--bg-surface);
            border: 1.5px solid var(--border-medium);
            border-radius: var(--radius-lg);
            color: var(--text-primary);
            font-size: var(--text-base);
            font-family: inherit;
            line-height: 1.5;
            transition: all var(--duration-300) ease;
            min-height: 52px;
            -webkit-appearance: none;
            appearance: none;
            touch-action: manipulation;
        }

        /* iOS خاص لإصلاح ارتفاع الحقول في */
        input.form-control,
        select.form-control,
        textarea.form-control {
            min-height: 52px;
            line-height: 1.5;
        }

        .form-control:focus {
            outline: none;
            border-color: var(--info);
            box-shadow: 0 0 0 3px rgba(77, 150, 255, 0.25);
            background: var(--bg-surface);
        }

        .form-control::placeholder {
            color: var(--text-muted);
            opacity: 0.8;
        }

        /* تحسين خاص لـ Android */
        .form-control.android-input {
            padding-top: var(--space-4);
            padding-bottom: var(--space-4);
        }

        /* تحسين خاص لـ iOS */
        .form-control.ios-input {
            -webkit-appearance: none;
            appearance: none;
        }

        select.form-control {
            background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='16' height='16' fill='%234d96ff' viewBox='0 0 16 16'%3E%3Cpath d='M7.247 11.14 2.451 5.658C1.885 5.013 2.345 4 3.204 4h9.592a1 1 0 0 1 .753 1.659l-4.796 5.48a1 1 0 0 1-1.506 0z'/%3E%3C/svg%3E");
            background-repeat: no-repeat;
            background-position: left var(--space-4) center;
            background-size: 16px;
            padding-left: 3rem;
        }

        textarea.form-control {
            min-height: 120px;
            resize: vertical;
            line-height: 1.6;
        }

        /* ========== Buttons محسنة لللمس ========== */
        .btn {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: var(--space-2);
            padding: var(--space-3) var(--space-4);
            border: none;
            border-radius: var(--radius-lg);
            font-size: var(--text-base);
            font-weight: 700;
            font-family: inherit;
            cursor: pointer;
            transition: all var(--duration-300) ease;
            text-decoration: none;
            min-height: 52px;
            width: 100%;
            touch-action: manipulation;
            position: relative;
            overflow: hidden;
            -webkit-tap-highlight-color: rgba(255, 255, 255, 0.1);
        }

        /* تحسين اللمس للأندرويد */
        .btn.android-btn:active {
            transform: scale(0.97);
        }

        /* تحسين اللمس لـ iOS */
        .btn.ios-btn:active {
            opacity: 0.8;
        }

        .btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none !important;
        }

        .btn::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
            transform: translateX(-100%);
        }

        .btn:active::after {
            animation: buttonShine 0.6s ease;
        }

        @keyframes buttonShine {
            to {
                transform: translateX(100%);
            }
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--primary-500) 0%, var(--primary-700) 100%);
            color: var(--text-primary);
            border: 1px solid var(--border-heavy);
        }

        .btn-secondary {
            background: linear-gradient(135deg, var(--purple) 0%, #4c51bf 100%);
            color: var(--text-primary);
            border: 1px solid var(--border-heavy);
        }

        .btn-success {
            background: linear-gradient(135deg, var(--success) 0%, #128C7E 100%);
            color: var(--text-primary);
            border: 1px solid var(--border-heavy);
        }

        .btn-danger {
            background: linear-gradient(135deg, var(--danger) 0%, #c9302c 100%);
            color: var(--text-primary);
            border: 1px solid var(--border-heavy);
        }

        .btn-warning {
            background: linear-gradient(135deg, var(--warning) 0%, #ec971f 100%);
            color: var(--text-primary);
            border: 1px solid var(--border-heavy);
        }

        .btn-sm {
            padding: var(--space-2) var(--space-3);
            font-size: var(--text-sm);
            min-height: 44px;
            width: auto;
        }

        .btn-group {
            display: flex;
            gap: var(--space-3);
            flex-wrap: wrap;
        }

        .btn-group-horizontal {
            flex-direction: row;
        }

        .btn-group-vertical {
            flex-direction: column;
        }

        /* ========== Duration Tags محسنة ========== */
        .duration-container {
            display: flex;
            flex-wrap: wrap;
            gap: var(--space-2);
        }

        .duration-tag {
            padding: var(--space-2) var(--space-3);
            background: rgba(77, 150, 255, 0.15);
            border: 1.5px solid rgba(77, 150, 255, 0.3);
            border-radius: var(--radius-full);
            font-size: var(--text-sm);
            color: var(--info);
            cursor: pointer;
            transition: all var(--duration-300) ease;
            flex-shrink: 0;
            min-height: 44px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            touch-action: manipulation;
        }

        .duration-tag:active {
            transform: scale(0.95);
        }

        .duration-tag.active {
            background: linear-gradient(135deg, var(--info) 0%, #2d7dfd 100%);
            color: var(--text-primary);
            border-color: var(--info);
            box-shadow: var(--shadow-md);
        }

        /* ========== Tables متجاوبة تماماً ========== */
        .table-responsive {
            width: 100%;
            overflow-x: auto;
            -webkit-overflow-scrolling: touch;
            border-radius: var(--radius-lg);
            border: 1px solid var(--border-light);
            background: var(--bg-surface);
            margin-top: var(--space-4);
        }

        .data-table {
            width: 100%;
            border-collapse: collapse;
            min-width: 600px;
        }

        .data-table th {
            padding: var(--space-3);
            text-align: right;
            font-weight: 700;
            color: var(--secondary);
            background: rgba(255, 255, 255, 0.05);
            border-bottom: 1px solid var(--border-light);
            font-size: var(--text-sm);
            white-space: nowrap;
            position: sticky;
            top: 0;
            backdrop-filter: blur(10px);
        }

        .data-table td {
            padding: var(--space-3);
            border-bottom: 1px solid var(--border-light);
            font-size: var(--text-sm);
            line-height: 1.6;
        }

        .data-table tr:last-child td {
            border-bottom: none;
        }

        .data-table tr:hover {
            background: rgba(255, 255, 255, 0.02);
        }

        /* ========== Badges متجاوبة ========== */
        .badge {
            display: inline-flex;
            align-items: center;
            padding: var(--space-1) var(--space-3);
            border-radius: var(--radius-full);
            font-size: var(--text-xs);
            font-weight: 700;
            text-align: center;
            white-space: nowrap;
        }

        .badge-success {
            background: rgba(37, 211, 102, 0.2);
            color: var(--success);
            border: 1px solid rgba(37, 211, 102, 0.3);
        }

        .badge-warning {
            background: rgba(240, 173, 78, 0.2);
            color: var(--warning);
            border: 1px solid rgba(240, 173, 78, 0.3);
        }

        .badge-danger {
            background: rgba(217, 83, 79, 0.2);
            color: var(--danger);
            border: 1px solid rgba(217, 83, 79, 0.3);
        }

        .badge-info {
            background: rgba(77, 150, 255, 0.2);
            color: var(--info);
            border: 1px solid rgba(77, 150, 255, 0.3);
        }

        /* ========== Notifications محسنة ========== */
        .notification-wrapper {
            position: fixed;
            top: max(var(--space-4), var(--safe-top));
            right: max(var(--space-4), var(--safe-right));
            left: max(var(--space-4), var(--safe-left));
            z-index: 9999;
            pointer-events: none;
            max-width: 500px;
            margin: 0 auto;
        }

        .notification {
            background: linear-gradient(135deg, var(--primary-500) 0%, var(--primary-700) 100%);
            color: var(--text-primary);
            padding: var(--space-3) var(--space-4);
            border-radius: var(--radius-lg);
            box-shadow: var(--shadow-xl);
            display: flex;
            align-items: center;
            justify-content: space-between;
            transform: translateY(-100%);
            opacity: 0;
            transition: all var(--duration-500) cubic-bezier(0.68, -0.55, 0.27, 1.55);
            pointer-events: all;
            border: 1px solid var(--border-medium);
            backdrop-filter: blur(20px);
        }

        .notification.show {
            transform: translateY(0);
            opacity: 1;
        }

        .notification-content {
            display: flex;
            align-items: center;
            gap: var(--space-3);
            flex: 1;
        }

        .notification-icon {
            font-size: 1.25rem;
            flex-shrink: 0;
        }

        .notification-message {
            font-size: var(--text-sm);
            line-height: 1.5;
            flex: 1;
        }

        .notification-close {
            background: none;
            border: none;
            color: inherit;
            font-size: 1.5rem;
            cursor: pointer;
            padding: var(--space-1);
            min-width: 44px;
            min-height: 44px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: var(--radius-full);
            transition: background var(--duration-200) ease;
            flex-shrink: 0;
            touch-action: manipulation;
        }

        .notification-close:active {
            background: rgba(255, 255, 255, 0.1);
        }

        /* ========== Loading States ========== */
        .loading {
            display: inline-block;
            width: 24px;
            height: 24px;
            border: 3px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top-color: var(--info);
            animation: spin 1s linear infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        .loading-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: var(--space-3);
            padding: var(--space-8) var(--space-4);
            color: var(--text-muted);
            text-align: center;
        }

        /* ========== Empty States ========== */
        .empty-state {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: var(--space-3);
            padding: var(--space-8) var(--space-4);
            text-align: center;
            color: var(--text-muted);
        }

        .empty-icon {
            font-size: 3rem;
            opacity: 0.3;
            margin-bottom: var(--space-2);
        }

        .empty-title {
            font-size: var(--text-lg);
            font-weight: 600;
            color: var(--text-secondary);
        }

        .empty-description {
            font-size: var(--text-sm);
            line-height: 1.6;
            max-width: 300px;
        }

        /* ========== Search and Filters ========== */
        .search-container {
            position: relative;
            margin-bottom: var(--space-4);
        }

        .search-input {
            width: 100%;
            padding: var(--space-3) var(--space-4) var(--space-3) 3rem;
            background: var(--bg-surface);
            border: 1.5px solid var(--border-medium);
            border-radius: var(--radius-lg);
            color: var(--text-primary);
            font-size: var(--text-base);
            min-height: 52px;
            line-height: 1.5;
        }

        .search-icon {
            position: absolute;
            left: var(--space-4);
            top: 50%;
            transform: translateY(-50%);
            color: var(--text-muted);
            pointer-events: none;
        }

        .filters-container {
            display: flex;
            gap: var(--space-3);
            margin-bottom: var(--space-4);
            flex-wrap: wrap;
        }

        .filter-select {
            flex: 1;
            min-width: 140px;
        }

        /* ========== تحسينات للأجهزة الكبيرة ========== */
        @media (min-width: 375px) {
            .stats-container {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .nav-button {
                min-width: 85px;
            }
        }

        @media (min-width: 414px) {
            .stats-container {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .nav-button {
                min-width: 90px;
                min-height: 75px;
            }
            
            .form-control {
                min-height: 56px;
            }
            
            .btn {
                min-height: 56px;
            }
        }

        @media (min-width: 480px) {
            .stats-container {
                grid-template-columns: repeat(4, 1fr);
            }
            
            .nav-container {
                justify-content: center;
            }
            
            .nav-button {
                flex: 1;
                min-width: auto;
                min-height: 80px;
            }
            
            .btn-group-horizontal .btn {
                width: auto;
                flex: 1;
            }
        }

        @media (min-width: 768px) {
            .app-wrapper {
                max-width: 768px;
                padding: 
                    max(var(--space-6), var(--safe-top))
                    max(var(--space-6), var(--safe-right))
                    max(var(--space-6), var(--safe-bottom))
                    max(var(--space-6), var(--safe-left));
            }
            
            .app-header {
                padding: var(--space-6);
            }
            
            .stat-item {
                padding: var(--space-4);
                min-height: 100px;
            }
            
            .stat-value {
                font-size: var(--text-2xl);
            }
            
            .form-row {
                display: grid;
                grid-template-columns: repeat(2, 1fr);
                gap: var(--space-4);
            }
        }

        @media (min-width: 1024px) {
            .app-wrapper {
                max-width: 1024px;
                padding: 
                    max(var(--space-8), var(--safe-top))
                    max(var(--space-8), var(--safe-right))
                    max(var(--space-8), var(--safe-bottom))
                    max(var(--space-8), var(--safe-left));
            }
            
            .content-layout {
                display: grid;
                grid-template-columns: 280px 1fr;
                gap: var(--space-6);
                align-items: start;
            }
            
            .nav-scroll-wrapper {
                position: sticky;
                top: var(--space-6);
                height: fit-content;
            }
            
            .nav-container {
                flex-direction: column;
                min-width: auto;
                padding: var(--space-4);
            }
            
            .nav-button {
                min-width: 100%;
                min-height: 85px;
                flex-direction: row;
                justify-content: flex-start;
                padding: var(--space-4);
                font-size: var(--text-sm);
            }
            
            .nav-icon {
                font-size: 1.5rem;
                width: 28px;
                height: 28px;
            }
        }

        /* ========== High DPI Screens ========== */
        @media (-webkit-min-device-pixel-ratio: 2), (min-resolution: 192dpi) {
            .app-card,
            .stat-item,
            .nav-container {
                border-width: 0.5px;
            }
        }

        @media (-webkit-min-device-pixel-ratio: 3), (min-resolution: 288dpi) {
            .app-card,
            .stat-item,
            .nav-container {
                border-width: 0.33px;
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
                scroll-behavior: auto !important;
            }
        }

        @media (prefers-contrast: high) {
            :root {
                --border-light: rgba(255, 255, 255, 0.5);
                --border-medium: rgba(255, 255, 255, 0.8);
            }
            
            .btn {
                border-width: 2px;
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

        /* ========== تحسينات خاصة للعرض في التطبيقات ========== */
        .web-in-app {
            /* إصلاحات للعرض في WebView */
            -webkit-overflow-scrolling: touch;
            overscroll-behavior: contain;
        }

        /* إصلاح ارتفاع الشاشة في iOS Safari */
        @supports (-webkit-touch-callout: none) {
            body {
                height: -webkit-fill-available;
            }
            
            .app-wrapper {
                min-height: -webkit-fill-available;
            }
        }

        /* إصلاحات للمتصفحات المختلفة */
        @supports (padding: max(0px)) {
            .app-wrapper {
                padding-top: max(env(safe-area-inset-top), var(--space-4));
                padding-bottom: max(env(safe-area-inset-bottom), var(--space-4));
            }
        }

        /* Dark Mode Support */
        @media (prefers-color-scheme: dark) {
            :root {
                --bg-body: #0a1929;
                --text-primary: #ffffff;
            }
        }

        @media (prefers-color-scheme: light) {
            :root {
                --bg-body: #f8fafc;
                --bg-card: rgba(255, 255, 255, 0.9);
                --bg-surface: rgba(255, 255, 255, 0.95);
                --text-primary: #1e293b;
                --text-secondary: #475569;
                --text-muted: #64748b;
                --border-light: rgba(0, 0, 0, 0.1);
                --border-medium: rgba(0, 0, 0, 0.2);
            }
            
            .app-header {
                border: 1px solid rgba(255, 255, 255, 0.2);
            }
            
            .notification {
                border: 1px solid rgba(255, 255, 255, 0.2);
            }
        }
    </style>
</head>
<body class="web-in-app">
    <div class="app-wrapper">
        <!-- Header -->
        <header class="app-header">
            <div class="header-decoration"></div>
            <div class="header-content">
                <h1 class="header-title">
                    <i class="fas fa-user-shield"></i>
                    لوحة تحكم الإدارة
                </h1>
                <p class="header-subtitle">إدارة النظام وتوليد أكواد التفعيل والتحكم بالمستخدمين</p>
                
                <div class="stats-container">
                    <div class="stat-item">
                        <div class="stat-value" id="totalCodes">0</div>
                        <div class="stat-label">الأكواد النشطة</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value" id="activeUsers">0</div>
                        <div class="stat-label">المستخدمين النشطين</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value" id="totalRevenue">0 ر.س</div>
                        <div class="stat-label">إجمالي الإيرادات</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value" id="todayCodes">0</div>
                        <div class="stat-label">أكواد اليوم</div>
                    </div>
                </div>
            </div>
        </header>

        <!-- Navigation -->
        <div class="nav-scroll-wrapper">
            <nav class="nav-container">
                <button class="nav-button active" data-tab="generate">
                    <i class="fas fa-key nav-icon"></i>
                    <span>توليد أكواد</span>
                </button>
                <button class="nav-button" data-tab="codes">
                    <i class="fas fa-list nav-icon"></i>
                    <span>الأكواد النشطة</span>
                </button>
                <button class="nav-button" data-tab="users">
                    <i class="fas fa-users nav-icon"></i>
                    <span>المستخدمين</span>
                </button>
                <button class="nav-button" data-tab="reports">
                    <i class="fas fa-chart-bar nav-icon"></i>
                    <span>التقارير</span>
                </button>
                <button class="nav-button" data-tab="settings">
                    <i class="fas fa-cog nav-icon"></i>
                    <span>الإعدادات</span>
                </button>
            </nav>
        </div>

        <!-- Main Content -->
        <main class="content-area">
            <!-- Generate Codes Section -->
            <section id="generate" class="content-section active">
                <div class="app-card">
                    <div class="card-header">
                        <div class="card-title">
                            <h2 class="card-heading">توليد كود تفعيل جديد</h2>
                            <p class="card-subheading">اختر المدة الزمنية وانقر على توليد</p>
                        </div>
                        <i class="fas fa-key card-icon"></i>
                    </div>

                    <form id="generateForm">
                        <div class="form-group">
                            <label class="form-label">
                                <i class="fas fa-clock"></i>
                                مدة التفعيل
                            </label>
                            <div class="duration-container" id="durationTags">
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

                        <div class="form-row">
                            <div class="form-group">
                                <label for="codeCount" class="form-label">
                                    <i class="fas fa-hashtag"></i>
                                    عدد الأكواد
                                </label>
                                <select id="codeCount" class="form-control" required>
                                    <option value="1">1 كود</option>
                                    <option value="5">5 أكواد</option>
                                    <option value="10">10 أكواد</option>
                                    <option value="20">20 كود</option>
                                    <option value="50">50 كود</option>
                                </select>
                            </div>

                            <div class="form-group">
                                <label for="price" class="form-label">
                                    <i class="fas fa-money-bill"></i>
                                    السعر (اختياري)
                                </label>
                                <input type="number" id="price" class="form-control" placeholder="أدخل السعر بالريال" min="0" step="1">
                            </div>
                        </div>

                        <div class="form-group">
                            <label for="adminToken" class="form-label">
                                <i class="fas fa-lock"></i>
                                كود الأمان (ADMIN_TOKEN)
                            </label>
                            <input type="password" id="adminToken" class="form-control" placeholder="أدخل كود الأمان" required>
                        </div>

                        <button type="button" class="btn btn-success" onclick="generateCodes()">
                            <i class="fas fa-bolt"></i>
                            توليد الأكواد
                        </button>
                    </form>
                </div>

                <div class="app-card" id="generatedCodesCard" style="display: none;">
                    <div class="card-header">
                        <div class="card-title">
                            <h2 class="card-heading">الأكواد المولدة</h2>
                            <p class="card-subheading">انسخ الأكواد أو أرسلها مباشرة</p>
                        </div>
                        <i class="fas fa-copy card-icon"></i>
                    </div>

                    <div class="form-group">
                        <label class="form-label">الأكواد المولدة:</label>
                        <textarea id="generatedCodes" class="form-control" rows="6" readonly style="font-family: 'Courier New', monospace;"></textarea>
                    </div>

                    <div class="btn-group btn-group-horizontal">
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

            <!-- Active Codes Section -->
            <section id="codes" class="content-section">
                <div class="app-card">
                    <div class="card-header">
                        <div class="card-title">
                            <h2 class="card-heading">الأكواد النشطة</h2>
                            <p class="card-subheading">إدارة وتتبع جميع أكواد التفعيل</p>
                        </div>
                        <div class="search-container">
                            <input type="text" id="searchCodes" class="search-input" placeholder="ابحث في الأكواد...">
                            <i class="fas fa-search search-icon"></i>
                        </div>
                    </div>

                    <div class="table-responsive">
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

            <!-- Users Section -->
            <section id="users" class="content-section">
                <div class="app-card">
                    <div class="card-header">
                        <div class="card-title">
                            <h2 class="card-heading">المستخدمين النشطين</h2>
                            <p class="card-subheading">عرض وإدارة حسابات المستخدمين</p>
                        </div>
                        <div class="filters-container">
                            <select id="userFilter" class="form-control filter-select" onchange="filterUsers()">
                                <option value="">جميع المستخدمين</option>
                                <option value="active">النشطين فقط</option>
                                <option value="expired">المنتهية صلاحيتهم</option>
                            </select>
                        </div>
                    </div>

                    <div class="table-responsive">
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

            <!-- Reports Section -->
            <section id="reports" class="content-section">
                <div class="app-card">
                    <div class="card-header">
                        <div class="card-title">
                            <h2 class="card-heading">تقارير النظام</h2>
                            <p class="card-subheading">إحصائيات وأداء النظام</p>
                        </div>
                        <i class="fas fa-chart-line card-icon"></i>
                    </div>

                    <div class="stats-container">
                        <div class="stat-item">
                            <div class="stat-value" id="totalGenerated">0</div>
                            <div class="stat-label">إجمالي الأكواد المولدة</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-value" id="totalUsed">0</div>
                            <div class="stat-label">الأكواد المستخدمة</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-value" id="avgDuration">0 يوم</div>
                            <div class="stat-label">متوسط المدة</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-value" id="successRate">0%</div>
                            <div class="stat-label">معدل النجاح</div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Settings Section -->
            <section id="settings" class="content-section">
                <div class="app-card">
                    <div class="card-header">
                        <div class="card-title">
                            <h2 class="card-heading">إعدادات النظام</h2>
                            <p class="card-subheading">تخصيص وتكوين النظام</p>
                        </div>
                        <i class="fas fa-sliders-h card-icon"></i>
                    </div>

                    <form id="settingsForm">
                        <div class="form-group">
                            <label for="apiUrl" class="form-label">
                                <i class="fas fa-server"></i>
                                عنوان الـ API
                            </label>
                            <input type="text" id="apiUrl" class="form-control" value="https://tarafbackend.onrender.com" readonly>
                            <small style="display: block; margin-top: var(--space-1); color: var(--text-muted);">
                                عنوان خادم الباك إند
                            </small>
                        </div>

                        <div class="form-row">
                            <div class="form-group">
                                <label for="defaultToken" class="form-label">
                                    <i class="fas fa-key"></i>
                                    كود الأمان الافتراضي
                                </label>
                                <input type="password" id="defaultToken" class="form-control" placeholder="أدخل كود الأمان الافتراضي">
                            </div>

                            <div class="form-group">
                                <label for="defaultPrice" class="form-label">
                                    <i class="fas fa-money-bill-wave"></i>
                                    السعر الافتراضي
                                </label>
                                <input type="number" id="defaultPrice" class="form-control" placeholder="السعر الافتراضي بالريال">
                            </div>
                        </div>

                        <div class="form-group">
                            <label for="autoRefresh" class="form-label">
                                <i class="fas fa-sync"></i>
                                تحديث البيانات تلقائياً
                            </label>
                            <select id="autoRefresh" class="form-control">
                                <option value="30">كل 30 ثانية</option>
                                <option value="60">كل دقيقة</option>
                                <option value="300">كل 5 دقائق</option>
                                <option value="0">غير مفعل</option>
                            </select>
                        </div>

                        <div class="btn-group btn-group-horizontal">
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
    <div class="notification-wrapper">
        <div class="notification" id="notification">
            <div class="notification-content">
                <i class="fas fa-check-circle notification-icon"></i>
                <span id="notificationMessage" class="notification-message">تمت العملية بنجاح</span>
            </div>
            <button class="notification-close" onclick="hideNotification()" aria-label="إغلاق">
                ×
            </button>
        </div>
    </div>

    <script>
        // ========== Device Detection and Optimization ==========
        class DeviceOptimizer {
            constructor() {
                this.init();
            }
            
            init() {
                this.detectDevice();
                this.applyOptimizations();
                this.setupViewport();
            }
            
            detectDevice() {
                const ua = navigator.userAgent;
                
                // iOS Detection
                this.isIOS = /iPad|iPhone|iPod/.test(ua) && !window.MSStream;
                this.isIPhone = /iPhone/.test(ua);
                this.isIPad = /iPad/.test(ua);
                
                // Android Detection
                this.isAndroid = /Android/.test(ua);
                this.isChrome = /Chrome/.test(ua);
                this.isSamsung = /Samsung/.test(ua);
                this.isHuawei = /Huawei/.test(ua);
                this.isXiaomi = /Mi|Redmi|Xiaomi/.test(ua);
                
                // Screen Size Detection
                this.screenWidth = window.screen.width;
                this.screenHeight = window.screen.height;
                this.pixelRatio = window.devicePixelRatio;
                
                // Notch Detection
                this.hasNotch = this.isIOS && (this.screenHeight >= 812 && this.screenWidth >= 375);
                
                // Foldable Detection
                this.isFoldable = window.matchMedia('(horizontal-viewport-segments: 2)').matches ||
                                 window.matchMedia('(vertical-viewport-segments: 2)').matches;
            }
            
            applyOptimizations() {
                // iOS Optimizations
                if (this.isIOS) {
                    document.body.classList.add('ios-device');
                    
                    // Add iOS specific classes
                    document.querySelectorAll('.form-control').forEach(el => {
                        el.classList.add('ios-input');
                    });
                    
                    document.querySelectorAll('.btn').forEach(el => {
                        el.classList.add('ios-btn');
                    });
                    
                    // Fix for iOS bounce
                    document.body.style.overflow = 'hidden';
                    document.body.style.position = 'fixed';
                    document.body.style.width = '100%';
                }
                
                // Android Optimizations
                if (this.isAndroid) {
                    document.body.classList.add('android-device', 'android-touch-fix');
                    
                    document.querySelectorAll('.form-control').forEach(el => {
                        el.classList.add('android-input');
                    });
                    
                    document.querySelectorAll('.btn').forEach(el => {
                        el.classList.add('android-btn');
                    });
                    
                    // Samsung specific
                    if (this.isSamsung) {
                        document.body.classList.add('samsung-device');
                    }
                    
                    // Huawei specific
                    if (this.isHuawei) {
                        document.body.classList.add('huawei-device', 'huawei-fix');
                    }
                    
                    // Xiaomi specific
                    if (this.isXiaomi) {
                        document.body.classList.add('xiaomi-device');
                    }
                }
                
                // Apply notch padding
                if (this.hasNotch) {
                    document.body.classList.add('iphone-notch');
                }
                
                // Apply foldable optimizations
                if (this.isFoldable) {
                    document.body.classList.add('foldable-device');
                }
            }
            
            setupViewport() {
                // Prevent zoom on input focus for iOS
                if (this.isIOS) {
                    document.addEventListener('touchstart', (e) => {
                        if (e.target.tagName === 'INPUT' || e.target.tagName === 'TEXTAREA' || e.target.tagName === 'SELECT') {
                            document.body.style.zoom = '100%';
                        }
                    });
                    
                    document.addEventListener('focusin', (e) => {
                        if (e.target.tagName === 'INPUT' || e.target.tagName === 'TEXTAREA' || e.target.tagName === 'SELECT') {
                            setTimeout(() => {
                                e.target.scrollIntoView({ behavior: 'smooth', block: 'center' });
                            }, 300);
                        }
                    });
                }
                
                // Android viewport fixes
                if (this.isAndroid) {
                    const viewport = document.querySelector('meta[name="viewport"]');
                    if (viewport) {
                        viewport.content = 'width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover, shrink-to-fit=no';
                    }
                }
            }
            
            getDeviceInfo() {
                return {
                    isIOS: this.isIOS,
                    isAndroid: this.isAndroid,
                    isIPhone: this.isIPhone,
                    isIPad: this.isIPad,
                    hasNotch: this.hasNotch,
                    screenWidth: this.screenWidth,
                    screenHeight: this.screenHeight,
                    pixelRatio: this.pixelRatio,
                    userAgent: navigator.userAgent
                };
            }
        }

        // ========== Main Application ==========
        const API_BASE_URL = "https://tarafbackend.onrender.com";
        let currentDuration = "1d";
        let autoRefreshInterval = null;
        let deviceOptimizer;

        // Initialize when DOM is loaded
        document.addEventListener('DOMContentLoaded', function() {
            initializeApplication();
        });

        function initializeApplication() {
            // Initialize device optimizer
            deviceOptimizer = new DeviceOptimizer();
            console.log('Device Info:', deviceOptimizer.getDeviceInfo());
            
            // Setup event listeners
            setupEventListeners();
            
            // Load settings
            loadSettings();
            
            // Setup duration tags
            setupDurationTags();
            
            // Load initial data
            loadDashboardStats();
            
            // Setup auto refresh
            setupAutoRefresh();
            
            // Apply device-specific optimizations
            applyDeviceSpecificOptimizations();
            
            // Prevent default touch behaviors
            preventDefaultTouchBehaviors();
        }

        function applyDeviceSpecificOptimizations() {
            const deviceInfo = deviceOptimizer.getDeviceInfo();
            
            // iPhone specific optimizations
            if (deviceInfo.isIPhone) {
                // Adjust for different iPhone models
                if (deviceInfo.screenWidth === 375) { // iPhone 12/13 mini, iPhone SE
                    document.documentElement.style.setProperty('--space-4', '0.875rem');
                } else if (deviceInfo.screenWidth === 390) { // iPhone 12/13
                    document.documentElement.style.setProperty('--space-4', '1rem');
                } else if (deviceInfo.screenWidth === 393) { // iPhone 14/15
                    document.documentElement.style.setProperty('--space-4', '1.125rem');
                } else if (deviceInfo.screenWidth === 430) { // iPhone 14 Pro Max / 15 Pro Max
                    document.documentElement.style.setProperty('--space-4', '1.25rem');
                }
                
                // High pixel ratio adjustments
                if (deviceInfo.pixelRatio >= 3) {
                    document.body.classList.add('high-dpi');
                }
            }
            
            // Android specific optimizations
            if (deviceInfo.isAndroid) {
                // Adjust for common Android screen sizes
                if (deviceInfo.screenWidth <= 360) { // Small Android devices
                    document.documentElement.style.setProperty('--text-base', '15px');
                } else if (deviceInfo.screenWidth >= 412) { // Large Android devices
                    document.documentElement.style.setProperty('--space-4', '1.125rem');
                }
            }
        }

        function preventDefaultTouchBehaviors() {
            // Prevent bounce on iOS
            document.addEventListener('touchmove', function(e) {
                if (e.scale !== 1) {
                    e.preventDefault();
                }
            }, { passive: false });
            
            // Prevent double tap zoom
            let lastTouchEnd = 0;
            document.addEventListener('touchend', function(e) {
                const now = Date.now();
                if (now - lastTouchEnd <= 300) {
                    e.preventDefault();
                }
                lastTouchEnd = now;
            }, { passive: false });
            
            // Prevent pull-to-refresh
            document.addEventListener('touchstart', function(e) {
                if (e.touches.length !== 1) return;
                
                const touch = e.touches[0];
                if (touch.clientY <= 10) {
                    e.preventDefault();
                }
            }, { passive: false });
        }

        // ... باقي الدوال كما هي مع بعض التحسينات الإضافية

        function setupEventListeners() {
            // Navigation
            document.querySelectorAll('.nav-button').forEach(button => {
                button.addEventListener('click', function(e) {
                    e.preventDefault();
                    const tabId = this.dataset.tab;
                    showTab(tabId);
                    
                    // Add touch feedback
                    this.classList.add('active-touch');
                    setTimeout(() => {
                        this.classList.remove('active-touch');
                    }, 200);
                });
                
                // Add touch feedback for mobile
                button.addEventListener('touchstart', function() {
                    this.classList.add('touch-active');
                });
                
                button.addEventListener('touchend', function() {
                    this.classList.remove('touch-active');
                });
            });
            
            // Form inputs
            document.querySelectorAll('.form-control').forEach(input => {
                // iOS specific input handling
                if (deviceOptimizer.isIOS) {
                    input.addEventListener('focus', function() {
                        setTimeout(() => {
                            this.scrollIntoView({ behavior: 'smooth', block: 'center' });
                        }, 100);
                    });
                }
                
                // Android specific input handling
                if (deviceOptimizer.isAndroid) {
                    input.addEventListener('touchstart', function() {
                        this.style.transform = 'scale(0.99)';
                    });
                    
                    input.addEventListener('touchend', function() {
                        this.style.transform = '';
                    });
                }
            });
            
            // Buttons touch feedback
            document.querySelectorAll('.btn').forEach(button => {
                button.addEventListener('touchstart', function() {
                    this.style.opacity = '0.9';
                });
                
                button.addEventListener('touchend', function() {
                    this.style.opacity = '';
                });
            });
            
            // Search functionality
            const searchInput = document.getElementById('searchCodes');
            if (searchInput) {
                searchInput.addEventListener('input', debounce(function() {
                    searchCodes(this.value);
                }, 300));
                
                // Prevent keyboard from pushing content on iOS
                if (deviceOptimizer.isIOS) {
                    searchInput.addEventListener('focus', function() {
                        setTimeout(() => {
                            document.body.scrollTop = 0;
                        }, 100);
                    });
                }
            }
            
            // Handle orientation changes
            window.addEventListener('orientationchange', function() {
                setTimeout(() => {
                    window.scrollTo(0, 0);
                    // Re-apply optimizations for new orientation
                    applyDeviceSpecificOptimizations();
                }, 300);
            });
            
            // Handle resize events
            let resizeTimeout;
            window.addEventListener('resize', function() {
                clearTimeout(resizeTimeout);
                resizeTimeout = setTimeout(() => {
                    applyDeviceSpecificOptimizations();
                }, 250);
            });
        }

        // ... باقي الدوال (showTab, setupDurationTags, generateCodes, etc.) 
        // تبقى كما هي مع تحسينات إضافية للتوافق

        function showTab(tabId) {
            // Hide all content sections
            document.querySelectorAll('.content-section').forEach(section => {
                section.style.display = 'none';
                section.classList.remove('active');
            });
            
            // Deactivate all nav buttons
            document.querySelectorAll('.nav-button').forEach(button => {
                button.classList.remove('active');
            });
            
            // Show target section
            const targetSection = document.getElementById(tabId);
            if (targetSection) {
                targetSection.style.display = 'flex';
                setTimeout(() => {
                    targetSection.classList.add('active');
                }, 10);
                
                // Activate corresponding nav button
                document.querySelector(`[data-tab="${tabId}"]`).classList.add('active');
                
                // Load tab data
                loadTabData(tabId);
                
                // Scroll to top for mobile
                if (window.innerWidth < 768) {
                    window.scrollTo({ top: 0, behavior: 'smooth' });
                }
            }
        }

        function generateCodes() {
            const adminToken = document.getElementById('adminToken').value.trim();
            const codeCount = parseInt(document.getElementById('codeCount').value);
            const price = document.getElementById('price').value;
            
            // Validation
            if (!adminToken) {
                showNotification('يرجى إدخال كود الأمان', 'error');
                return;
            }
            
            if (codeCount < 1 || codeCount > 50) {
                showNotification('عدد الأكواد يجب أن يكون بين 1 و 50', 'error');
                return;
            }
            
            // Show loading state with device-specific feedback
            const generateBtn = document.querySelector('#generate .btn-success');
            const originalContent = generateBtn.innerHTML;
            
            // Device-specific loading feedback
            if (deviceOptimizer.isIOS) {
                generateBtn.innerHTML = '<i class="fas fa-spinner fa-spin"></i><span>جاري التوليد...</span>';
            } else if (deviceOptimizer.isAndroid) {
                generateBtn.innerHTML = '<i class="fas fa-circle-notch fa-spin"></i><span>جاري التوليد...</span>';
            } else {
                generateBtn.innerHTML = '<i class="fas fa-spinner fa-spin"></i><span>جاري التوليد...</span>';
            }
            
            generateBtn.disabled = true;
            
            // Haptic feedback for supported devices
            if (navigator.vibrate) {
                navigator.vibrate(50);
            }
            
            // Generate codes
            // ... بقية كود generateCodes كما هو
        }

        // ... باقي الدوال تبقى كما هي مع إضافة تحسينات التوافق

        // Utility functions
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

        function showNotification(message, type = 'success') {
            const notification = document.getElementById('notification');
            const messageEl = document.getElementById('notificationMessage');
            const icon = notification.querySelector('.notification-icon');
            
            // Set type-specific styling
            switch(type) {
                case 'success':
                    icon.className = 'fas fa-check-circle notification-icon';
                    notification.style.background = 'linear-gradient(135deg, var(--primary-500) 0%, var(--primary-700) 100%)';
                    break;
                case 'error':
                    icon.className = 'fas fa-exclamation-circle notification-icon';
                    notification.style.background = 'linear-gradient(135deg, var(--danger) 0%, #c9302c 100%)';
                    break;
                case 'warning':
                    icon.className = 'fas fa-exclamation-triangle notification-icon';
                    notification.style.background = 'linear-gradient(135deg, var(--warning) 0%, #ec971f 100%)';
                    break;
                default:
                    icon.className = 'fas fa-info-circle notification-icon';
                    notification.style.background = 'linear-gradient(135deg, var(--info) 0%, #2d7dfd 100%)';
            }
            
            messageEl.textContent = message;
            notification.classList.add('show');
            
            // Device-specific notification duration
            const duration = deviceOptimizer.isIOS ? 4000 : 3000;
            
            setTimeout(() => {
                hideNotification();
            }, duration);
            
            // Haptic feedback for supported devices
            if (type === 'success' && navigator.vibrate) {
                navigator.vibrate([50, 50, 50]);
            }
        }

        function hideNotification() {
            const notification = document.getElementById('notification');
            notification.classList.remove('show');
        }

        // Export functions to window
        window.generateCodes = generateCodes;
        window.copyCodes = copyCodes;
        window.shareCodes = shareCodes;
        window.showTab = showTab;
        window.hideNotification = hideNotification;
        window.saveSettings = saveSettings;
        window.resetSettings = resetSettings;
        window.filterUsers = filterUsers;
    </script>
</body>
</html>