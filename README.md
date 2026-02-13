<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=5.0, user-scalable=yes">
<title>تقاريرك - النظام المتكامل</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;500;600;700;800;900&display=swap');

/* ========== المتغيرات الأساسية ========== */
:root {
    --primary: #066d4d;
    --primary-dark: #044a35;
    --primary-light: #0a9d72;
    --secondary: #ffd166;
    --secondary-dark: #ffc145;
    --danger: #ff6b6b;
    --success: #25D366;
    --gray-light: #f8fdfa;
    --gray: #e0f0ea;
    --text-dark: #083024;
    --text-light: #666;
    --white: #ffffff;
    --shadow: 0 10px 30px rgba(4, 74, 53, 0.12);
    --border: #d4ebe2;
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    -webkit-tap-highlight-color: transparent;
}

html, body {
    font-family: 'Cairo', sans-serif;
    background: linear-gradient(135deg, #f0f9f6 0%, #e8f4f0 50%, #d4ebe2 100%);
    direction: rtl;
    overflow-x: hidden;
    min-height: 100vh;
    -webkit-text-size-adjust: 100%;
    -moz-text-size-adjust: 100%;
    -ms-text-size-adjust: 100%;
    text-size-adjust: 100%;
    touch-action: manipulation;
}

.wrapper {
    max-width: 900px;
    margin: auto;
    padding: 20px;
    width: 100%;
}

/* ========== شريط الأخبار العلوي ========== */
.top-marquee {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    width: 100%;
    background: linear-gradient(135deg, #022e22 0%, #044a35 100%);
    color: #fff;
    padding: 10px 5px;
    font-size: 12px;
    z-index: 300;
    overflow: hidden;
    height: 45px;
    white-space: nowrap;
    border-bottom: 3px solid #ffd166;
    box-shadow: 0 4px 12px rgba(2, 46, 34, 0.25);
    display: flex;
    align-items: center;
}

.marquee-inner {
    display: inline-block;
    padding-left: 2%;
    animation: newsScroll 30s linear infinite;
    color: #e8f4f0;
    font-weight: 500;
}

@keyframes newsScroll {
    0% { transform: translateX(-100%); }
    100% { transform: translateX(100%); }
}

.top-marquee:hover .marquee-inner {
    animation-play-state: paused;
}

/* ========== نظام الأزرار المحسّن ========== */
.top-small-buttons button,
.main-buttons-bar button,
#aiFillFloatingBtn {
    -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
    box-sizing: border-box;
    outline: none;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    user-select: none;
    transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
}

/* ========== المجموعة الأولى: الأزرار الصغيرة ========== */
.top-small-buttons {
    position: fixed;
    top: 45px;
    left: 0;
    right: 0;
    width: 100%;
    z-index: 250;
    background: linear-gradient(135deg, #ffffff 0%, #f5fcf9 100%);
    padding: 8px 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-bottom: 1px solid #e0f0ea;
    box-shadow: 0 2px 8px rgba(4, 74, 53, 0.08);
    box-sizing: border-box;
}

.small-buttons-grid {
    display: flex;
    gap: 8px;
    width: 100%;
    max-width: 600px;
    justify-content: center;
}

.small-btn {
    border: 2px solid;
    padding: 6px 4px;
    font-size: 10px;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
    font-weight: 700;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 3px;
    min-height: 45px;
    min-width: 90px;
    box-shadow: 0 1px 4px rgba(0,0,0,0.1);
    flex: 1;
    position: relative;
    overflow: hidden;
}

.small-btn:active {
    box-shadow: 0 0 0 2px rgba(255,255,255,0.5), inset 0 3px 5px rgba(0,0,0,0.1) !important;
    filter: brightness(0.95);
}

#saveTeacherBtn {
    background: linear-gradient(135deg, #4f7bff 0%, #3b5bdb 100%);
    color: white;
    border-color: #3b5bdb;
}

#clearBtn {
    background: linear-gradient(135deg, #ffd166 0%, #ffc145 100%);
    color: #5a3e00;
    border-color: #ffc145;
}

#savedReportsBtn {
    background: linear-gradient(135deg, #9D50BB 0%, #6E48AA 100%);
    color: white;
    border-color: #6E48AA;
}

#settingsBtn {
    background: linear-gradient(135deg, #718096 0%, #4a5568 100%);
    color: white;
    border-color: #4a5568;
}

.small-btn-icon {
    font-size: 12px;
    color: white;
    transition: none;
}

.small-btn .small-btn-text {
    font-size: 9px;
    font-weight: 800;
    text-align: center;
    line-height: 1.1;
    white-space: nowrap;
    transition: none;
}

/* ========== المجموعة الثانية: الأزرار الكبيرة ========== */
.main-buttons-bar {
    position: fixed;
    top: 98px;
    left: 0;
    right: 0;
    width: 100%;
    z-index: 240;
    background: linear-gradient(135deg, #f8fdfa 0%, #f0f9f6 100%);
    padding: 10px 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    box-shadow: 0 3px 10px rgba(4, 74, 53, 0.1);
    border-bottom: 1px solid #d4ebe2;
    box-sizing: border-box;
}

.main-buttons-grid {
    display: flex;
    gap: 20px;
    width: 100%;
    max-width: 350px;
    justify-content: center;
}

.main-btn {
    border: 2px solid;
    padding: 12px 10px;
    font-size: 13px;
    border-radius: 12px;
    cursor: pointer;
    transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
    font-weight: 700;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 6px;
    min-height: 65px;
    min-width: 130px;
    box-shadow: 0 3px 10px rgba(0,0,0,0.15);
    flex: 1;
    position: relative;
    overflow: hidden;
}

.main-btn:active {
    box-shadow: 0 0 0 3px rgba(255,255,255,0.5), inset 0 4px 6px rgba(0,0,0,0.1) !important;
    filter: brightness(0.95);
}

#pdfBtn {
    background: linear-gradient(135deg, #ff6b6b 0%, #ee5a52 100%);
    color: white;
    border-color: #ee5a52;
}

#whatsappBtn {
    background: linear-gradient(135deg, #25D366 0%, #1da851 100%);
    color: white;
    border-color: #1da851;
}

.main-btn-icon {
    font-size: 18px;
    color: white;
    transition: none;
}

.main-btn .main-btn-text {
    font-size: 12px;
    font-weight: 800;
    text-align: center;
    line-height: 1.2;
    white-space: nowrap;
    transition: none;
}

/* ========== شريط التقدم العلوي ========== */
.progress-bar-container {
    position: fixed;
    top: 163px;
    left: 0;
    right: 0;
    width: 100%;
    z-index: 230;
    background: linear-gradient(135deg, #ffffff 0%, #f8fdfa 100%);
    padding: 15px 20px;
    border-bottom: 2px solid #d4ebe2;
    box-shadow: 0 4px 15px rgba(4, 74, 53, 0.15);
    display: none;
    flex-direction: column;
    align-items: center;
    gap: 10px;
    font-family: 'Cairo', sans-serif;
    backdrop-filter: blur(5px);
    box-sizing: border-box;
}

.progress-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    max-width: 900px;
    margin: 0 auto;
    color: #044a35;
    font-weight: 700;
    font-size: 15px;
}

.progress-stats {
    display: flex;
    gap: 15px;
    align-items: center;
}

.progress-percentage {
    background: linear-gradient(135deg, #ffd166, #ffc233);
    color: #5a3e00;
    padding: 5px 15px;
    border-radius: 30px;
    font-size: 14px;
    font-weight: 800;
    box-shadow: 0 2px 8px rgba(255, 209, 102, 0.3);
    border: 1px solid #ffb830;
}

.progress-message {
    color: #066d4d;
    font-size: 13px;
    font-weight: 600;
    background: #e8f4f0;
    padding: 5px 15px;
    border-radius: 30px;
    border: 1px solid #c0e0d6;
}

.progress-track {
    width: 100%;
    max-width: 900px;
    margin: 0 auto;
    height: 18px;
    background: #e0f0ea;
    border-radius: 30px;
    overflow: hidden;
    border: 1px solid #c0e0d6;
    box-shadow: inset 0 2px 5px rgba(0,0,0,0.1);
    position: relative;
}

.progress-fill {
    height: 100%;
    background: linear-gradient(90deg, #066d4d, #0a9d72, #066d4d);
    background-size: 200% 100%;
    animation: progressShimmer 2s linear infinite;
    border-radius: 30px;
    transition: width 0.5s cubic-bezier(0.4, 0, 0.2, 1);
    position: relative;
    box-shadow: 0 0 15px rgba(6, 109, 77, 0.5);
}

@keyframes progressShimmer {
    0% { background-position: 200% 0; }
    100% { background-position: -200% 0; }
}

.criteria-status {
    width: 100%;
    max-width: 900px;
    margin: 5px auto 0;
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    justify-content: center;
    font-size: 11px;
}

.criterion-badge {
    background: #f0f9f6;
    border: 1px solid #c0e0d6;
    border-radius: 20px;
    padding: 3px 10px;
    color: #044a35;
    font-weight: 600;
    display: inline-flex;
    align-items: center;
    gap: 5px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.05);
}

.criterion-badge.completed {
    background: #d4edda;
    border-color: #066d4d;
    color: #066d4d;
}

.criterion-badge i {
    font-size: 10px;
}

.criterion-weight {
    background: #ffd166;
    color: #5a3e00;
    border-radius: 12px;
    padding: 2px 6px;
    font-size: 9px;
    font-weight: 800;
    margin-right: 5px;
}

/* ========== زر التعبئة الذكية العائم ========== */
#aiFillFloatingBtn {
    position: fixed;
    bottom: 30px;
    left: 30px;
    width: 100px;
    height: 100px;
    color: white;
    border: none;
    border-radius: 50%;
    font-size: 16px;
    font-weight: 900;
    cursor: pointer;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 6px;
    border: 4px solid rgba(255, 255, 255, 0.7);
    z-index: 1000;
    overflow: hidden;
    transform: translateY(0);
    animation: floatButton 3s ease-in-out infinite;
    background: linear-gradient(135deg, #9D50BB 0%, #6E48AA 25%, #533D8B 50%, #3A2569 100%);
    box-shadow: 0 12px 35px rgba(157, 80, 187, 0.6), 0 0 0 3px rgba(255, 255, 255, 0.3), 0 0 25px rgba(157, 80, 187, 0.5);
}

#aiFillFloatingBtn .floating-ai-icon {
    font-size: 38px;
    animation: magicalPulse 2s infinite;
    filter: drop-shadow(0 3px 6px rgba(0, 0, 0, 0.5));
    margin-bottom: 2px;
    color: #FFFFFF;
    transition: none;
}

#aiFillFloatingBtn .floating-ai-text {
    font-size: 14px;
    font-weight: 900;
    letter-spacing: 0.5px;
    text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
    color: #FFFFFF;
    background: linear-gradient(45deg, #FFFFFF, #F0F0F0, #FFFFFF);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    background-size: 200% auto;
    animation: textShine 2s ease-in-out infinite;
    white-space: nowrap;
    transition: none;
}

@keyframes floatButton {
    0%, 100% { transform: translateY(0) rotate(0deg); }
    25% { transform: translateY(-12px) rotate(3deg); }
    50% { transform: translateY(0) rotate(0deg); }
    75% { transform: translateY(-8px) rotate(-3deg); }
}

@keyframes magicalPulse {
    0%, 100% { 
        transform: scale(1) rotate(0deg);
        filter: drop-shadow(0 3px 6px rgba(0, 0, 0, 0.5)) brightness(1);
    }
    25% { 
        transform: scale(1.15) rotate(10deg);
        filter: drop-shadow(0 5px 10px rgba(255, 255, 255, 0.6)) brightness(1.2);
    }
    50% { 
        transform: scale(1.1) rotate(-5deg);
        filter: drop-shadow(0 4px 8px rgba(255, 255, 255, 0.5)) brightness(1.1);
    }
    75% { 
        transform: scale(1.18) rotate(5deg);
        filter: drop-shadow(0 6px 12px rgba(255, 255, 255, 0.7)) brightness(1.3);
    }
}

@keyframes textShine {
    0%, 100% { 
        background-position: 0% 50%;
        text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
    }
    50% { 
        background-position: 100% 50%;
        text-shadow: 0 3px 6px rgba(255, 255, 255, 0.3), 0 0 10px rgba(255, 255, 255, 0.2);
    }
}

#aiFillFloatingBtn.loading {
    animation: loadingMagicalGlow 1.5s ease-in-out infinite;
}

@keyframes loadingMagicalGlow {
    0%, 100% { 
        box-shadow: 0 12px 35px rgba(0,0,0,0.4), 0 0 0 4px rgba(255, 255, 255, 0.4), 0 0 30px rgba(0,0,0,0.3);
    }
    50% { 
        box-shadow: 0 18px 45px rgba(0,0,0,0.6), 0 0 0 5px rgba(255, 255, 255, 0.7), 0 0 40px rgba(0,0,0,0.5);
    }
}

#aiFillFloatingBtn.loading .floating-ai-icon {
    animation: magicalSpin 1.2s linear infinite;
}

@keyframes magicalSpin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}

/* ========== شاشة التفعيل ========== */
#activationScreen {
    position: fixed;
    top: 0; left: 0; right: 0; bottom: 0;
    background: linear-gradient(135deg, #022e22, #044a35);
    z-index: 9999;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'Cairo', sans-serif;
}

#activationScreen .activation-box {
    background: white;
    padding: 30px;
    border-radius: 15px;
    width: 90%;
    max-width: 400px;
    text-align: center;
    box-shadow: 0 15px 40px rgba(0,0,0,0.3);
    border: 3px solid #ffd166;
}

#activationScreen h3 {
    color: #044a35; 
    margin-bottom: 20px; 
    font-size: 22px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
}

#activationScreen p {
    color: #666; 
    font-size: 14px; 
    margin-bottom: 20px;
}

