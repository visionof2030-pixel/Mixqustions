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
*{margin:0;padding:0;box-sizing:border-box; -webkit-tap-highlight-color: transparent;}
html,body{font-family:'Cairo',sans-serif;background: linear-gradient(135deg, #f0f9f6 0%, #e8f4f0 50%, #d4ebe2 100%);direction:rtl;overflow-x:hidden;min-height:100vh;-webkit-text-size-adjust:100%; -moz-text-size-adjust:100%; -ms-text-size-adjust:100%; text-size-adjust:100%; touch-action: manipulation;}
.wrapper{max-width:900px;margin:auto;padding:20px;width:100%;}

/* شريط الأخبار العلوي */
.top-marquee{
position:fixed;top:0;left:0;right:0;width:100%;background:linear-gradient(135deg, #022e22 0%, #044a35 100%);color:#fff;
padding:10px 5px;font-size:12px;z-index:300;overflow:hidden;height:45px;
white-space:nowrap;border-bottom:3px solid #ffd166;box-shadow:0 4px 12px rgba(2, 46, 34, 0.25);
display:flex;align-items:center;
}
.marquee-inner{
display:inline-block;
padding-left:2%;
animation:newsScroll 30s linear infinite;
color:#e8f4f0;font-weight:500;
}
@keyframes newsScroll{
0%{transform:translateX(-100%);}
100%{transform:translateX(100%);}
}
.top-marquee:hover .marquee-inner{animation-play-state:paused;}

/* ==================== نظام الأزرار المحسّن ==================== */

/* إعادة تعيين موحد لجميع الأزرار */
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

/* المجموعة الأولى: الأزرار الصغيرة أعلى الهيدر */
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
    max-width: 500px;
    justify-content: center;
}

/* تصميم الأزرار الصغيرة */
.small-btn {
    border: 2px solid;
    padding: 6px 4px;
    font-size: 9px;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
    font-weight: 700;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 3px;
    min-height: 40px;
    min-width: 80px;
    box-shadow: 0 1px 4px rgba(0,0,0,0.1);
    flex: 1;
    position: relative;
    overflow: hidden;
}

/* إزالة تأثيرات الحركة والاهتزاز */
.small-btn:active,
.small-btn:focus,
.small-btn:hover {
    transform: none !important;
    line-height: inherit !important;
    font-weight: 700 !important;
    height: auto !important;
    width: auto !important;
}

/* تأثير الضغط الخفيف */
.small-btn:active {
    box-shadow: 0 0 0 2px rgba(255,255,255,0.5), inset 0 3px 5px rgba(0,0,0,0.1) !important;
    filter: brightness(0.95);
}

/* زر حفظ البيانات - أزرق */
#saveTeacherBtn {
    background: linear-gradient(135deg, #4f7bff 0%, #3b5bdb 100%);
    color: white;
    border-color: #3b5bdb;
}

#saveTeacherBtn:hover {
    background: linear-gradient(135deg, #3b5bdb 0%, #2d4ac0 100%);
    filter: brightness(1.05);
    box-shadow: 0 3px 8px rgba(59, 91, 219, 0.3);
}

#saveTeacherBtn:active {
    filter: brightness(0.9);
}

/* زر مسح البيانات - أصفر */
#clearBtn {
    background: linear-gradient(135deg, #ffd166 0%, #ffc145 100%);
    color: #5a3e00;
    border-color: #ffc145;
}

#clearBtn:hover {
    background: linear-gradient(135deg, #ffc145 0%, #ffb830 100%);
    filter: brightness(1.05);
    box-shadow: 0 3px 8px rgba(255, 193, 69, 0.3);
}

#clearBtn:active {
    filter: brightness(0.9);
}

/* زر الضبط - رمادي */
#settingsBtn {
    background: linear-gradient(135deg, #718096 0%, #4a5568 100%);
    color: white;
    border-color: #4a5568;
}

#settingsBtn:hover {
    background: linear-gradient(135deg, #4a5568 0%, #2d3748 100%);
    filter: brightness(1.05);
    box-shadow: 0 3px 8px rgba(74, 85, 104, 0.3);
}