#activationCodeInput {
    width: 100%;
    padding: 15px;
    border: 2px solid #d4ebe2;
    border-radius: 10px;
    font-size: 16px;
    text-align: center;
    margin-bottom: 20px;
    font-family: 'Cairo', sans-serif;
    transition: all 0.3s;
}

#activationCodeInput:focus {
    outline: none;
    border-color: #066d4d;
    box-shadow: 0 0 0 3px rgba(6, 109, 77, 0.15);
}

#activationScreen button {
    width: 100%;
    padding: 15px;
    background: linear-gradient(135deg, #066d4d 0%, #05553d 100%);
    color: white;
    border: none;
    border-radius: 10px;
    font-weight: 700;
    cursor: pointer;
    font-size: 16px;
    transition: all 0.3s;
    font-family: 'Cairo', sans-serif;
}

#activationScreen button:hover {
    background: linear-gradient(135deg, #05553d 0%, #044a35 100%);
    filter: brightness(1.05);
}

#contactForTrialBtn {
    width: 100%;
    padding: 15px;
    background: linear-gradient(135deg, #5a67d8 0%, #4c51bf 100%);
    color: white;
    border: none;
    border-radius: 10px;
    font-weight: 700;
    cursor: pointer;
    font-size: 16px;
    transition: all 0.3s;
    font-family: 'Cairo', sans-serif;
    margin-top: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
}

#contactForTrialBtn:hover {
    background: linear-gradient(135deg, #4c51bf 0%, #434190 100%);
    filter: brightness(1.05);
}

#activationError {
    color: #d9534f;
    font-size: 13px;
    margin-top: 15px;
    padding: 10px;
    background: #fee;
    border-radius: 8px;
    border-right: 4px solid #d9534f;
    display: none;
}

/* ========== تحسين واجهة الإدخال ========== */
.input-section {
    background: #ffffff;
    padding: 25px;
    border-radius: 20px;
    margin-top: 220px;
    border: 2px solid #e0f0ea;
    box-shadow: 0 10px 30px rgba(4, 74, 53, 0.12);
    position: relative;
    overflow: hidden;
}

.input-section::before {
    content: '';
    position: absolute;
    top: 0;
    right: 0;
    width: 100%;
    height: 5px;
    background: linear-gradient(to left, #066d4d, #ffd166, #25D366);
}

.input-section h2 {
    color: #044a35;
    font-size: 24px;
    margin-bottom: 30px;
    padding-bottom: 15px;
    border-bottom: 3px solid #e0f0ea;
    text-align: center;
    font-weight: 900;
    position: relative;
}

.input-section h2::after {
    content: '';
    position: absolute;
    bottom: -3px;
    right: 50%;
    transform: translateX(50%);
    width: 120px;
    height: 3px;
    background: linear-gradient(to left, #066d4d, #ffd166);
    border-radius: 2px;
}

/* تصميم الحقول */
.form-group {
    margin-bottom: 25px;
    position: relative;
}

.form-group label {
    font-size: 16px;
    font-weight: 800;
    margin-bottom: 10px;
    display: flex;
    align-items: center;
    gap: 12px;
    padding-right: 8px;
    position: relative;
    color: #083024;
}

.form-group label i {
    color: #066d4d;
    font-size: 16px;
    background: #f0f9f6;
    padding: 7px;
    border-radius: 10px;
    border: 1px solid #d4ebe2;
    box-shadow: 0 2px 5px rgba(0,0,0,0.05);
}

.form-group label::before {
    content: '';
    width: 8px;
    height: 8px;
    background: #ffd166;
    border-radius: 50%;
    display: inline-block;
    margin-left: 6px;
    box-shadow: 0 0 6px #ffd166;
}

input, select, textarea {
    width: 100%;
    padding: 16px;
    margin-top: 8px;
    border: 2px solid #d4ebe2;
    border-radius: 12px;
    font-size: 18px;
    background: #f9fcfb;
    transition: all 0.3s;
    font-family: 'Cairo', sans-serif;
    color: #083024;
    box-shadow: inset 0 2px 8px rgba(0,0,0,0.05);
    -webkit-appearance: none;
}

input:focus, select:focus, textarea:focus {
    outline: none;
    border-color: #066d4d;
    box-shadow: 0 0 0 4px rgba(6,109,77,0.15), inset 0 2px 8px rgba(0,0,0,0.05);
    background: #ffffff;
}

textarea {
    height: 120px;
    resize: none;
    overflow: hidden;
    line-height: 1.7;
    font-size: 17px;
}

.form-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
}

/* تلميحات للأزرار */
button[title] {
    position: relative;
}

button[title]:hover::after {
    content: attr(title);
    position: absolute;
    bottom: calc(100% + 10px);
    right: 50%;
    transform: translateX(50%);
    background: rgba(4, 58, 42, 0.95);
    color: white;
    padding: 10px 15px;
    border-radius: 8px;
    font-size: 12px;
    white-space: pre-line;
    z-index: 1000;
    border: 1px solid #044a35;
    box-shadow: 0 5px 15px rgba(0,0,0,0.15);
    max-width: 300px;
    min-width: 200px;
}

button[title]:hover::before {
    content: '';
    position: absolute;
    bottom: calc(100% + 2px);
    right: 50%;
    transform: translateX(50%);
    border: 6px solid transparent;
    border-top-color: rgba(4, 58, 42, 0.95);
    z-index: 1000;
}

/* إشعارات */
.notification {
    position: fixed;
    top: 150px;
    right: 10px;
    left: 10px;
    background: linear-gradient(135deg, #066d4d 0%, #044a35 100%);
    color: white;
    padding: 12px 18px;
    border-radius: 10px;
    box-shadow: 0 6px 20px rgba(4, 74, 53, 0.3);
    z-index: 1000;
    display: flex;
    align-items: center;
    gap: 10px;
    font-weight: 600;
    transform: translateX(150%);
    transition: transform 0.4s cubic-bezier(0.68, -0.55, 0.27, 1.55);
    border-right: 5px solid #ffd166;
    text-align: center;
    justify-content: center;
}

.notification.show {
    transform: translateX(0);
}

.notification i {
    font-size: 18px;
}

/* ========== أنماط القوائم ========== */
.levels-container {
    background: #f8fdfa;
    border-radius: 12px;
    padding: 15px;
    margin-bottom: 20px;
    border: 2px solid #d4ebe2;
    box-shadow: 0 4px 10px rgba(0,0,0,0.05);
}

.level-indicator {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 15px;
    padding: 8px;
    background: linear-gradient(135deg, #066d4d 0%, #044a35 100%);
    border-radius: 8px;
    color: white;
    font-weight: 700;
    font-size: 14px;
}

.level-indicator span {
    background: rgba(255,255,255,0.2);
    padding: 3px 10px;
    border-radius: 20px;
    font-size: 12px;
}

.level-select {
    margin-bottom: 15px;
}

.level-select select {
    width: 100%;
    padding: 12px;
    border: 2px solid #d4ebe2;
    border-radius: 8px;
    font-family: 'Cairo', sans-serif;
    font-size: 14px;
    background: white;
    cursor: pointer;
}

.level-select select:focus {
    border-color: #066d4d;
    outline: none;
}

.level-select label {
    font-size: 12px;
    color: #044a35;
    font-weight: 600;
    margin-bottom: 5px;
    display: flex;
    align-items: center;
    gap: 5px;
}

.level-select label i {
    color: #066d4d;
    font-size: 12px;
}

/* معلومات المعيار المحدد */
.criterion-info {
    background: white;
    border-radius: 8px;
    padding: 10px 15px;
    margin: 15px 0;
    border-right: 4px solid #ffd166;
    display: flex;
    align-items: center;
    justify-content: space-between;
    box-shadow: 0 2px 8px rgba(0,0,0,0.05);
}

.criterion-name {
    font-weight: 800;
    color: #044a35;
    font-size: 14px;
}

.criterion-weight {
    background: #ffd166;
    color: #5a3e00;
    padding: 3px 10px;
    border-radius: 20px;
    font-weight: 700;
    font-size: 12px;
}

/* أنماط البحث */
#reportSearchContainer {
    position: relative;
    margin-bottom: 15px;
}

#searchResults {
    display: none;
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    background: white;
    border: 1px solid #ddd;
    border-radius: 6px;
    max-height: 200px;
    overflow-y: auto;
    z-index: 1000;
    box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}

#searchResults div {
    padding: 8px 12px;
    cursor: pointer;
    border-bottom: 1px solid #eee;
}

#searchResults div:hover {
    background-color: #f0f9f6 !important;
    color: #066d4d;
}

#searchResults div:last-child {
    border-bottom: none;
}

#reportSearch:focus {
    outline: none;
    border-color: #066d4d;
    box-shadow: 0 0 0 2px rgba(6, 109, 77, 0.2);
}

/* خانة عنوان التقرير اليدوية */
.manual-title-container {
    margin-top: 15px;
    padding: 15px;
    background: #f8fdfa;
    border-radius: 12px;
    border: 2px solid #d4ebe2;
}

.manual-title-container label {
    display: flex;
    align-items: center;
    gap: 10px;
    color: #044a35;
    font-weight: 700;
    margin-bottom: 10px;
}

.manual-title-container input {
    background: white;
    border: 2px solid #d4ebe2;
    padding: 12px;
    border-radius: 8px;
    font-size: 16px;
}

/* قسم الأدوات */
.tools-section {
    background: #f8fdfa;
    padding: 18px;
    border-radius: 12px;
    border: 1px solid #d4ebe2;
    margin-top: 10px;
    box-shadow: 0 3px 10px rgba(0,0,0,0.05);
    counter-reset: tool-counter;
}

.tools-grid {
    display: grid;
    gap: 12px;
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
}

.tool-checkbox {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 10px 10px 10px 30px;
    background: white;
    border-radius: 10px;
    border: 2px solid #d4ebe2;
    transition: all 0.3s;
    cursor: pointer;
    position: relative;
    min-height: 50px;
}

.tool-checkbox::before {
    counter-increment: tool-counter;
    content: counter(tool-counter);
    position: absolute;
    right: 8px;
    background: #066d4d;
    color: white;
    width: 20px;
    height: 20px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 11px;
    font-weight: 700;
}

.tool-checkbox:hover {
    border-color: #066d4d;
    background: #f0f9f6;
    box-shadow: 0 4px 8px rgba(6, 109, 77, 0.1);
    transform: translateY(-2px);
}

.tool-checkbox input[type="checkbox"] {
    width: 20px;
    height: 20px;
    cursor: pointer;
    position: absolute;
    opacity: 0;
    z-index: 1;
}

.tool-checkbox span {
    font-size: 14px;
    font-weight: 700;
    color: #083024;
    margin-right: 25px;
    flex: 1;
}

.tool-checkbox.checked {
    border-color: #066d4d;
    background: #e8f4f0;
    box-shadow: 0 4px 10px rgba(6, 109, 77, 0.15);
}

.checkmark {
    color: #066d4d;
    font-size: 16px;
    margin-right: 5px;
    display: none;
}

.tool-checkbox.checked .checkmark {
    display: inline-block;
}

/* ========== نافذة التقارير المحفوظة ========== */
#savedReportsModal {
    display: none;
    position: fixed;
    top: 0; left: 0; right: 0; bottom: 0;
    background: rgba(0,0,0,0.5);
    z-index: 6000;
    align-items: center;
    justify-content: center;
    font-family: 'Cairo', sans-serif;
}

#savedReportsModal > div {
    background: white;
    padding: 25px;
    border-radius: 15px;
    width: 90%;
    max-width: 800px;
    max-height: 80vh;
    overflow-y: auto;
    box-shadow: 0 15px 40px rgba(0,0,0,0.3);
    border: 3px solid #ffd166;
}

#savedReportsModal h3 {
    color: #044a35;
    text-align: center;
    margin-bottom: 20px;
    font-size: 22px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
    position: sticky;
    top: 0;
    background: white;
    padding-bottom: 10px;
    border-bottom: 2px solid #d4ebe2;
}

.reports-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 15px;
    margin-bottom: 20px;
}

.report-card {
    background: #f8fdfa;
    border: 2px solid #d4ebe2;
    border-radius: 12px;
    padding: 15px;
    transition: all 0.3s;
    position: relative;
    overflow: hidden;
}

.report-card:hover {
    border-color: #066d4d;
    box-shadow: 0 5px 15px rgba(6,109,77,0.15);
    transform: translateY(-3px);
}

.report-card.completed {
    border-right: 6px solid #066d4d;
    background: #f0f9f6;
}

.report-card .report-title {
    font-weight: 800;
    color: #044a35;
    font-size: 16px;
    margin-bottom: 10px;
    padding-left: 25px;
}

.report-card .report-criterion {
    font-size: 12px;
    color: #066d4d;
    margin-bottom: 8px;
    display: flex;
    align-items: center;
    gap: 5px;
}

.report-card .report-criterion i {
    font-size: 10px;
}

.report-card .report-weight {
    background: #ffd166;
    color: #5a3e00;
    padding: 2px 8px;
    border-radius: 15px;
    font-size: 11px;
    font-weight: 700;
    display: inline-block;
    margin-bottom: 10px;
}

.report-card .report-date {
    font-size: 11px;
    color: #666;
    margin-bottom: 15px;
    display: flex;
    align-items: center;
    gap: 5px;
}

.report-actions {
    display: flex;
    gap: 8px;
    justify-content: flex-end;
}

.report-actions button {
    padding: 6px 12px;
    border: none;
    border-radius: 6px;
    font-size: 11px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s;
    display: flex;
    align-items: center;
    gap: 5px;
}

.report-actions .load-btn {
    background: #066d4d;
    color: white;
    flex: 1;
}

.report-actions .load-btn:hover {
    background: #044a35;
}

.report-actions .delete-btn {
    background: #fee;
    color: #d9534f;
    border: 1px solid #fcc;
}

.report-actions .delete-btn:hover {
    background: #fdd;
    color: #b52b27;
}

.close-reports-btn {
    width: 100%;
    padding: 12px;
    background: #066d4d;
    color: white;
    border: none;
    border-radius: 10px;
    font-weight: 700;
    cursor: pointer;
    font-size: 14px;
    transition: all 0.3s;
    position: sticky;
    bottom: 0;
}

.close-reports-btn:hover {
    background: #044a35;
}

.empty-reports {
    text-align: center;
    padding: 30px;
    color: #666;
    font-size: 14px;
    background: #f8fdfa;
    border-radius: 10px;
    border: 2px dashed #d4ebe2;
}

.empty-reports i {
    font-size: 40px;
    color: #c0e0d6;
    margin-bottom: 10px;
}

/* ========== نافذة الإعدادات ========== */
#settingsModal {
    display: none;
    position: fixed;
    top: 0; left: 0; right: 0; bottom: 0;
    background: rgba(0,0,0,0.5);
    z-index: 5000;
    align-items: center;
    justify-content: center;
    font-family: 'Cairo', sans-serif;
}

#settingsModal > div {
    background: white;
    padding: 25px;
    border-radius: 15px;
    width: 90%;
    max-width: 400px;
    max-height: 80vh;
    overflow-y: auto;
    box-shadow: 0 15px 40px rgba(0,0,0,0.3);
    border: 3px solid #ffd166;
}

#settingsModal h3 {
    color: #044a35;
    text-align: center;
    margin-bottom: 15px;
    font-size: 22px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
}

#settingsModal #subInfo {
    font-size: 14px;
    line-height: 2;
    color: #333;
    text-align: center;
    margin-bottom: 15px;
}

#settingsModal label {
    font-weight: 700;
    color: #044a35;
    display: block;
    margin-bottom: 8px;
    display: flex;
    align-items: center;
    gap: 8px;
}

#settingsModal input[type="date"] {
    width: 100%;
    margin-top: 8px;
    padding: 10px;
    border-radius: 8px;
    border: 2px solid #d4ebe2;
    font-family: 'Cairo', sans-serif;
    font-size: 16px;
}

#settingsModal input[type="date"]:focus {
    outline: none;
    border-color: #066d4d;
    box-shadow: 0 0 0 3px rgba(6,109,77,0.15);
}

#settingsModal button {
    width: 100%;
    padding: 12px;
    background: #066d4d;
    color: white;
    border: none;
    border-radius: 10px;
    font-weight: 700;
    cursor: pointer;
    font-family: 'Cairo', sans-serif;
    transition: all 0.3s;
    margin-top: 10px;
}

#settingsModal button:hover {
    background: #05553d;
    filter: brightness(1.05);
}

#settingsModal .btn-secondary {
    background: #4f7bff;
    margin-top: 5px;
}

#settingsModal .btn-secondary:hover {
    background: #3b5bdb;
    filter: brightness(1.05);
}

#settingsModal hr {
    margin: 15px 0;
    border: none;
    border-top: 1px solid #d4ebe2;
}

/* ========== أنماط الثيمات ========== */
.theme-light-blue body {
    background: linear-gradient(135deg, #e8f0ff 0%, #d6e4ff 50%, #c2d4ff 100%) !important;
}

.theme-light-blue .input-section {
    background: #ffffff;
    border: 2px solid #c2d4ff;
    box-shadow: 0 10px 30px rgba(66, 133, 244, 0.15);
}

.theme-light-blue .input-section::before {
    background: linear-gradient(to left, #4285f4, #34a853, #fbbc05);
}

.theme-light-blue .input-section h2 {
    color: #4285f4;
}

.theme-light-blue .top-marquee {
    background: linear-gradient(135deg, #1a73e8 0%, #4285f4 100%);
}

.theme-light-blue #aiFillFloatingBtn {
    background: linear-gradient(135deg, #4285f4 0%, #34a853 25%, #fbbc05 50%, #ea4335 100%) !important;
}

.theme-dark body {
    background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%) !important;
    color: #e0e0e0;
}

.theme-dark .input-section {
    background: #1e293b;
    border: 2px solid #334155;
    color: #e0e0e0;
}

.theme-dark .input-section h2 {
    color: #60a5fa;
}

.theme-dark input,
.theme-dark select,
.theme-dark textarea {
    background: #1e293b;
    border-color: #475569;
    color: #e0e0e0;
}

.theme-dark .top-marquee {
    background: linear-gradient(135deg, #0f172a 0%, #1e293b 100%);
}

.theme-dark #aiFillFloatingBtn {
    background: linear-gradient(135deg, #6d28d9 0%, #7c3aed 25%, #8b5cf6 50%, #a78bfa 100%) !important;
}

.theme-green body {
    background: linear-gradient(135deg, #e6f7ef 0%, #d4f0e4 50%, #c2e8d9 100%) !important;
}

.theme-green .input-section {
    background: #ffffff;
    border: 2px solid #2ecc71;
    box-shadow: 0 10px 30px rgba(46, 204, 113, 0.15);
}

.theme-green .input-section h2 {
    color: #27ae60;
}

.theme-green .top-marquee {
    background: linear-gradient(135deg, #1e8449 0%, #27ae60 100%);
}

.theme-green #aiFillFloatingBtn {
    background: linear-gradient(135deg, #27ae60 0%, #2ecc71 25%, #3498db 50%, #9b59b6 100%) !important;
}

/* ========== قسم PDF ========== */
@page {
    size: A4;
    margin: 10mm;
}

:root {
    --main: #062f25;
    --border: #2f9e8f;
    --bg: #ffffff;
}

#report-content {
    width: 100%;
    max-width: 210mm;
    margin: 4mm auto 0 auto;
    padding: 0 6mm;
    box-sizing: border-box;
    display: none;
    font-family: 'Cairo', sans-serif;
    background: var(--bg);
}

.header {
    background: var(--main);
    height: 150px;
    border-radius: 8px;
    color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    margin-bottom: 8px;
}

.header img {
    width: 260px;
    filter: brightness(0) invert(1);
}

.header-school-title {
    position: absolute;
    right: 12px;
    top: 20px;
    font-size: 14px;
    font-weight: 800;
}

.header-school {
    position: absolute;
    right: 12px;
    top: 45px;
    font-size: 16px;
    font-weight: 700;
    max-width: 70%;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    text-align: right;
}

.header-education {
    position: absolute;
    left: 50%;
    bottom: 18px;
    transform: translateX(-50%);
    font-size: 16px;
    font-weight: 800;
    text-align: center;
    width: 100%;
}

.header-date {
    position: absolute;
    left: 12px;
    top: 10px;
    font-size: 12px;
    text-align: right;
}

.info-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 6px;
    margin-bottom: 6px;
}

.info-grid2 {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 6px;
    margin-bottom: 6px;
}

.info-box {
    border: 1px solid var(--border);
    border-radius: 7px;
    padding: 14px 4px 6px;
    position: relative;
    text-align: center;
    font-size: 11px;
    min-height: 34px;
    overflow: hidden;
    background: var(--bg);
}

.info-title {
    position: absolute;
    top: 4px;
    right: 50%;
    transform: translateX(50%);
    font-size: 8px;
    font-weight: 800;
    color: var(--main);
    white-space: nowrap;
}

.info-value {
    font-size: 11px;
    font-weight: 600;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}

.subject-lesson-box {
    border: 1px solid var(--border);
    border-radius: 7px;
    position: relative;
    padding: 14px 4px 6px;
    overflow: hidden;
    height: 48px;
    min-height: 48px;
    max-height: 48px;
    background: var(--bg);
}

.subject-lesson-title {
    position: absolute;
    top: 4px;
    right: 50%;
    transform: translateX(50%);
    font-size: 8px;
    font-weight: 800;
    color: var(--main);
}

.subject-lesson {
    display: grid;
    grid-template-columns: 1fr 1px 1fr;
    align-items: center;
    text-align: center;
    font-size: 11px;
    height: 100%;
}

.subject-divider {
    background: var(--border);
    height: 60%;
    margin: auto;
}

.box-objective {
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 8px;
    margin-bottom: 6px;
    height: 95px;
    display: flex;
    flex-direction: column;
    overflow: hidden;
    background: var(--bg);
}

.box-objective .box-title {
    text-align: center;
    color: var(--main);
    font-weight: 800;
    font-size: 8px;
    margin-bottom: 4px;
}

.box-objective .box-content {
    font-size: 14px;
    line-height: 1.5;
    text-align: center;
    overflow: hidden;
}

.box {
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 8px;
    margin-bottom: 6px;
    height: 137px;
    display: flex;
    flex-direction: column;
    overflow: hidden;
    background: var(--bg);
}

.box-title {
    text-align: center;
    color: var(--main);
    font-weight: 800;
    font-size: 14px;
    margin-bottom: 4px;
}

.box-content {
    font-size: 14px;
    line-height: 1.5;
    text-align: center;
    overflow: hidden;
}

.row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 6px;
}

.tools-box {
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 6px;
    margin-bottom: 6px;
    overflow: hidden;
    background: var(--bg);
}

.tools-title {
    text-align: center;
    font-weight: 800;
    color: var(--main);
    font-size: 13px;
    margin-bottom: 4px;
}

.tools-list {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 6px;
    font-size: 12px;
}

.tool {
    background: #eef7f4;
    border: 1px solid #cfe8df;
    border-radius: 16px;
    padding: 3px 8px;
    display: flex;
    align-items: center;
    gap: 5px;
    white-space: nowrap;
}

.tool span {
    background: var(--border);
    color: #fff;
    border-radius: 50%;
    width: 12px;
    height: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 8px;
}

.images {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 6px;
    margin-bottom: 6px;
}

.image-box {
    border: 1px dashed var(--border);
    height: 160px;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    background: #f9fdfb;
    position: relative;
}

.image-box::before {
    content: 'صورة توثيقية';
    position: absolute;
    top: 4px;
    right: 4px;
    font-size: 12px;
    background: rgba(255,255,255,.9);
    padding: 1px 5px;
    border-radius: 3px;
    z-index: 1;
}

.image-box img {
    width: 65%;
    height: 100%;
    object-fit: contain;
    display: block;
}

.signatures {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 30px;
    text-align: center;
    font-size: 13px;
    margin-bottom: 6px;
}

.signature-box {
    padding-top: 4px;
}

.signature-role {
    font-size: 12px;
    color: var(--main);
    font-weight: 700;
    margin-bottom: 2px;
}

.signature-name {
    font-size: 14px;
    font-weight: 900;
    color: #000;
}

.sign-line {
    border-top: 1px solid #000;
    margin: 6px auto 0;
    width: 70%;
}

.footer-box {
    background: var(--main);
    color: #fff;
    text-align: center;
    font-size: 11px;
    padding: 3px 4px;
    border-radius: 6px;
}

.pdf-export * {
    -webkit-print-color-adjust: exact !important;
    print-color-adjust: exact !important;
    color-adjust: exact !important;
}

#subjectBox, #lessonBox {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    width: 100%;
    height: 100%;
    padding: 0 5px;
    transition: all 0.3s ease;
}

/* ========== تحسينات للهواتف المحمولة ========== */
@media (max-width: 768px) {
    .top-small-buttons {
        padding: 6px 15px;
    }
    
    .small-buttons-grid {
        gap: 6px;
    }
    
    .small-btn {
        min-height: 38px;
        min-width: 70px;
        padding: 4px 3px;
        font-size: 9px;
    }
    
    .small-btn-icon {
        font-size: 10px;
    }
    
    .small-btn .small-btn-text {
        font-size: 8px;
    }
    
    .main-buttons-bar {
        padding: 8px 15px;
    }
    
    .main-buttons-grid {
        gap: 12px;
        max-width: 280px;
    }
    
    .main-btn {
        min-height: 55px;
        min-width: 110px;
        padding: 8px 6px;
    }
    
    .main-btn-icon {
        font-size: 16px;
    }
    
    .main-btn .main-btn-text {
        font-size: 11px;
    }
    
    .progress-bar-container {
        top: 153px;
        padding: 10px 15px;
    }
    
    .progress-header {
        font-size: 13px;
    }
    
    .progress-percentage {
        padding: 3px 10px;
        font-size: 12px;
    }
    
    .progress-message {
        padding: 3px 10px;
        font-size: 11px;
    }
    
    #aiFillFloatingBtn {
        width: 85px;
        height: 85px;
        bottom: 20px;
        left: 20px;
    }
    
    #aiFillFloatingBtn .floating-ai-icon {
        font-size: 32px;
    }
    
    #aiFillFloatingBtn .floating-ai-text {
        font-size: 12px;
    }
    
    .input-section {
        margin-top: 210px;
        padding: 15px;
    }
    
    .input-section h2 {
        font-size: 20px;
    }
    
    .form-row {
        grid-template-columns: 1fr;
        gap: 15px;
    }
    
    .tools-grid {
        grid-template-columns: repeat(2, 1fr);
    }
}

@media (max-width: 480px) {
    .top-marquee {
        font-size: 11px;
        height: 40px;
    }
    
    .marquee-inner {
        animation-duration: 35s;
    }
    
    .small-btn {
        min-height: 35px;
        min-width: 60px;
        padding: 3px 2px;
        font-size: 8px;
    }
    
    .small-btn-icon {
        font-size: 9px;
    }
    
    .small-btn .small-btn-text {
        font-size: 7px;
    }
    
    .main-btn {
        min-height: 50px;
        min-width: 95px;
    }
    
    .main-btn-icon {
        font-size: 14px;
    }
    
    .main-btn .main-btn-text {
        font-size: 10px;
    }
    
    .progress-bar-container {
        top: 148px;
        padding: 8px 10px;
    }
    
    .criteria-status {
        gap: 4px;
    }
    
    .criterion-badge {
        padding: 2px 6px;
        font-size: 9px;
    }
    
    #aiFillFloatingBtn {
        width: 75px;
        height: 75px;
        bottom: 15px;
        left: 15px;
    }
    
    #aiFillFloatingBtn .floating-ai-icon {
        font-size: 28px;
    }
    
    #aiFillFloatingBtn .floating-ai-text {
        font-size: 11px;
    }
    
    .input-section {
        margin-top: 190px;
        padding: 12px;
    }
    
    input, select, textarea {
        padding: 12px;
        font-size: 16px;
    }
    
    .form-group label {
        font-size: 13px;
    }
    
    .tool-checkbox {
        padding: 6px 6px 6px 26px;
    }
    
    .tool-checkbox span {
        font-size: 12px;
    }
    
    .tools-grid {
        grid-template-columns: 1fr;
    }
}