#settingsBtn:active {
    filter: brightness(0.9);
}

/* زر التقارير المحفوظة - جديد */
#savedReportsBtn {
    background: linear-gradient(135deg, #9D50BB 0%, #6E48AA 100%);
    color: white;
    border-color: #6E48AA;
}

#savedReportsBtn:hover {
    background: linear-gradient(135deg, #6E48AA 0%, #533D8B 100%);
    filter: brightness(1.05);
    box-shadow: 0 3px 8px rgba(157, 80, 187, 0.3);
}

#savedReportsBtn:active {
    filter: brightness(0.9);
}

.small-btn-icon {
    font-size: 10px;
    color: white;
    transition: none;
}

.small-btn .small-btn-text {
    font-size: 8px;
    font-weight: 800;
    text-align: center;
    line-height: 1.1;
    white-space: nowrap;
    transition: none;
}

/* المجموعة الثانية: الأزرار الكبيرة */
.main-buttons-bar {
    position: fixed;
    top: 93px; /* أسفل الأزرار الصغيرة */
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
    gap: 15px;
    width: 100%;
    max-width: 300px;
    justify-content: center;
}

/* تصميم الأزرار الرئيسية */
.main-btn {
    border: 2px solid;
    padding: 12px 8px;
    font-size: 12px;
    border-radius: 12px;
    cursor: pointer;
    transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
    font-weight: 700;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 6px;
    min-height: 60px;
    min-width: 120px;
    box-shadow: 0 3px 10px rgba(0,0,0,0.15);
    flex: 1;
    position: relative;
    overflow: hidden;
}

/* إزالة تأثيرات الحركة والاهتزاز */
.main-btn:active,
.main-btn:focus,
.main-btn:hover {
    transform: none !important;
    line-height: inherit !important;
    font-weight: 700 !important;
    height: auto !important;
    width: auto !important;
}

/* تأثير الضغط الخفيف */
.main-btn:active {
    box-shadow: 0 0 0 3px rgba(255,255,255,0.5), inset 0 4px 6px rgba(0,0,0,0.1) !important;
    filter: brightness(0.95);
}

/* زر تنزيل PDF - أحمر */
#pdfBtn {
    background: linear-gradient(135deg, #ff6b6b 0%, #ee5a52 100%);
    color: white;
    border-color: #ee5a52;
}

#pdfBtn:hover {
    background: linear-gradient(135deg, #ee5a52 0%, #d64545 100%);
    filter: brightness(1.05);
    box-shadow: 0 5px 15px rgba(238, 90, 82, 0.4);
}

#pdfBtn:active {
    filter: brightness(0.9);
}

/* زر مشاركة واتساب - أخضر */
#whatsappBtn {
    background: linear-gradient(135deg, #25D366 0%, #1da851 100%);
    color: white;
    border-color: #1da851;
}

#whatsappBtn:hover {
    background: linear-gradient(135deg, #1da851 0%, #179244 100%);
    filter: brightness(1.05);
    box-shadow: 0 5px 15px rgba(29, 168, 81, 0.4);
}

#whatsappBtn:active {
    filter: brightness(0.9);
}

.main-btn-icon {
    font-size: 16px;
    color: white;
    transition: none;
}

.main-btn .main-btn-text {
    font-size: 11px;
    font-weight: 800;
    text-align: center;
    line-height: 1.2;
    white-space: nowrap;
    transition: none;
}

/* ========== شريط التقدم العلوي - معدل حسب المعايير الفعلية ========== */
.progress-bar-container {
    position: fixed;
    top: 153px; /* أسفل الأزرار الكبيرة */
    left: 0;
    right: 0;
    width: 100%;
    z-index: 230;
    background: linear-gradient(135deg, #ffffff 0%, #f8fdfa 100%);
    padding: 15px 20px;
    border-bottom: 2px solid #d4ebe2;
    box-shadow: 0 4px 15px rgba(4, 74, 53, 0.15);
    display: flex;
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
    background: linear-gradient(90deg, #066d4d, #0a9d