/* ========== ثيمات PDF ========== */
.pdf-theme-classic {
    --main: #062f25;
    --border: #2f9e8f;
    --bg: #ffffff;
}

.pdf-theme-professional {
    --main: #1a365d;
    --border: #4299e1;
    --bg: #ffffff;
}

.pdf-theme-professional .header {
    background: linear-gradient(135deg, #1a365d 0%, #2d3748 100%);
}

.pdf-theme-minimal {
    --main: #4a5568;
    --border: #cbd5e0;
    --bg: #ffffff;
}

.pdf-theme-minimal .header {
    background: #4a5568;
}

.pdf-theme-tech {
    --main: #2d3748;
    --border: #4fd1c7;
    --bg: #ffffff;
}

.pdf-theme-tech .header {
    background: linear-gradient(135deg, #2d3748 0%, #4a5568 100%);
}

.pdf-theme-educational {
    --main: #2b6cb0;
    --border: #4299e1;
    --bg: #ffffff;
}

.pdf-theme-educational .header {
    background: linear-gradient(135deg, #2b6cb0 0%, #3182ce 100%);
}
</style>
</head>

<body class="theme-default">

<!-- زر التعبئة الذكية العائم -->
<button id="aiFillFloatingBtn" onclick="fillWithAI()" title="تعبئة الحقول تلقائياً باستخدام الذكاء الاصطناعي">
    <i class="fas fa-wand-magic-sparkles floating-ai-icon"></i>
    <span class="floating-ai-text">تعبئة ذكية</span>
</button>

<!-- شاشة كود التفعيل -->
<div id="activationScreen">
    <div class="activation-box">
        <h3><i class="fas fa-lock"></i> تفعيل الأداة</h3>
        <p>أدخل كود التفعيل الذي حصلت عليه من المطور</p>
        <input id="activationCodeInput" placeholder="أدخل كود التفعيل هنا">
        <button onclick="activateTool()">تفعيل</button>
        <button id="contactForTrialBtn" onclick="contactForTrial()">
            <i class="fas fa-comments"></i>
            تواصل للتجربة أو الاشتراك
        </button>
        <div id="activationError">كود غير صالح. الرجاء التأكد من الكود والمحاولة مرة أخرى.</div>
    </div>
</div>

<!-- شريط الأخبار العلوي -->
<div class="top-marquee">
<div class="marquee-inner">
<i class="fas fa-bullhorn" style="margin-left:10px;"></i>
مرحباً بك في نظام تقاريرك - يمكنك إدخال البيانات يدوياً أو استخدام التعبئة الذكية
</div>
</div>

<!-- ========== المجموعة الأولى: الأزرار الصغيرة ========== -->
<div class="top-small-buttons">
    <div class="small-buttons-grid">
        <button class="small-btn" id="saveTeacherBtn" onclick="saveTeacherData()" title="حفظ بيانات المعلم والمدرسة">
            <i class="fas fa-save small-btn-icon"></i>
            <span class="small-btn-text">حفظ البيانات</span>
        </button>
        <button class="small-btn" id="clearBtn" onclick="clearData()" title="مسح جميع البيانات المدخلة">
            <i class="fas fa-trash-alt small-btn-icon"></i>
            <span class="small-btn-text">مسح البيانات</span>
        </button>
        <button class="small-btn" id="savedReportsBtn" onclick="openSavedReports()" title="عرض التقارير المحفوظة">
            <i class="fas fa-folder-open small-btn-icon"></i>
            <span class="small-btn-text">التقارير المحفوظة</span>
        </button>
        <button class="small-btn" id="settingsBtn" onclick="openSettings()" title="إعدادات الاشتراك">
            <i class="fas fa-cog small-btn-icon"></i>
            <span class="small-btn-text">الضبط</span>
        </button>
    </div>
</div>

<!-- ========== المجموعة الثانية: الأزرار الكبيرة ========== -->
<div class="main-buttons-bar">
    <div class="main-buttons-grid">
        <button class="main-btn" id="whatsappBtn" onclick="sharePDFWhatsApp()" title="مشاركة التقرير عبر واتساب">
            <i class="fab fa-whatsapp main-btn-icon"></i>
            <span class="main-btn-text">مشاركة واتساب</span>
        </button>
        <button class="main-btn" id="pdfBtn" onclick="downloadPDF()" title="تحويل التقرير إلى PDF وتنزيله">
            <i class="fas fa-file-pdf main-btn-icon"></i>
            <span class="main-btn-text">تنزيل PDF</span>
        </button>
    </div>
</div>

<!-- ========== شريط التقدم العلوي ========== -->
<div class="progress-bar-container" id="progressBarContainer">
    <div class="progress-header">
        <div><i class="fas fa-chart-line"></i> تقدم إنجاز التقارير</div>
        <div class="progress-stats">
            <span class="progress-percentage" id="progressPercentage">0%</span>
            <span class="progress-message" id="progressMessage"></span>
        </div>
    </div>
    <div class="progress-track">
        <div class="progress-fill" id="progressFill" style="width: 0%;"></div>
    </div>
    <div class="criteria-status" id="criteriaStatus"></div>
</div>

<!-- المحتوى الرئيسي -->
<div class="wrapper">
<div class="input-section">
  
  <h2><i class="fas fa-tools" style="margin-left:10px;"></i>تقاريرك - النظام المتكامل</h2>
  
  <!-- ========== القوائم المتتالية (اختيارية) ========== -->
  <div class="levels-container">
    <div class="level-indicator">
      <span>اختر المعايير والتصنيفات (اختياري)</span>
      <span><i class="fas fa-layer-group"></i> للمساعدة</span>
    </div>
    
    <!-- المستوى الأول: المعايير التربوية -->
    <div class="level-select">
      <label><i class="fas fa-star"></i> معيار الاداء الوظيفي</label>
      <select id="criterionSelect" onchange="loadSubcategories()">
        <option value="">اختر معيار الاداء الوظيفي (اختياري)</option>
      </select>
    </div>
    
    <!-- معلومات المعيار المحدد -->
    <div id="criterionInfo" class="criterion-info" style="display: none;">
      <span id="selectedCriterionName" class="criterion-name"></span>
      <span id="selectedCriterionWeight" class="criterion-weight"></span>
    </div>
    
    <!-- المستوى الثاني: التصنيفات الفرعية -->
    <div class="level-select">
      <label><i class="fas fa-list-ul"></i> التصنيف الفرعي</label>
      <select id="subcategorySelect" onchange="loadReports()" disabled>
        <option value="">اختر التصنيف الفرعي (اختياري)</option>
      </select>
    </div>
    
    <!-- المستوى الثالث: التقارير -->
    <div class="level-select">
      <label><i class="fas fa-file-alt"></i> التقرير</label>
      <select id="reportSelect" onchange="updateReportFromSelection()" disabled>
        <option value="">اختر التقرير (اختياري)</option>
      </select>
    </div>
    
    <!-- البحث المتقدم -->
    <div id="reportSearchContainer">
        <input type="text" id="reportSearch" placeholder="ابحث عن تقرير (اختياري)..." style="width:100%; padding:12px; border:2px solid #d4ebe2; border-radius:8px; font-size:14px;">
        <div id="searchResults"></div>
    </div>
    
    <!-- خانة عنوان التقرير اليدوية (إلزامي) -->
    <div class="manual-title-container">
        <label><i class="fas fa-heading"></i> عنوان التقرير <span style="color:#ff6b6b;">*</span></label>
        <input type="text" id="manualReportTitle" placeholder="أدخل عنوان التقرير (مثال: تقرير زيارة صفية)" oninput="updateReport()" required>
    </div>
  </div>
  
  <!-- حقول الإدخال الأساسية -->
  <div class="form-group">
    <label><i class="fas fa-university"></i>إدارة التعليم</label>
    <select id="education" oninput="updateReport()">
      <option value="">اختر إدارة التعليم</option>
    </select>
  </div>
  
  <div class="form-group">
    <label><i class="fas fa-school"></i>اسم المدرسة</label>
    <input id="school" value="مثال: مدرسة سعيد بن العاص" placeholder="أدخل اسم المدرسة" oninput="updateReport()">
  </div>
  
  <div class="form-row">
    <div class="form-group">
      <label><i class="fas fa-chalkboard-teacher"></i>صفة المعلّم</label>
      <select id="teacherType" oninput="updateReport()">
        <option value="المعلم">المعلم</option>
        <option value="المعلمة">المعلمة</option>
      </select>
    </div>
    
    <div class="form-group">
      <label><i class="fas fa-user"></i>اسم المعلّم</label>
      <input id="teacher" value="مثال: فهد الخالدي" placeholder="اسم المعلم" oninput="updateReport()">
    </div>
  </div>
  
  <div class="form-row">
    <div class="form-group">
      <label><i class="fas fa-user-tie"></i>صفة المدير</label>
      <select id="principalType" oninput="updateReport()">
        <option value="المدير">المدير</option>
        <option value="المديرة">المديرة</option>
      </select>
    </div>
    
    <div class="form-group">
      <label><i class="fas fa-user-cog"></i>اسم المدير</label>
      <input id="principal" value="مثال: نايف اللحياني" placeholder="اسم مدير المدرسة" oninput="updateReport()">
    </div>
  </div>
  
  <div class="form-row">
    <div class="form-group">
      <label><i class="fas fa-users-class"></i>الصف</label>
      <input id="grade" placeholder="مثال: ٥/٣" oninput="updateReport()">
    </div>
    
    <div class="form-group">
      <label><i class="fas fa-calendar-alt"></i>الفصل الدراسي</label>
      <select id="term" oninput="updateReport()">
        <option value="">اختر الفصل</option>
        <option value="الأول">الأول</option>
        <option value="الثاني">الثاني</option>
        <option value="الثالث">الثالث</option>
      </select>
    </div>
  </div>
  
  <div class="form-row">
    <div class="form-group">
      <label><i class="fas fa-book"></i>المادة</label>
      <input id="subject" placeholder="مثال: لغتي" oninput="updateReport()">
    </div>
    
    <div class="form-group">
      <label><i class="fas fa-book-open"></i>الدرس</label>
      <input id="lesson" placeholder="مثال: درس الضرب" oninput="updateReport()">
    </div>
  </div>
  
  <div class="form-row">
    <div class="form-group">
      <label><i class="fas fa-bullseye"></i>المستهدفون</label>
      <input id="target" placeholder="مثال: جميع طلاب الصف" oninput="updateReport()">
    </div>
    
    <div class="form-group">
      <label><i class="fas fa-user-check"></i>عدد الحضور</label>
      <input id="count" placeholder="مثال: ٢٥ طالب" oninput="updateReport()">
    </div>
  </div>
  
  <div class="form-group">
    <label><i class="fas fa-map-marker-alt"></i>مكان التنفيذ</label>
    <input id="place" placeholder="مثال: داخل الصف" oninput="updateReport()">
  </div>
  
  <div class="form-group">
    <label><i class="fas fa-flag"></i>الهدف التربوي</label>
    <textarea id="goal" placeholder="أدخل الهدف التربوي" oninput="updateReport()"></textarea>
  </div>
  
  <div class="form-group">
    <label><i class="fas fa-file-signature"></i>نبذة مختصرة</label>
    <textarea id="summary" placeholder="أدخل نبذة مختصرة عن التقرير" oninput="updateReport()"></textarea>
  </div>
  
  <div class="form-group">
    <label><i class="fas fa-tasks"></i>إجراءات التنفيذ</label>
    <textarea id="steps" placeholder="كيف تم تنفيذ النشاط؟" oninput="updateReport()"></textarea>
  </div>
  
  <div class="form-group">
    <label><i class="fas fa-chess-board"></i>الاستراتيجيات</label>
    <textarea id="strategies" placeholder="ما هي الاستراتيجيات المستخدمة" oninput="updateReport()"></textarea>
  </div>
  
  <div class="form-row">
    <div class="form-group">
      <label><i class="fas fa-thumbs-up"></i>نقاط القوة</label>
      <textarea id="strengths" placeholder="نقاط القوة في الحصة" oninput="updateReport()"></textarea>
    </div>
    
    <div class="form-group">
      <label><i class="fas fa-tools"></i>نقاط التحسين</label>
      <textarea id="improve" placeholder="نقاط تحتاج تطوير" oninput="updateReport()"></textarea>
    </div>
  </div>
  
  <div class="form-group">
    <label><i class="fas fa-lightbulb"></i>التوصيات</label>
    <textarea id="recomm" placeholder="توصيات مستقبلية" oninput="updateReport()"></textarea>
  </div>
  
  <!-- قسم الأدوات والوسائل التعليمية -->
  <div class="form-group">
    <label><i class="fas fa-tools"></i>الأدوات والوسائل التعليمية</label>
    <div class="tools-section" id="toolsSection">
      <div class="tools-grid" id="toolsGrid">
        <p style="text-align:center;color:#666;">جارٍ تحميل الأدوات التعليمية...</p>
      </div>
      <div style="text-align:center; margin-top:10px; font-size:11px; color:#666;">
        <i class="fas fa-info-circle"></i> اضغط على الأداة لتحديدها
      </div>
    </div>
  </div>
  
  <div class="form-row">
    <div class="form-group">
      <label><i class="fas fa-camera"></i>الصورة 1</label>
      <input type="file" accept="image/*" onchange="loadImage(this,'imgBox1')">
    </div>
    
    <div class="form-group">
      <label><i class="fas fa-camera"></i>الصورة 2</label>
      <input type="file" accept="image/*" onchange="loadImage(this,'imgBox2')">
    </div>
  </div>

</div>
</div>

<!-- قسم PDF -->
<div id="report-content" class="pdf-export" style="display:none;">
<div class="header">
  <img src="https://i.ibb.co/zH7k1s8c/IMG-2987.png" alt="شعار وزارة التعليم">
  <div class="header-school-title">اسم المدرسة</div>
  <div class="header-school" id="schoolBox"></div>
  <div class="header-education" id="educationBox"></div>
  <div class="header-date">
    <span id="hDate"></span><br>
    <span id="gDate"></span>
  </div>
</div>

<div class="info-grid">
  <div class="info-box"><div class="info-title">الفصل الدراسي</div><div class="info-value" id="termBox"></div></div>
  <div class="info-box"><div class="info-title">الصف</div><div class="info-value" id="gradeBox"></div></div>
  <div class="info-box"><div class="info-title">العدد</div><div class="info-value" id="countBox"></div></div>
  <div class="info-box"><div class="info-title">المستهدفون</div><div class="info-value" id="targetBox"></div></div>
</div>

<div class="info-grid2">
  <div class="info-box"><div class="info-title">نوع التقرير</div><div class="info-value" id="reportTypeBox"></div></div>

  <div class="subject-lesson-box">
    <div class="subject-lesson-title">المادة | الدرس</div>
    <div class="subject-lesson">
      <div id="subjectBox"></div>
      <div class="subject-divider"></div>
      <div id="lessonBox"></div>
    </div>
  </div>

  <div class="info-box"><div class="info-title">مكان التنفيذ</div><div class="info-value" id="placeBox"></div></div>
</div>

<div class="box-objective">
  <div class="box-title">الهدف التربوي</div>
  <div class="box-content" id="goalBox"></div>
</div>

<div class="row">
  <div class="box"><div class="box-title">النبذة</div><div class="box-content" id="summaryBox"></div></div>
  <div class="box"><div class="box-title">إجراءات التنفيذ</div><div class="box-content" id="stepsBox"></div></div>
</div>

<div class="row">
  <div class="box"><div class="box-title">الاستراتيجيات</div><div class="box-content" id="strategiesBox"></div></div>
  <div class="box"><div class="box-title">نقاط القوة</div><div class="box-content" id="strengthsBox"></div></div>
</div>

<div class="row">
  <div class="box"><div class="box-title">نقاط التحسين</div><div class="box-content" id="improveBox"></div></div>
  <div class="box"><div class="box-title">التوصيات</div><div class="box-content" id="recommBox"></div></div>
</div>

<div class="tools-box">
  <div class="tools-title">الأدوات والوسائل التعليمية</div>
  <div class="tools-list" id="toolsListBox"></div>
</div>

<div class="images">
  <div class="image-box" id="imgBox1"></div>
  <div class="image-box" id="imgBox2"></div>
</div>

<div class="signatures">
  <div class="signature-box">
    <div class="signature-role" id="teacherTypeBox"></div>
    <div class="signature-name" id="teacherBox"></div>
    <div class="sign-line"></div>
  </div>
  <div class="signature-box">
    <div class="signature-role" id="principalTypeBox"></div>
    <div class="signature-name" id="principalBox"></div>
    <div class="sign-line"></div>
  </div>
</div>

<div class="footer-box">
  وزارة التعليم – المملكة العربية السعودية
</div>
</div>

<!-- نافذة التقارير المحفوظة -->
<div id="savedReportsModal">
  <div>
    <h3><i class="fas fa-folder-open"></i> التقارير المحفوظة</h3>
    
    <div id="savedReportsList" class="reports-grid">
      <!-- سيتم تعبئتها ديناميكياً -->
    </div>
    
    <button class="close-reports-btn" onclick="closeSavedReports()">
      <i class="fas fa-times"></i> إغلاق
    </button>
  </div>
</div>

<!-- نافذة الإعدادات -->
<div id="settingsModal">
  <div>
    <h3><i class="fas fa-info-circle"></i> معلومات الاشتراك</h3>

    <div id="subInfo" style="font-size:14px;line-height:2;color:#333;text-align:center;">
      جارٍ التحميل...
    </div>

    <hr style="margin:15px 0;">

    <label style="font-weight:700;color:#044a35;display:block;">
      <i class="fas fa-calendar-alt"></i> تاريخ التقرير
    </label>

    <input type="date" id="customReportDate" style="
      width:100%;
      margin-top:8px;
      padding:10px;
      border-radius:8px;
      border:2px solid #d4ebe2;
      font-family:'Cairo';
    ">

    <button onclick="saveReportDate()" class="btn-secondary" style="
      margin-top:10px;
      width:100%;
      padding:10px;
      background:#4f7bff;
      color:white;
      border:none;
      border-radius:10px;
      font-weight:700;
      cursor:pointer;
    ">
      حفظ تاريخ التقرير
    </button>

    <hr style="margin:15px 0;">

    <h4 style="color:#044a35; margin-bottom:10px;">
        <i class="fas fa-palette"></i> تغيير الثيمات
    </h4>

    <div style="background:#f8fdfa; padding:15px; border-radius:10px; border:1px solid #d4ebe2; margin-bottom:15px;">
        <label style="display:block; font-weight:700; margin-bottom:8px; color:#044a35;">
            <i class="fas fa-desktop"></i> ثيم واجهة الأداة
        </label>
        <select id="appThemeSelect" style="width:100%; padding:10px; border-radius:8px; border:2px solid #d4ebe2; font-family:'Cairo'; background:white;">
            <option value="default">الثيم الافتراضي (فاتح)</option>
            <option value="light-blue">الأزرق الفاتح</option>
            <option value="dark">الوضع المظلم</option>
            <option value="green">الأخضر التربوي</option>
        </select>
    </div>

    <div style="background:#f8fdfa; padding:15px; border-radius:10px; border:1px solid #d4ebe2; margin-bottom:15px;">
        <label style="display:block; font-weight:700; margin-bottom:8px; color:#044a35;">
            <i class="fas fa-file-pdf"></i> ثيم ملف PDF
        </label>
        <select id="pdfThemeSelect" style="width:100%; padding:10px; border-radius:8px; border:2px solid #d4ebe2; font-family:'Cairo'; background:white;">
            <option value="classic">كلاسيكي (افتراضي)</option>
            <option value="professional">احترافي</option>
            <option value="minimal">ميني (بسيط)</option>
            <option value="tech">تقني</option>
            <option value="educational">تعليمي</option>
        </select>
    </div>

    <button onclick="applyThemes()" style="
      margin-top:5px;
      width:100%;
      padding:10px;
      background:#9D50BB;
      color:white;
      border:none;
      border-radius:10px;
      font-weight:700;
      cursor:pointer;
      display:flex;
      align-items:center;
      justify-content:center;
      gap:8px;
    ">
      <i class="fas fa-check"></i> تطبيق الثيمات
    </button>

    <button onclick="closeSettings()" style="
      margin-top:20px;
      width:100%;
      padding:12px;
      background:#066d4d;
      color:white;
      border:none;
      border-radius:10px;
      font-weight:700;
      cursor:pointer;
    ">
      إغلاق
    </button>
  </div>
</div>

<script>
// ==================== المتغيرات العامة ====================
window.__ACTIVATED__ = false;
window.allCriteria = [];
window.subcategoriesByCriterion = {};
window.reportsBySubcategory = {};
window.allReportsList = [];

const ACTIVATION_KEY_NAME = "activation_code";
const BACKEND_URL = "https://deep-qphc.onrender.com";
const APP_THEME_KEY = "app_theme";
const PDF_THEME_KEY = "pdf_theme";
const REPORTS_STORAGE_KEY = "saved_educational_reports";

let currentHijriDate = '';
let currentGregorianDate = '';
let educationalCriteria = [];

// ==================== دوال التفعيل ====================
function hideActivationScreen() {
    if (window.__ACTIVATED__) {
        document.getElementById("activationScreen").style.display = "none";
        document.body.style.overflow = "auto";
    }
}

function showActivationError() {
    document.getElementById("activationError").style.display = "block";
}

async function activateTool() {
    const code = document.getElementById("activationCodeInput").value.trim();
    if (!code) {
        showActivationError();
        return;
    }

    try {
        const res = await fetch(BACKEND_URL + "/health", {
            headers: { "X-Activation-Code": code }
        });

        if (!res.ok) throw new Error("Invalid");

        localStorage.setItem(ACTIVATION_KEY_NAME, code);
        window.__ACTIVATED__ = true;
        hideActivationScreen();
        showNotification("تم تفعيل الأداة بنجاح! ✓");

    } catch {
        showActivationError();
    }
}

function contactForTrial() {
    const message = encodeURIComponent("أرغب في تجربة أداة إصدار التقارير التربوية أو الاشتراك فيها.\n\nيرجى التواصل معي للمزيد من المعلومات.");
    window.open(`https://wa.me/966597077245?text=${message}`, '_blank');
}

// ==================== دوال التاريخ ====================
async function loadDates() {
    let g = new Date();
    currentGregorianDate = `${g.getDate()}/${g.getMonth()+1}/${g.getFullYear()}`;

    const customDate = localStorage.getItem("custom_report_date");
    if (customDate) {
        g = new Date(customDate);
        currentGregorianDate = `${g.getDate()}/${g.getMonth()+1}/${g.getFullYear()}`;
    }

    try {
        const response = await fetch(
            `https://api.aladhan.com/v1/gToH?date=${g.getDate()}-${g.getMonth()+1}-${g.getFullYear()}`
        );
        const data = await response.json();
        const hijri = data.data.hijri;

        const toArabic = n => n.toString().replace(/[0-9]/g, d => '٠١٢٣٤٥٦٧٨٩'[d]);

        currentHijriDate = `${toArabic(hijri.year)}/${toArabic(hijri.month.number)}/${toArabic(hijri.day)}`;

        document.getElementById('hDate').innerHTML = currentHijriDate + " هـ";
        document.getElementById('gDate').innerHTML = currentGregorianDate + " م";

    } catch (error) {
        console.error("خطأ في تحميل التاريخ:", error);
        currentHijriDate = "١٤٤٦/٠٦/٠١";
        document.getElementById('hDate').innerHTML = currentHijriDate + " هـ";
        document.getElementById('gDate').innerHTML = currentGregorianDate + " م";
    }
}

// ==================== دوال الثيمات ====================
function loadThemeSettings() {
    const savedAppTheme = localStorage.getItem(APP_THEME_KEY) || 'default';
    const appThemeSelect = document.getElementById('appThemeSelect');
    appThemeSelect.value = savedAppTheme;
    applyAppTheme(savedAppTheme);
    
    const savedPdfTheme = localStorage.getItem(PDF_THEME_KEY) || 'classic';
    const pdfThemeSelect = document.getElementById('pdfThemeSelect');
    pdfThemeSelect.value = savedPdfTheme;
    applyPdfTheme(savedPdfTheme);
}

function applyAppTheme(themeName) {
    document.body.classList.remove('theme-light-blue', 'theme-dark', 'theme-green', 'theme-default');
    document.body.classList.add('theme-' + themeName);
    updateAiButtonTheme(themeName);
    localStorage.setItem(APP_THEME_KEY, themeName);
}

function updateAiButtonTheme(themeName) {
    const aiButton = document.getElementById('aiFillFloatingBtn');
    const aiIcon = aiButton.querySelector('.floating-ai-icon');
    const aiText = aiButton.querySelector('.floating-ai-text');
    
    switch(themeName) {
        case 'light-blue':
            aiButton.style.background = 'linear-gradient(135deg, #4285f4 0%, #34a853 25%, #fbbc05 50%, #ea4335 100%)';
            aiButton.style.boxShadow = '0 12px 35px rgba(66, 133, 244, 0.6), 0 0 0 3px rgba(255, 255, 255, 0.3), 0 0 25px rgba(66, 133, 244, 0.5)';
            break;
        case 'dark':
            aiButton.style.background = 'linear-gradient(135deg, #6d28d9 0%, #7c3aed 25%, #8b5cf6 50%, #a78bfa 100%)';
            aiButton.style.boxShadow = '0 12px 35px rgba(109, 40, 217, 0.6), 0 0 0 3px rgba(255, 255, 255, 0.3), 0 0 25px rgba(109, 40, 217, 0.5)';
            break;
        case 'green':
            aiButton.style.background = 'linear-gradient(135deg, #27ae60 0%, #2ecc71 25%, #3498db 50%, #9b59b6 100%)';
            aiButton.style.boxShadow = '0 12px 35px rgba(46, 204, 113, 0.6), 0 0 0 3px rgba(255, 255, 255, 0.3), 0 0 25px rgba(46, 204, 113, 0.5)';
            break;
        default:
            aiButton.style.background = 'linear-gradient(135deg, #9D50BB 0%, #6E48AA 25%, #533D8B 50%, #3A2569 100%)';
            aiButton.style.boxShadow = '0 12px 35px rgba(157, 80, 187, 0.6), 0 0 0 3px rgba(255, 255, 255, 0.3), 0 0 25px rgba(157, 80, 187, 0.5)';
    }
    
    aiIcon.style.color = '#FFFFFF';
    aiText.style.background = 'linear-gradient(45deg, #FFFFFF, #F0F9F6, #FFFFFF)';
    aiText.style.webkitBackgroundClip = 'text';
    aiText.style.webkitTextFillColor = 'transparent';
    aiText.style.backgroundClip = 'text';
}

function applyPdfTheme(themeName) {
    const reportContent = document.getElementById('report-content');
    reportContent.classList.remove(
        'pdf-theme-classic', 'pdf-theme-professional', 'pdf-theme-minimal', 'pdf-theme-tech', 'pdf-theme-educational'
    );
    reportContent.classList.add('pdf-theme-' + themeName);
    localStorage.setItem(PDF_THEME_KEY, themeName);
}

function applyThemes() {
    const appTheme = document.getElementById('appThemeSelect').value;
    const pdfTheme = document.getElementById('pdfThemeSelect').value;
    applyAppTheme(appTheme);
    applyPdfTheme(pdfTheme);
    showNotification('تم تطبيق الثيمات بنجاح! ✓');
    closeSettings();
}

// ==================== دوال حفظ واستعراض التقارير ====================
function calculateProgress() {
    const savedReports = JSON.parse(localStorage.getItem(REPORTS_STORAGE_KEY)) || {};
    const criteria = educationalCriteria.length > 0 ? educationalCriteria : window.allCriteria || [];
    
    if (criteria.length === 0) {
        document.getElementById('progressBarContainer').style.display = 'none';
        return;
    }
    
    document.getElementById('progressBarContainer').style.display = 'flex';
    
    const totalWeight = criteria.reduce((sum, c) => sum + (parseFloat(c.weight) || 0), 0);
    let completedWeight = 0;
    const completedCriteria = [];
    const pendingCriteria = [];
    
    criteria.forEach(criterion => {
        const criterionId = criterion.id;
        const criterionWeight = parseFloat(criterion.weight) || 0;
        
        if (savedReports[criterionId]) {
            completedWeight += criterionWeight;
            completedCriteria.push(criterion);
        } else {
            pendingCriteria.push(criterion);
        }
    });
    
    const percentage = totalWeight > 0 ? Math.round((completedWeight / totalWeight) * 100) : 0;
    
    document.getElementById('progressPercentage').textContent = percentage + '%';
    document.getElementById('progressFill').style.width = percentage + '%';
    
    const completedCount = completedCriteria.length;
    const totalCount = criteria.length;
    document.getElementById('progressMessage').textContent = 
        `${completedCount} من ${totalCount} معايير مكتملة (${completedWeight} من ${totalWeight} نقطة)`;
    
    const criteriaStatus = document.getElementById('criteriaStatus');
    criteriaStatus.innerHTML = '';
    
    completedCriteria.forEach(criterion => {
        const badge = document.createElement('span');
        badge.className = 'criterion-badge completed';
        badge.innerHTML = `<i class="fas fa-check-circle"></i> ${criterion.name} <span class="criterion-weight">${criterion.weight}%</span>`;
        criteriaStatus.appendChild(badge);
    });
    
    pendingCriteria.forEach(criterion => {
        const badge = document.createElement('span');
        badge.className = 'criterion-badge';
        badge.innerHTML = `<i class="fas fa-hourglass-half"></i> ${criterion.name} <span class="criterion-weight">${criterion.weight}%</span>`;
        criteriaStatus.appendChild(badge);
    });
}

function saveCurrentReport() {
    const reportTitle = document.getElementById('manualReportTitle').value.trim();
    if (!reportTitle) {
        showNotification('الرجاء إدخال عنوان التقرير');
        return false;
    }
    
    const criterionId = document.getElementById('criterionSelect').value || 'manual_' + Date.now();
    const criterionName = document.getElementById('selectedCriterionName')?.textContent || 'تقرير يدوي';
    const criterionWeight = document.getElementById('selectedCriterionWeight')?.textContent || '0%';
    
    const savedReports = JSON.parse(localStorage.getItem(REPORTS_STORAGE_KEY)) || {};
    
    const reportData = {
        id: Date.now().toString(),
        title: reportTitle,
        criterionId: criterionId,
        criterionName: criterionName,
        weight: criterionWeight,
        date: currentGregorianDate,
        hijriDate: currentHijriDate,
        data: {
            education: document.getElementById('education').value,
            school: document.getElementById('school').value,
            teacherType: document.getElementById('teacherType').value,
            teacher: document.getElementById('teacher').value,
            principalType: document.getElementById('principalType').value,
            principal: document.getElementById('principal').value,
            grade: document.getElementById('grade').value,
            term: document.getElementById('term').value,
            subject: document.getElementById('subject').value,
            lesson: document.getElementById('lesson').value,
            target: document.getElementById('target').value,
            count: document.getElementById('count').value,
            place: document.getElementById('place').value,
            goal: document.getElementById('goal').value,
            summary: document.getElementById('summary').value,
            steps: document.getElementById('steps').value,
            strategies: document.getElementById('strategies').value,
            strengths: document.getElementById('strengths').value,
            improve: document.getElementById('improve').value,
            recomm: document.getElementById('recomm').value,
            tools: []
        }
    };
    
    const toolCheckboxes = document.querySelectorAll('.tool-checkbox input[type="checkbox"]');
    toolCheckboxes.forEach(checkbox => {
        if (checkbox.checked) {
            reportData.data.tools.push(checkbox.value);
        }
    });
    
    savedReports[criterionId] = reportData;
    localStorage.setItem(REPORTS_STORAGE_KEY, JSON.stringify(savedReports));
    
    calculateProgress();
    showNotification('تم حفظ التقرير بنجاح!');
    return true;
}

function loadSavedReport(criterionId) {
    const savedReports = JSON.parse(localStorage.getItem(REPORTS_STORAGE_KEY)) || {};
    const report = savedReports[criterionId];
    
    if (!report) return false;
    
    // تعبئة الحقول بالبيانات المحفوظة
    document.getElementById('education').value = report.data.education || '';
    document.getElementById('school').value = report.data.school || '';
    document.getElementById('teacherType').value = report.data.teacherType || 'المعلم';
    document.getElementById('teacher').value = report.data.teacher || '';
    document.getElementById('principalType').value = report.data.principalType || 'المدير';
    document.getElementById('principal').value = report.data.principal || '';
    document.getElementById('grade').value = report.data.grade || '';
    document.getElementById('term').value = report.data.term || '';
    document.getElementById('subject').value = report.data.subject || '';
    document.getElementById('lesson').value = report.data.lesson || '';
    document.getElementById('target').value = report.data.target || '';
    document.getElementById('count').value = report.data.count || '';
    document.getElementById('place').value = report.data.place || '';
    document.getElementById('goal').value = report.data.goal || '';
    document.getElementById('summary').value = report.data.summary || '';
    document.getElementById('steps').value = report.data.steps || '';
    document.getElementById('strategies').value = report.data.strategies || '';
    document.getElementById('strengths').value = report.data.strengths || '';
    document.getElementById('improve').value = report.data.improve || '';
    document.getElementById('recomm').value = report.data.recomm || '';
    document.getElementById('manualReportTitle').value = report.title || '';
    
    // تحديد الأدوات
    if (report.data.tools && Array.isArray(report.data.tools)) {
        const toolCheckboxes = document.querySelectorAll('.tool-checkbox');
        toolCheckboxes.forEach(toolElement => {
            const checkbox = toolElement.querySelector('input[type="checkbox"]');
            if (checkbox && report.data.tools.includes(checkbox.value)) {
                checkbox.checked = true;
                toolElement.classList.add('checked');
            } else {
                checkbox.checked = false;
                toolElement.classList.remove('checked');
            }
        });
    }
    
    updateReport();
    updateToolsDisplay();
    showNotification('تم تحميل التقرير بنجاح!');
    return true;
}

function deleteSavedReport(criterionId) {
    if (!confirm('هل أنت متأكد من حذف هذا التقرير؟')) return;
    
    const savedReports = JSON.parse(localStorage.getItem(REPORTS_STORAGE_KEY)) || {};
    delete savedReports[criterionId];
    localStorage.setItem(REPORTS_STORAGE_KEY, JSON.stringify(savedReports));
    
    calculateProgress();
    
    if (document.getElementById('savedReportsModal').style.display === 'flex') {
        closeSavedReports();
        setTimeout(openSavedReports, 300);
    }
    
    showNotification('تم حذف التقرير بنجاح!');
}

function openSavedReports() {
    const savedReports = JSON.parse(localStorage.getItem(REPORTS_STORAGE_KEY)) || {};
    const reportsList = document.getElementById('savedReportsList');
    
    if (Object.keys(savedReports).length === 0) {
        reportsList.innerHTML = `
            <div class="empty-reports">
                <i class="fas fa-folder-open"></i>
                <p>لا توجد تقارير محفوظة</p>
                <p style="font-size:12px; margin-top:10px;">قم بإنشاء تقرير وحفظه ليظهر هنا</p>
            </div>
        `;
    } else {
        reportsList.innerHTML = '';
        
        const reports = Object.values(savedReports).sort((a, b) => b.id - a.id);
        
        reports.forEach(report => {
            const card = document.createElement('div');
            card.className = 'report-card completed';
            card.innerHTML = `
                <div class="report-title">${report.title}</div>
                <div class="report-criterion"><i class="fas fa-star"></i> ${report.criterionName}</div>
                <div class="report-weight">الوزن: ${report.weight}</div>
                <div class="report-date"><i class="fas fa-calendar"></i> ${report.date} | ${report.hijriDate} هـ</div>
                <div class="report-actions">
                    <button class="load-btn" onclick="loadSavedReport('${report.criterionId}'); closeSavedReports();"><i class="fas fa-download"></i> تحميل</button>
                    <button class="delete-btn" onclick="deleteSavedReport('${report.criterionId}')"><i class="fas fa-trash"></i></button>
                </div>
            `;
            reportsList.appendChild(card);
        });
    }
    
    document.getElementById('savedReportsModal').style.display = 'flex';
}

function closeSavedReports() {
    document.getElementById('savedReportsModal').style.display = 'none';
}

// ==================== دوال تحميل البيانات ====================
async function loadDataFromBackend() {
    try {
        const structureResponse = await fetch(BACKEND_URL + "/api/full-structure");
        const structureData = await structureResponse.json();
        
        const structure = structureData.structure;
        
        window.allCriteria = structure;
        educationalCriteria = structure;
        
        const criterionSelect = document.getElementById("criterionSelect");
        criterionSelect.innerHTML = '<option value="">اختر معيار الاداء الوظيفي (اختياري)</option>';
        
        structure.forEach(criterion => {
            const option = document.createElement("option");
            option.value = criterion.id;
            option.textContent = `${criterion.name} (${criterion.weight}%)`;
            criterionSelect.appendChild(option);
            
            window.subcategoriesByCriterion[criterion.id] = criterion.subcategories || [];
            
            if (criterion.subcategories) {
                criterion.subcategories.forEach(sub => {
                    window.reportsBySubcategory[sub.id] = sub.reports || [];
                    
                    if (sub.reports) {
                        sub.reports.forEach(report => {
                            window.allReportsList.push({
                                id: report.id,
                                name: report.name,
                                subcategory_id: sub.id,
                                subcategory_name: sub.name,
                                criterion_id: criterion.id,
                                criterion_name: criterion.name
                            });
                        });
                    }
                });
            }
        });
        
        const educationResponse = await fetch(BACKEND_URL + "/api/education-offices");
        const educationOffices = await educationResponse.json();
        
        const educationSelect = document.getElementById("education");
        educationSelect.innerHTML = '<option value="">اختر إدارة التعليم</option>';
        
        educationOffices.forEach(office => {
            const option = document.createElement("option");
            option.value = office;
            option.textContent = office;
            educationSelect.appendChild(option);
        });
        
        const toolsResponse = await fetch(BACKEND_URL + "/api/educational-tools");
        const educationalTools = await toolsResponse.json();
        
        const toolsGrid = document.getElementById("toolsGrid");
        toolsGrid.innerHTML = "";
        
        educationalTools.forEach((tool, index) => {
            const toolId = `tool${index + 1}`;
            const label = document.createElement("label");
            label.className = "tool-checkbox";
            label.setAttribute("onclick", "toggleTool(this)");
            label.innerHTML = `
                <input type="checkbox" id="${toolId}" value="${tool}" style="display:none;">
                <span>${tool}</span>
                <span class="checkmark">✅</span>
            `;
            toolsGrid.appendChild(label);
        });
        
        calculateProgress();
        console.log("تم تحميل البيانات بنجاح");
        
    } catch (error) {
        console.error("خطأ في تحميل البيانات:", error);
        showNotification("حدث خطأ في تحميل البيانات. سيتم استخدام البيانات المحفوظة محلياً.");
    }
}

// ==================== دوال القوائم المتتالية ====================
function loadSubcategories() {
    const criterionId = document.getElementById('criterionSelect').value;
    const subcategorySelect = document.getElementById('subcategorySelect');
    const reportSelect = document.getElementById('reportSelect');
    const criterionInfo = document.getElementById('criterionInfo');
    
    if (!criterionId) {
        subcategorySelect.innerHTML = '<option value="">اختر التصنيف الفرعي (اختياري)</option>';
        subcategorySelect.disabled = true;
        reportSelect.innerHTML = '<option value="">اختر التقرير (اختياري)</option>';
        reportSelect.disabled = true;
        criterionInfo.style.display = 'none';
        return;
    }
    
    const criterion = window.allCriteria.find(c => c.id === criterionId);
    if (criterion) {
        document.getElementById('selectedCriterionName').textContent = criterion.name;
        document.getElementById('selectedCriterionWeight').textContent = criterion.weight + '%';
        criterionInfo.style.display = 'flex';
    }
    
    const subcategories = window.subcategoriesByCriterion[criterionId] || [];
    
    subcategorySelect.innerHTML = '<option value="">اختر التصنيف الفرعي (اختياري)</option>';
    subcategories.forEach(sub => {
        const option = document.createElement("option");
        option.value = sub.id;
        option.textContent = sub.name;
        subcategorySelect.appendChild(option);
    });
    
    subcategorySelect.disabled = false;
    reportSelect.innerHTML = '<option value="">اختر التقرير (اختياري)</option>';
    reportSelect.disabled = true;
}

function loadReports() {
    const subcategoryId = document.getElementById('subcategorySelect').value;
    const reportSelect = document.getElementById('reportSelect');
    
    if (!subcategoryId) {
        reportSelect.innerHTML = '<option value="">اختر التقرير (اختياري)</option>';
        reportSelect.disabled = true;
        return;
    }
    
    const reports = window.reportsBySubcategory[subcategoryId] || [];
    
    reportSelect.innerHTML = '<option value="">اختر التقرير (اختياري)</option>';
    reports.forEach(report => {
        const option = document.createElement("option");
        option.value = report.id;
        option.textContent = report.name;
        reportSelect.appendChild(option);
    });
    
    reportSelect.disabled = false;
}

function updateReportFromSelection() {
    const reportSelect = document.getElementById('reportSelect');
    const manualTitleInput = document.getElementById('manualReportTitle');
    
    if (reportSelect.value && reportSelect.selectedOptions[0]) {
        manualTitleInput.value = reportSelect.selectedOptions[0].textContent;
    }
    
    updateReport();
}

function handleReportSearch() {
    const reportSearch = document.getElementById('reportSearch');
    const searchResults = document.getElementById('searchResults');
    
    const searchTerm = reportSearch.value.trim().toLowerCase();
    
    if (searchTerm === '') {
        searchResults.style.display = 'none';
        searchResults.innerHTML = '';
        return;
    }
    
    const filteredReports = window.allReportsList.filter(report => 
        report.name.toLowerCase().includes(searchTerm)
    );
    
    if (filteredReports.length > 0) {
        searchResults.innerHTML = '';
        
        filteredReports.slice(0, 15).forEach(report => {
            const div = document.createElement('div');
            div.textContent = `${report.name} (${report.criterion_name})`;
            div.style.padding = '8px 12px';
            div.style.cursor = 'pointer';
            div.style.borderBottom = '1px solid #eee';
            
            div.onmouseover = () => div.style.backgroundColor = '#f0f9f6';
            div.onmouseout = () => div.style.backgroundColor = 'white';
            div.onclick = () => {
                const criterionSelect = document.getElementById('criterionSelect');
                criterionSelect.value = report.criterion_id;
                loadSubcategories();
                
                setTimeout(() => {
                    const subcategorySelect = document.getElementById('subcategorySelect');
                    subcategorySelect.value = report.subcategory_id;
                    loadReports();
                    
                    setTimeout(() => {
                        const reportSelect = document.getElementById('reportSelect');
                        reportSelect.value = report.id;
                        document.getElementById('manualReportTitle').value = report.name;
                        updateReport();
                    }, 100);
                }, 100);
                
                reportSearch.value = '';
                searchResults.style.display = 'none';
                showNotification(`تم تحديد التقرير: ${report.name}`);
            };
            searchResults.appendChild(div);
        });
        searchResults.style.display = 'block';
    } else {
        searchResults.innerHTML = '<div style="padding:12px; color:#666; text-align:center;">لا توجد نتائج</div>';
        searchResults.style.display = 'block';
    }
}

// ==================== دوال التعبئة الذكية ====================
async function fillWithAI() {
    const activationCode = localStorage.getItem(ACTIVATION_KEY_NAME);
    if (!activationCode) {
        alert('الرجاء تفعيل الأداة أولاً باستخدام كود التفعيل');
        return;
    }
    
    if (!navigator.onLine) {
        alert('لا يوجد اتصال بالإنترنت. الرجاء التأكد من الاتصال');
        return;
    }
    
    const reportName = document.getElementById('manualReportTitle').value.trim();
    if (!reportName) {
        alert('الرجاء إدخال عنوان التقرير أولاً');
        return;
    }
    
    const criterionId = document.getElementById('criterionSelect').value;
    const subcategoryId = document.getElementById('subcategorySelect').value;
    const reportId = document.getElementById('reportSelect').value;
    
    const aiButton = document.getElementById('aiFillFloatingBtn');
    const originalText = aiButton.querySelector('.floating-ai-text').textContent;
    const originalIcon = aiButton.querySelector('.floating-ai-icon').className;
    
    aiButton.classList.add('loading');
    aiButton.querySelector('.floating-ai-text').textContent = 'جارٍ...';
    aiButton.querySelector('.floating-ai-icon').className = 'fas fa-spinner fa-spin floating-ai-icon';
    aiButton.disabled = true;
    
    try {
        // حتى لو لم يتم اختيار معايير، نرسل الطلب مع بيانات افتراضية
        const response = await fetch(BACKEND_URL + "/api/generate-report-content", {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
                'X-Activation-Code': activationCode
            },
            body: JSON.stringify({
                criterion_id: criterionId || 'default',
                subcategory_id: subcategoryId || 'default',
                report_id: reportId || 'default',
                report_data: {
                    subject: document.getElementById('subject').value || 'الموضوع',
                    lesson: document.getElementById('lesson').value || 'الدرس',
                    grade: document.getElementById('grade').value || 'الصف',
                    target: document.getElementById('target').value || 'الطلاب',
                    place: document.getElementById('place').value || 'المدرسة',
                    count: document.getElementById('count').value || 'عدد الطلاب'
                }
            })
        });

        if (!response.ok) throw new Error("تعذر تنفيذ الطلب");

        const data = await response.json();
        
        if (!data || !data.content) {
            throw new Error('لم يتم الحصول على إجابة من الذكاء الاصطناعي');
        }
        
        parseAIResponseProfessional(data.content);
        showNotification('تم تعبئة الحقول باستخدام الذكاء الاصطناعي بنجاح! ✓');
        saveCurrentReport();
        
    } catch (error) {
        console.error('خطأ في الذكاء الاصطناعي:', error);
        alert(error.message || "تعذر تنفيذ الطلب.");
    } finally {
        aiButton.classList.remove('loading');
        aiButton.querySelector('.floating-ai-text').textContent = originalText;
        aiButton.querySelector('.floating-ai-icon').className = originalIcon;
        aiButton.disabled = false;
        updateAiButtonTheme(localStorage.getItem(APP_THEME_KEY) || 'default');
    }
}

// ==================== دوال مساعدة ====================
function adaptSubjectLessonFont() {
    const elements = [
        document.getElementById('subjectBox'),
        document.getElementById('lessonBox')
    ];

    elements.forEach(el => {
        if (!el || !el.parentElement) return;

        const text = el.innerText.trim();
        const textLength = text.length;
        const container = el.parentElement;
        const containerWidth = container.clientWidth - 30;
        const containerHeight = container.clientHeight - 20;

        el.style.whiteSpace = 'nowrap';
        el.style.overflow = 'hidden';
        el.style.textOverflow = 'ellipsis';
        el.style.textAlign = 'center';
        el.style.display = 'flex';
        el.style.alignItems = 'center';
        el.style.justifyContent = 'center';
        el.style.padding = '0 5px';
        el.style.width = '100%';
        el.style.height = '100%';

        if (!text || text === 'غير محدد' || textLength === 0) {
            el.style.fontSize = '11px';
            el.style.fontWeight = '600';
            el.style.lineHeight = '1.2';
            return;
        }

        const approxCharWidth = 7;
        const approxTextWidth = textLength * approxCharWidth;
        const widthRatio = approxTextWidth / containerWidth;
        
        let fontSize, fontWeight, lineHeight;
        
        if (widthRatio > 2.0) {
            fontSize = '7px';
            fontWeight = '600';
            lineHeight = '1.0';
            el.style.whiteSpace = 'normal';
            el.style.display = '-webkit-box';
            el.style.WebkitLineClamp = '2';
            el.style.WebkitBoxOrient = 'vertical';
        } else if (widthRatio > 1.2) {
            fontSize = '8px';
            fontWeight = '600';
            lineHeight = '1.1';
        } else if (widthRatio > 0.8) {
            fontSize = '9px';
            fontWeight = '700';
            lineHeight = '1.2';
        } else if (widthRatio > 0.5) {
            fontSize = '10px';
            fontWeight = '800';
            lineHeight = '1.3';
        } else {
            fontSize = '12px';
            fontWeight = '900';
            lineHeight = '1.4';
        }

        if (containerHeight < 30) {
            fontSize = Math.min(parseInt(fontSize), 9) + 'px';
            lineHeight = '1.1';
        }

        el.style.fontSize = fontSize;
        el.style.fontWeight = fontWeight;
        el.style.lineHeight = lineHeight;
    });
}

function adaptSubjectLessonFontWithRetry() {
    adaptSubjectLessonFont();
    setTimeout(adaptSubjectLessonFont, 100);
}

function updateReport() {
    document.getElementById('educationBox').innerText = document.getElementById('education').value || 'غير محدد';
    document.getElementById('schoolBox').innerText = document.getElementById('school').value || 'غير محدد';
    
    const termValue = document.getElementById('term').value;
    document.getElementById('termBox').innerText = termValue ? `الفصل الدراسي ${termValue}` : 'غير محدد';
    document.getElementById('gradeBox').innerText = document.getElementById('grade').value || 'غير محدد';
    document.getElementById('countBox').innerText = document.getElementById('count').value || 'غير محدد';
    document.getElementById('reportTypeBox').innerText = document.getElementById('manualReportTitle').value || 'تقرير';
    document.getElementById('targetBox').innerText = document.getElementById('target').value || 'غير محدد';
    document.getElementById('placeBox').innerText = document.getElementById('place').value || 'غير محدد';
    document.getElementById('subjectBox').innerText = document.getElementById('subject').value || 'غير محدد';
    document.getElementById('lessonBox').innerText = document.getElementById('lesson').value || 'غير محدد';
    
    document.getElementById('teacherBox').innerText = document.getElementById('teacher').value || 'غير محدد';
    document.getElementById('principalBox').innerText = document.getElementById('principal').value || 'غير محدد';
    document.getElementById('teacherTypeBox').innerText = document.getElementById('teacherType').value || 'المعلم';
    document.getElementById('principalTypeBox').innerText = document.getElementById('principalType').value || 'المدير';
    
    document.getElementById('goalBox').innerText = document.getElementById('goal').value || 'لم يتم تحديد الهدف التربوي';
    document.getElementById('summaryBox').innerText = document.getElementById('summary').value || 'لم يتم إضافة نبذة مختصرة';
    document.getElementById('stepsBox').innerText = document.getElementById('steps').value || 'لم يتم تحديد إجراءات التنفيذ';
    document.getElementById('strategiesBox').innerText = document.getElementById('strategies').value || 'لم يتم تحديد الاستراتيجيات';
    document.getElementById('strengthsBox').innerText = document.getElementById('strengths').value || 'لم يتم تحديد نقاط القوة';
    document.getElementById('improveBox').innerText = document.getElementById('improve').value || 'لم يتم تحديد نقاط التحسين';
    document.getElementById('recommBox').innerText = document.getElementById('recomm').value || 'لم يتم تحديد التوصيات';
    
    updateToolsDisplay();
    setTimeout(adaptSubjectLessonFontWithRetry, 10);
}

function toggleTool(element) {
    const checkbox = element.querySelector('input[type="checkbox"]');
    checkbox.checked = !checkbox.checked;
    if (checkbox.checked) {
        element.classList.add('checked');
    } else {
        element.classList.remove('checked');
    }
    updateToolsDisplay();
}

function updateToolsDisplay() {
    const toolsListBox = document.getElementById('toolsListBox');
    toolsListBox.innerHTML = '';
    
    const selectedTools = [];
    
    const toolCheckboxes = document.querySelectorAll('.tool-checkbox input[type="checkbox"]');
    toolCheckboxes.forEach(checkbox => {
        if (checkbox.checked) {
            selectedTools.push(checkbox.value);
        }
    });
    
    selectedTools.forEach(tool => {
        const toolElement = document.createElement('div');
        toolElement.className = 'tool';
        toolElement.innerHTML = `<span>✓</span> ${tool}`;
        toolsListBox.appendChild(toolElement);
    });
    
    if (selectedTools.length === 0) {
        const noToolsMessage = document.createElement('div');
        noToolsMessage.style.textAlign = 'center';
        noToolsMessage.style.color = '#666';
        noToolsMessage.style.fontSize = '9px';
        noToolsMessage.style.padding = '4px';
        noToolsMessage.textContent = 'لم يتم اختيار أي أدوات';
        toolsListBox.appendChild(noToolsMessage);
    }
}

function loadImage(input, target) {
    if (input.files && input.files[0]) {
        const reader = new FileReader();
        reader.onload = function(e) {
            const imgBox = document.getElementById(target);
            imgBox.innerHTML = '';
            const img = document.createElement('img');
            img.src = e.target.result;
            imgBox.appendChild(img);
        };
        reader.readAsDataURL(input.files[0]);
    }
}

function saveTeacherData() {
    saveCurrentReport();
    
    const teacherData = {
        education: document.getElementById('education').value,
        school: document.getElementById('school').value,
        grade: document.getElementById('grade').value,
        subject: document.getElementById('subject').value,
        target: document.getElementById('target').value,
        place: document.getElementById('place').value,
        lesson: document.getElementById('lesson').value,
        teacher: document.getElementById('teacher').value,
        principal: document.getElementById('principal').value,
        teacherType: document.getElementById('teacherType').value,
        principalType: document.getElementById('principalType').value,
        term: document.getElementById('term').value,
        count: document.getElementById('count').value,
        manualTitle: document.getElementById('manualReportTitle').value,
        criterion: document.getElementById('criterionSelect').value,
        subcategory: document.getElementById('subcategorySelect').value,
        report: document.getElementById('reportSelect').value,
        tools: []
    };
    
    const toolCheckboxes = document.querySelectorAll('.tool-checkbox input[type="checkbox"]');
    toolCheckboxes.forEach(checkbox => {
        if (checkbox.checked) {
            teacherData.tools.push(checkbox.value);
        }
    });
    
    const textFields = ['goal', 'summary', 'steps', 'strategies', 'strengths', 'improve', 'recomm'];
    textFields.forEach(field => {
        teacherData[field] = document.getElementById(field).value;
    });
    
    localStorage.setItem('teacherData', JSON.stringify(teacherData));
    showNotification('تم حفظ بيانات المعلم بنجاح!');
}

function showNotification(message) {
    const notification = document.createElement('div');
    notification.className = 'notification';
    notification.innerHTML = `<i class="fas fa-check-circle"></i><span>${message}</span>`;
    document.body.appendChild(notification);
    
    setTimeout(() => {
        notification.classList.add('show');
    }, 10);
    
    setTimeout(() => {
        notification.classList.remove('show');
        setTimeout(() => {
            document.body.removeChild(notification);
        }, 400);
    }, 3000);
}

function loadTeacherData() {
    const savedData = localStorage.getItem('teacherData');
    
    if (savedData) {
        const teacherData = JSON.parse(savedData);
        
        document.getElementById('education').value = teacherData.education || '';
        document.getElementById('school').value = teacherData.school || '';
        document.getElementById('grade').value = teacherData.grade || '';
        document.getElementById('subject').value = teacherData.subject || '';
        document.getElementById('target').value = teacherData.target || '';
        document.getElementById('place').value = teacherData.place || '';
        document.getElementById('lesson').value = teacherData.lesson || '';
        document.getElementById('teacher').value = teacherData.teacher || '';
        document.getElementById('principal').value = teacherData.principal || '';
        document.getElementById('teacherType').value = teacherData.teacherType || 'المعلم';
        document.getElementById('principalType').value = teacherData.principalType || 'المدير';
        document.getElementById('term').value = teacherData.term || '';
        document.getElementById('count').value = teacherData.count || '';
        document.getElementById('manualReportTitle').value = teacherData.manualTitle || '';
        
        const textFields = ['goal', 'summary', 'steps', 'strategies', 'strengths', 'improve', 'recomm'];
        textFields.forEach(field => {
            if (teacherData[field]) {
                document.getElementById(field).value = teacherData[field];
            }
        });
        
        if (teacherData.tools && Array.isArray(teacherData.tools)) {
            const toolCheckboxes = document.querySelectorAll('.tool-checkbox');
            toolCheckboxes.forEach(toolElement => {
                const checkbox = toolElement.querySelector('input[type="checkbox"]');
                if (checkbox && teacherData.tools.includes(checkbox.value)) {
                    checkbox.checked = true;
                    toolElement.classList.add('checked');
                }
            });
        }
        
        updateReport();
        updateToolsDisplay();
    }
}

function parseAIResponseProfessional(response) {
    const lines = response.split('\n').filter(line => line.trim());
    
    const fieldMapping = {
        '1': 'goal', '2': 'summary', '3': 'steps', '4': 'strategies',
        '5': 'strengths', '6': 'improve', '7': 'recomm'
    };
    
    let foundFields = 0;
    
    lines.forEach(line => {
        const match = line.match(/^(\d+)[\.\-]\s*(.+)/);
        if (match) {
            const fieldNumber = match[1];
            let content = match[2].trim();
            
            content = removeFieldTitles(content);
            
            if (fieldMapping[fieldNumber]) {
                const fieldId = fieldMapping[fieldNumber];
                content = ensureWordCount(content, 25);
                document.getElementById(fieldId).value = content;
                foundFields++;
            }
        }
    });
    
    if (foundFields < 3) {
        fallbackProfessionalAIParsing(response);
    }
    
    updateReport();
}

function removeFieldTitles(content) {
    const fieldTitles = [
        'الهدف التربوي', 'نبذة مختصرة', 'إجراءات التنفيذ', 'الاستراتيجيات',
        'نقاط القوة', 'نقاط التحسين', 'التوصيات', 'هو:', 'تشمل:', 'يتضمن:',
        'يتمثل في', 'يشمل', 'تحتوي', 'تتضمن'
    ];
    
    let cleanedContent = content;
    
    fieldTitles.forEach(title => {
        const regex = new RegExp(`^${title}[:\\.\\-]?\\s*`, 'i');
        cleanedContent = cleanedContent.replace(regex, '');
        const regex2 = new RegExp(`\\s*${title}[:\\.\\-]?\\s*`, 'gi');
        cleanedContent = cleanedContent.replace(regex2, ' ');
    });
    
    return cleanedContent.trim().replace(/\s+/g, ' ') || content;
}

function ensureWordCount(content, targetWords) {
    const words = content.split(' ');
    
    if (words.length >= targetWords - 5 && words.length <= targetWords + 5) {
        return content;
    }
    
    if (words.length < targetWords - 5) {
        const professionalPhrases = [
            'مع التركيز على تحقيق أهداف التعلم وتنمية المهارات الأساسية',
            'بما يسهم في رفع مستوى التحصيل الدراسي وتحسين المخرجات التعليمية',
            'مع مراعاة الفروق الفردية وتنويع أساليب التدريس',
            'لضمان تحقيق رؤية التعليم وتطوير العملية التعليمية',
            'مع الاستفادة من أفضل الممارسات التربوية والتقنيات التعليمية الحديثة'
        ];
    
        let extendedContent = content;
        while (extendedContent.split(' ').length < targetWords) {
            const randomPhrase = professionalPhrases[Math.floor(Math.random() * professionalPhrases.length)];
            extendedContent += ' ' + randomPhrase;
        }
        
        return extendedContent;
    }
    
    return words.slice(0, targetWords).join(' ');
}

function fallbackProfessionalAIParsing(response) {
    const sentences = response.split(/[\.\n]/).filter(s => {
        const trimmed = s.trim();
        return trimmed.length > 20 && 
               !trimmed.match(/الهدف التربوي|نبذة مختصرة|إجراءات التنفيذ|الاستراتيجيات|نقاط القوة|نقاط التحسين|التوصيات/i);
    });
    
    const fields = ['goal', 'summary', 'steps', 'strategies', 'strengths', 'improve', 'recomm'];
    
    let sentenceIndex = 0;
    fields.forEach((field, index) => {
        if (sentenceIndex < sentences.length) {
            let content = sentences[sentenceIndex].trim();
            content = removeFieldTitles(content);
            content = ensureWordCount(content, 25);
            document.getElementById(field).value = content;
            sentenceIndex++;
        }
    });
}

function clearData() {
    if (confirm("هل أنت متأكد من مسح جميع البيانات؟")) {
        localStorage.clear();
        location.reload();
    }
}

async function downloadPDF() {
    await loadDates();
    
    document.querySelector('.top-small-buttons').style.visibility = 'hidden';
    document.querySelector('.main-buttons-bar').style.visibility = 'hidden';
    document.querySelector('.top-marquee').style.visibility = 'hidden';
    document.querySelector('.progress-bar-container').style.visibility = 'hidden';
    document.getElementById('aiFillFloatingBtn').style.visibility = 'hidden';
    document.body.style.margin = "0";
    document.body.style.background = "white";

    const reportContent = document.getElementById('report-content');
    reportContent.style.display = 'block';
    reportContent.style.visibility = 'visible';
    reportContent.style.opacity = '1';
    reportContent.style.position = 'relative';
    reportContent.style.top = '0';
    reportContent.style.left = '0';

    const cleanFileName = document.getElementById('manualReportTitle').value.replace(/[\/\\:*?"<>|]/g, '_') || 'تقرير';

    await new Promise(resolve => setTimeout(resolve, 300));

    html2pdf().set({
        filename: cleanFileName + ".pdf",
        html2canvas: {
            scale: 3,
            useCORS: true,
            scrollY: 0,
            backgroundColor: '#ffffff',
            onclone: function(clonedDoc) {
                clonedDoc.getElementById('report-content').style.background = '#ffffff';
                clonedDoc.querySelectorAll('*').forEach(el => {
                    el.style.color = '';
                    el.style.backgroundColor = '';
                });
            }
        },
        jsPDF: {unit: "mm", format: "a4", orientation: "portrait"}
    })
    .from(reportContent)
    .save()
    .then(() => {
        document.querySelector('.top-small-buttons').style.visibility = 'visible';
        document.querySelector('.main-buttons-bar').style.visibility = 'visible';
        document.querySelector('.top-marquee').style.visibility = 'visible';
        document.querySelector('.progress-bar-container').style.visibility = 'visible';
        document.getElementById('aiFillFloatingBtn').style.visibility = 'visible';
        document.body.style.margin = "";
        document.body.style.background = "#f9fcfb";
        reportContent.style.display = 'none';
        showNotification("تم تنزيل التقرير بصيغة PDF ✓");
    });
}

async function sharePDFWhatsApp() {
    await loadDates();
    
    document.querySelector('.top-small-buttons').style.visibility = 'hidden';
    document.querySelector('.main-buttons-bar').style.visibility = 'hidden';
    document.querySelector('.top-marquee').style.visibility = 'visible';
    document.querySelector('.progress-bar-container').style.visibility = 'hidden';
    document.getElementById('aiFillFloatingBtn').style.visibility = 'hidden';
    document.body.style.margin = "0";
    document.body.style.background = "white";

    const reportContent = document.getElementById('report-content');
    reportContent.style.display = 'block';
    reportContent.style.visibility = 'visible';
    reportContent.style.opacity = '1';
    reportContent.style.position = 'relative';
    reportContent.style.top = '0';
    reportContent.style.left = '0';

    const reportName = document.getElementById('manualReportTitle').value || 'تقرير';

    await new Promise(resolve => setTimeout(resolve, 300));

    await html2pdf().set({
        margin: 0,
        image: {type: "jpeg", quality: 1},
        html2canvas: {
            scale: 3,
            scrollY: 0,
            useCORS: true,
            backgroundColor: '#ffffff',
            onclone: function(clonedDoc) {
                clonedDoc.getElementById('report-content').style.background = '#ffffff';
            }
        },
        jsPDF: {unit: "mm", format: "a4", orientation: "portrait"}
    })
    .from(reportContent)
    .toPdf()
    .output('blob')
    .then((pdfBlob) => {
        document.querySelector('.top-small-buttons').style.visibility = 'visible';
        document.querySelector('.main-buttons-bar').style.visibility = 'visible';
        document.querySelector('.top-marquee').style.visibility = 'visible';
        document.querySelector('.progress-bar-container').style.visibility = 'visible';
        document.getElementById('aiFillFloatingBtn').style.visibility = 'visible';
        document.body.style.margin = "";
        document.body.style.background = "#f9fcfb";
        reportContent.style.display = 'none';

        let file = new File([pdfBlob], reportName + ".pdf", {type: "application/pdf"});
        if (navigator.canShare && navigator.canShare({files:[file]})) {
            navigator.share({
                files:[file], 
                title: reportName,
                text: "تقرير: " + reportName
            });
        } else {
            let url = URL.createObjectURL(pdfBlob);
            window.open(`https://wa.me/?text=${encodeURIComponent("تقرير: " + reportName + "\n\n" + url)}`, "_blank");
        }
    });
}

// ==================== دوال نافذة الإعدادات ====================
function openSettings() {
    document.getElementById("settingsModal").style.display = "flex";
    loadSavedReportDate();
    loadSubscriptionStatus();
}

function closeSettings() {
    document.getElementById("settingsModal").style.display = "none";
}

async function loadSubscriptionStatus() {
    const code = localStorage.getItem(ACTIVATION_KEY_NAME);
    if (!code) {
        document.getElementById("subInfo").innerHTML = "لم يتم تفعيل الأداة بعد<br>يرجى استخدام كود التفعيل";
        return;
    }

    try {
        const res = await fetch(BACKEND_URL + "/subscription/status", {
            headers: { "X-Activation-Code": code }
        });

        if (!res.ok) throw new Error();

        const data = await res.json();
        const expires = data.expires_at ? new Date(data.expires_at).toLocaleDateString('ar-SA') : "غير محدد";

        document.getElementById("subInfo").innerHTML = `
            <div>📅 <strong>تاريخ الانتهاء:</strong> ${expires}</div>
            <div>📊 <strong>الاستخدام:</strong> ${data.usage_used} / ${data.usage_limit}</div>
            <div>🔋 <strong>المتبقي:</strong> ${data.usage_remaining}</div>
        `;
    } catch {
        document.getElementById("subInfo").innerHTML = "تعذر تحميل معلومات الاشتراك<br>يرجى التأكد من اتصال الإنترنت";
    }
}

function saveReportDate() {
    const date = document.getElementById("customReportDate").value;
    if (date) {
        localStorage.setItem("custom_report_date", date);
        showNotification("تم حفظ تاريخ التقرير ✓");
        closeSettings();
        loadDates();
    } else {
        showNotification("يرجى اختيار تاريخ صحيح");
    }
}

function loadSavedReportDate() {
    const saved = localStorage.getItem("custom_report_date");
    if (saved) {
        document.getElementById("customReportDate").value = saved;
    }
}

// ==================== التهيئة ====================
document.addEventListener("DOMContentLoaded", async () => {
    const code = localStorage.getItem(ACTIVATION_KEY_NAME);

    if (!code) {
        document.getElementById("activationScreen").style.display = "flex";
        document.body.style.overflow = "hidden";
    } else {
        try {
            const res = await fetch(BACKEND_URL + "/health", {
                headers: { "X-Activation-Code": code }
            });
            
            if (res.ok) {
                window.__ACTIVATED__ = true;
                hideActivationScreen();
            } else {
                throw new Error();
            }
        } catch {
            localStorage.removeItem(ACTIVATION_KEY_NAME);
            document.getElementById("activationScreen").style.display = "flex";
            document.body.style.overflow = "hidden";
        }
    }

    await loadDates();
    loadThemeSettings();
    await loadDataFromBackend();
    loadTeacherData();
    updateReport();

    document.getElementById('reportSearch').addEventListener('input', handleReportSearch);

    document.addEventListener('click', function(event) {
        const searchResults = document.getElementById('searchResults');
        if (!event.target.closest('#reportSearchContainer')) {
            searchResults.style.display = 'none';
        }
    });

    window.addEventListener('resize', adaptSubjectLessonFont);

    document.addEventListener('input', function(e) {
        if (e.target.id === 'subject' || e.target.id === 'lesson') {
            setTimeout(adaptSubjectLessonFont, 50);
        }
    });
});
</script>

</body>
</html>