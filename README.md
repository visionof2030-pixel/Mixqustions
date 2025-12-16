<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أداة قالب امتحان اللغة الإنجليزية - ثالث متوسط</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f7fa;
            color: #333;
            line-height: 1.6;
            padding: 20px;
            max-width: 1200px;
            margin: 0 auto;
        }
        
        .header {
            background: linear-gradient(135deg, #2c6bbd 0%, #1d428a 100%);
            color: white;
            padding: 25px;
            border-radius: 12px;
            margin-bottom: 30px;
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
            text-align: center;
        }
        
        .header h1 {
            font-size: 28px;
            margin-bottom: 10px;
        }
        
        .header p {
            font-size: 16px;
            opacity: 0.9;
        }
        
        .controls {
            background-color: white;
            padding: 25px;
            border-radius: 12px;
            margin-bottom: 30px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            justify-content: center;
        }
        
        .btn {
            padding: 12px 25px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .btn-primary {
            background-color: #2c6bbd;
            color: white;
        }
        
        .btn-primary:hover {
            background-color: #1d428a;
            transform: translateY(-3px);
        }
        
        .btn-secondary {
            background-color: #28a745;
            color: white;
        }
        
        .btn-secondary:hover {
            background-color: #1e7e34;
            transform: translateY(-3px);
        }
        
        .btn-warning {
            background-color: #ffc107;
            color: #333;
        }
        
        .btn-warning:hover {
            background-color: #e0a800;
            transform: translateY(-3px);
        }
        
        .btn-danger {
            background-color: #dc3545;
            color: white;
        }
        
        .btn-danger:hover {
            background-color: #bd2130;
            transform: translateY(-3px);
        }
        
        .btn-info {
            background-color: #17a2b8;
            color: white;
        }
        
        .btn-info:hover {
            background-color: #138496;
            transform: translateY(-3px);
        }
        
        .exam-container {
            background-color: white;
            border-radius: 12px;
            padding: 30px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
            margin-bottom: 30px;
        }
        
        .exam-header {
            text-align: center;
            margin-bottom: 30px;
            border-bottom: 2px solid #2c6bbd;
            padding-bottom: 20px;
        }
        
        .ministry-logo {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 20px;
            margin-bottom: 20px;
        }
        
        .logo-placeholder {
            width: 100px;
            height: 50px;
            background-color: #f0f0f0;
            border: 1px dashed #ccc;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #777;
            font-size: 12px;
        }
        
        .exam-title {
            font-size: 22px;
            font-weight: 700;
            color: #1d428a;
            margin-bottom: 10px;
        }
        
        .exam-info {
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 15px;
            margin-bottom: 25px;
        }
        
        .info-item {
            background-color: #f8f9fa;
            padding: 12px 18px;
            border-radius: 8px;
            flex: 1;
            min-width: 200px;
        }
        
        .info-item label {
            font-weight: 600;
            color: #1d428a;
            display: block;
            margin-bottom: 5px;
        }
        
        .info-item input {
            width: 100%;
            padding: 8px 12px;
            border: 1px solid #ddd;
            border-radius: 6px;
            font-size: 16px;
        }
        
        .section {
            margin-bottom: 35px;
            border: 1px solid #e9ecef;
            border-radius: 10px;
            padding: 25px;
            background-color: #fdfdfd;
        }
        
        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid #e9ecef;
        }
        
        .section-title {
            font-size: 20px;
            font-weight: 700;
            color: #1d428a;
        }
        
        .section-controls {
            display: flex;
            gap: 10px;
        }
        
        .section-controls button {
            padding: 8px 15px;
            border-radius: 6px;
            border: none;
            background-color: #f0f0f0;
            cursor: pointer;
            font-size: 14px;
        }
        
        .question {
            background-color: white;
            border-radius: 8px;
            padding: 20px;
            margin-bottom: 20px;
            border-left: 4px solid #2c6bbd;
            box-shadow: 0 3px 8px rgba(0, 0, 0, 0.05);
        }
        
        .question-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 15px;
        }
        
        .question-text {
            font-weight: 600;
            margin-bottom: 15px;
        }
        
        .options {
            margin-left: 20px;
        }
        
        .option {
            margin-bottom: 10px;
            display: flex;
            align-items: center;
        }
        
        .option-label {
            font-weight: 600;
            margin-right: 10px;
            min-width: 30px;
        }
        
        .option-text {
            flex: 1;
            padding: 8px 12px;
            border: 1px solid #e9ecef;
            border-radius: 6px;
            background-color: #f8f9fa;
        }
        
        .option-text:focus {
            outline: none;
            border-color: #2c6bbd;
        }
        
        .pictures-section {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .picture-item {
            text-align: center;
            border: 1px solid #e9ecef;
            border-radius: 8px;
            padding: 15px;
            background-color: #f8f9fa;
        }
        
        .picture-placeholder {
            width: 100%;
            height: 100px;
            background-color: #f0f0f0;
            border: 1px dashed #ccc;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #777;
            font-size: 14px;
            margin-bottom: 10px;
            border-radius: 6px;
        }
        
        .reading-text {
            background-color: #f8f9fa;
            padding: 20px;
            border-radius: 8px;
            margin-bottom: 25px;
            line-height: 1.8;
        }
        
        .true-false {
            display: flex;
            gap: 20px;
            align-items: center;
            margin-bottom: 15px;
        }
        
        .true-false-label {
            min-width: 200px;
        }
        
        .writing-area {
            width: 100%;
            min-height: 150px;
            padding: 15px;
            border: 1px solid #e9ecef;
            border-radius: 8px;
            font-size: 16px;
            line-height: 1.6;
            margin-top: 15px;
            background-color: #f8f9fa;
        }
        
        .footer {
            text-align: center;
            margin-top: 40px;
            padding-top: 20px;
            border-top: 1px solid #e9ecef;
            color: #666;
            font-size: 14px;
        }
        
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            justify-content: center;
            align-items: center;
        }
        
        .modal-content {
            background-color: white;
            padding: 30px;
            border-radius: 12px;
            width: 90%;
            max-width: 700px;
            max-height: 80vh;
            overflow-y: auto;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
        }
        
        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            border-bottom: 2px solid #e9ecef;
            padding-bottom: 15px;
        }
        
        .modal-title {
            font-size: 22px;
            font-weight: 700;
            color: #1d428a;
        }
        
        .close-modal {
            font-size: 28px;
            cursor: pointer;
            color: #777;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #333;
        }
        
        .form-group input, .form-group textarea, .form-group select {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
        }
        
        .form-group textarea {
            min-height: 120px;
            resize: vertical;
        }
        
        .option-inputs {
            margin-top: 20px;
        }
        
        .option-input {
            display: flex;
            align-items: center;
            margin-bottom: 10px;
        }
        
        .option-input label {
            min-width: 40px;
            margin-bottom: 0;
            margin-right: 10px;
        }
        
        .option-input input {
            flex: 1;
        }
        
        .modal-buttons {
            display: flex;
            justify-content: flex-end;
            gap: 15px;
            margin-top: 30px;
        }
        
        .question-list {
            max-height: 400px;
            overflow-y: auto;
            margin-bottom: 20px;
        }
        
        .question-list-item {
            padding: 15px;
            border: 1px solid #e9ecef;
            border-radius: 8px;
            margin-bottom: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            background-color: #f8f9fa;
        }
        
        .question-list-text {
            flex: 1;
            margin-right: 15px;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
        }
        
        @media (max-width: 768px) {
            .controls {
                flex-direction: column;
            }
            
            .btn {
                width: 100%;
                justify-content: center;
            }
            
            .exam-info {
                flex-direction: column;
            }
            
            .section-controls {
                flex-direction: column;
                width: 100%;
            }
            
            .modal-content {
                width: 95%;
                padding: 20px;
            }
        }
    </style>
</head>
<body>
    <div class="header">
        <h1><i class="fas fa-file-word"></i> أداة قالب امتحان اللغة الإنجليزية</h1>
        <p>للصف الثالث متوسط - الترم الثاني - إمكانية التعديل والخلط والتصدير</p>
    </div>
    
    <div class="controls">
        <button class="btn btn-primary" id="shuffleBtn">
            <i class="fas fa-random"></i> خلط الأسئلة
        </button>
        <button class="btn btn-secondary" id="editBtn">
            <i class="fas fa-edit"></i> تعديل/إضافة أسئلة
        </button>
        <button class="btn btn-warning" id="exportWordBtn">
            <i class="fas fa-file-word"></i> تصدير كملف Word
        </button>
        <button class="btn btn-danger" id="exportPdfBtn">
            <i class="fas fa-file-pdf"></i> تصدير كملف PDF
        </button>
        <button class="btn btn-info" id="printBtn">
            <i class="fas fa-print"></i> طباعة النموذج
        </button>
    </div>
    
    <div class="exam-container" id="examContainer">
        <div class="exam-header">
            <div class="ministry-logo">
                <div class="logo-placeholder">شعار الوزارة</div>
                <div>
                    <div>Kingdom of Saudi Arabia Ministry of Education</div>
                    <div>Education Directorate in Makkah</div>
                    <div>Saeed Ibn Alas Intermediate School</div>
                </div>
            </div>
            
            <div class="exam-title">Super Goal 3 - English Language</div>
            <div>3<sup>rd</sup> Intermediate Grade - 2nd Term rescheduled Exam 1447-2026</div>
            <div>Time: 2 hours</div>
        </div>
        
        <div class="exam-info">
            <div class="info-item">
                <label for="studentName">اسم الطالب:</label>
                <input type="text" id="studentName" value="">
            </div>
            <div class="info-item">
                <label for="seatNumber">رقم الجلوس:</label>
                <input type="text" id="seatNumber" value="">
            </div>
            <div class="info-item">
                <label for="correctorName">المصحح:</label>
                <input type="text" id="correctorName" value="">
            </div>
            <div class="info-item">
                <label for="reviewerName">المراجع:</label>
                <input type="text" id="reviewerName" value="">
            </div>
        </div>
        
        <!-- Grammar Section -->
        <div class="section" id="grammarSection">
            <div class="section-header">
                <h2 class="section-title">Grammar</h2>
                <div class="section-controls">
                    <button class="shuffle-section" data-section="grammar"><i class="fas fa-random"></i> خلط</button>
                </div>
            </div>
            
            <div class="question" id="grammar1">
                <div class="question-header">
                    <div class="question-number">1</div>
                </div>
                <div class="question-text">he ______ plays football on weekends.</div>
                <div class="options">
                    <div class="option">
                        <div class="option-label">a.</div>
                        <input type="text" class="option-text" value="does">
                    </div>
                    <div class="option">
                        <div class="option-label">b.</div>
                        <input type="text" class="option-text" value="always">
                    </div>
                    <div class="option">
                        <div class="option-label">c.</div>
                        <input type="text" class="option-text" value="has">
                    </div>
                </div>
            </div>
            
            <div class="question" id="grammar2">
                <div class="question-header">
                    <div class="question-number">2</div>
                </div>
                <div class="question-text">How often ______ drink coffee?</div>
                <div class="options">
                    <div class="option">
                        <div class="option-label">a.</div>
                        <input type="text" class="option-text" value="does">
                    </div>
                    <div class="option">
                        <div class="option-label">b.</div>
                        <input type="text" class="option-text" value="did">
                    </div>
                    <div class="option">
                        <div class="option-label">c.</div>
                        <input type="text" class="option-text" value="do">
                    </div>
                </div>
            </div>
            
            <!-- More grammar questions would be here in a complete version -->
        </div>
        
        <!-- Orthography Section -->
        <div class="section" id="orthographySection">
            <div class="section-header">
                <h2 class="section-title">Orthography</h2>
                <div class="section-controls">
                    <button class="shuffle-section" data-section="orthography"><i class="fas fa-random"></i> خلط</button>
                </div>
            </div>
            
            <div class="question" id="orthography1">
                <div class="question-header">
                    <div class="question-number">10</div>
                </div>
                <div class="question-text">which letter completes the word? " ______ilk ".</div>
                <div class="options">
                    <div class="option">
                        <div class="option-label">a.</div>
                        <input type="text" class="option-text" value="N">
                    </div>
                    <div class="option">
                        <div class="option-label">b.</div>
                        <input type="text" class="option-text" value="M">
                    </div>
                    <div class="option">
                        <div class="option-label">c.</div>
                        <input type="text" class="option-text" value="T">
                    </div>
                </div>
            </div>
            
            <!-- More orthography questions would be here in a complete version -->
        </div>
        
        <!-- Vocabulary Section -->
        <div class="section" id="vocabularySection">
            <div class="section-header">
                <h2 class="section-title">Vocabulary</h2>
                <div class="section-controls">
                    <button class="shuffle-section" data-section="vocabulary"><i class="fas fa-random"></i> خلط</button>
                </div>
            </div>
            
            <div class="pictures-section">
                <div class="picture-item">
                    <div class="picture-placeholder">صورة 1</div>
                    <div>الكلمة: <input type="text" class="picture-word" value="Lamb"></div>
                </div>
                <div class="picture-item">
                    <div class="picture-placeholder">صورة 2</div>
                    <div>الكلمة: <input type="text" class="picture-word" value="Shrimp"></div>
                </div>
                <!-- More picture items would be here in a complete version -->
            </div>
        </div>
        
        <!-- Reading Section -->
        <div class="section" id="readingSection">
            <div class="section-header">
                <h2 class="section-title">Reading</h2>
                <div class="section-controls">
                    <button class="shuffle-section" data-section="reading"><i class="fas fa-random"></i> خلط</button>
                </div>
            </div>
            
            <div class="reading-text">
                <p>King Salman bin Abdulaziz was born in Riyadh. He studied religion, science, and the Holy Qur'an at the Princes' School. He became King of Saudi Arabia in 2015. He helped Riyadh grow from a small town into a major modern city. He also supported humanitarian and cultural projects inside and outside the Kingdom.</p>
            </div>
            
            <div class="question" id="reading1">
                <div class="question-text">1. King Salman was born in Jeddah.</div>
                <div class="true-false">
                    <div class="true-false-label"></div>
                    <div>
                        <input type="radio" name="reading1" id="reading1-t" value="T">
                        <label for="reading1-t">T</label>
                        <input type="radio" name="reading1" id="reading1-f" value="F">
                        <label for="reading1-f">F</label>
                    </div>
                </div>
            </div>
            
            <!-- More reading questions would be here in a complete version -->
        </div>
        
        <!-- Writing Section -->
        <div class="section" id="writingSection">
            <div class="section-header">
                <h2 class="section-title">Writing</h2>
            </div>
            
            <div class="question-text">Write a coherent paragraph of 3-5 sentences using 8 words from the following list: (enjoy -- fitness -- work out -- spend time -- lifestyle -- herbal tea -- puzzle -- fan)</div>
            
            <textarea class="writing-area" id="writingArea" placeholder="اكتب فقرتك هنا..."></textarea>
        </div>
        
        <div class="footer">
            <p>My best wishes</p>
            <p>Teacher Fahad Alkhaldi</p>
        </div>
    </div>
    
    <!-- Edit/Add Questions Modal -->
    <div class="modal" id="editModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title">تعديل/إضافة أسئلة</h2>
                <span class="close-modal" id="closeEditModal">&times;</span>
            </div>
            
            <div class="form-group">
                <label for="sectionSelect">القسم:</label>
                <select id="sectionSelect">
                    <option value="grammar">Grammar</option>
                    <option value="orthography">Orthography</option>
                    <option value="vocabulary">Vocabulary</option>
                    <option value="reading">Reading</option>
                    <option value="writing">Writing</option>
                </select>
            </div>
            
            <div class="form-group">
                <label for="questionText">نص السؤال:</label>
                <textarea id="questionText" placeholder="أدخل نص السؤال..."></textarea>
            </div>
            
            <div class="form-group">
                <label>نوع السؤال:</label>
                <div>
                    <input type="radio" name="questionType" id="typeMultiple" value="multiple" checked>
                    <label for="typeMultiple">اختيار من متعدد</label>
                    <input type="radio" name="questionType" id="typeTrueFalse" value="truefalse">
                    <label for="typeTrueFalse">صح/خطأ</label>
                    <input type="radio" name="questionType" id="typeOpen" value="open">
                    <label for="typeOpen">سؤال مفتوح</label>
                </div>
            </div>
            
            <div class="option-inputs" id="optionInputs">
                <div class="option-input">
                    <label>أ.</label>
                    <input type="text" id="optionA" placeholder="الخيار الأول">
                </div>
                <div class="option-input">
                    <label>ب.</label>
                    <input type="text" id="optionB" placeholder="الخيار الثاني">
                </div>
                <div class="option-input">
                    <label>ج.</label>
                    <input type="text" id="optionC" placeholder="الخيار الثالث">
                </div>
            </div>
            
            <div class="modal-buttons">
                <button class="btn btn-secondary" id="addQuestionBtn">إضافة سؤال جديد</button>
                <button class="btn btn-primary" id="saveQuestionBtn">حفظ التعديلات</button>
                <button class="btn btn-warning" id="cancelEditBtn">إلغاء</button>
            </div>
            
            <div id="questionListContainer">
                <h3 style="margin-top: 30px; margin-bottom: 15px;">الأسئلة الحالية:</h3>
                <div class="question-list" id="questionList">
                    <!-- Questions will be listed here -->
                </div>
            </div>
        </div>
    </div>

    <!-- Export Modal -->
    <div class="modal" id="exportModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title" id="exportModalTitle">تصدير الامتحان</h2>
                <span class="close-modal" id="closeExportModal">&times;</span>
            </div>
            
            <div id="exportMessage">
                <p>يتم تحضير الملف للتصدير، الرجاء الانتظار...</p>
                <div style="text-align: center; margin: 30px 0;">
                    <i class="fas fa-spinner fa-spin fa-3x" style="color: #2c6bbd;"></i>
                </div>
            </div>
            
            <div class="modal-buttons" id="exportModalButtons" style="display: none;">
                <button class="btn btn-primary" id="downloadExportBtn">تحميل الملف</button>
                <button class="btn btn-warning" id="closeExportBtn">إغلاق</button>
            </div>
        </div>
    </div>

    <script>
        // العناصر الرئيسية
        const shuffleBtn = document.getElementById('shuffleBtn');
        const editBtn = document.getElementById('editBtn');
        const exportWordBtn = document.getElementById('exportWordBtn');
        const exportPdfBtn = document.getElementById('exportPdfBtn');
        const printBtn = document.getElementById('printBtn');
        const editModal = document.getElementById('editModal');
        const exportModal = document.getElementById('exportModal');
        const closeEditModal = document.getElementById('closeEditModal');
        const closeExportModal = document.getElementById('closeExportModal');
        const sectionSelect = document.getElementById('sectionSelect');
        const questionTypeRadios = document.querySelectorAll('input[name="questionType"]');
        const optionInputs = document.getElementById('optionInputs');
        const addQuestionBtn = document.getElementById('addQuestionBtn');
        const saveQuestionBtn = document.getElementById('saveQuestionBtn');
        const cancelEditBtn = document.getElementById('cancelEditBtn');
        const questionList = document.getElementById('questionList');
        const exportModalTitle = document.getElementById('exportModalTitle');
        const exportMessage = document.getElementById('exportMessage');
        const exportModalButtons = document.getElementById('exportModalButtons');
        const downloadExportBtn = document.getElementById('downloadExportBtn');
        const closeExportBtn = document.getElementById('closeExportBtn');
        
        // استدعاء الدوال الأساسية عند تحميل الصفحة
        document.addEventListener('DOMContentLoaded', function() {
            updateQuestionList();
            
            // إضافة مستمعي الأحداث لنوع السؤال
            questionTypeRadios.forEach(radio => {
                radio.addEventListener('change', function() {
                    if (this.value === 'multiple') {
                        optionInputs.style.display = 'block';
                    } else if (this.value === 'truefalse') {
                        optionInputs.style.display = 'none';
                    } else {
                        optionInputs.style.display = 'none';
                    }
                });
            });
        });
        
        // وظيفة خلط الأسئلة
        shuffleBtn.addEventListener('click', function() {
            // خلط أسئلة القواعد
            const grammarSection = document.getElementById('grammarSection');
            const grammarQuestions = Array.from(grammarSection.querySelectorAll('.question'));
            
            // خلط الأسئلة
            shuffleArray(grammarQuestions);
            
            // إعادة إضافة الأسئلة بالترتيب الجديد
            grammarQuestions.forEach((question, index) => {
                grammarSection.appendChild(question);
                question.querySelector('.question-number').textContent = index + 1;
            });
            
            // خلط أسئلة التهجئة
            const orthographySection = document.getElementById('orthographySection');
            const orthographyQuestions = Array.from(orthographySection.querySelectorAll('.question'));
            
            shuffleArray(orthographyQuestions);
            orthographyQuestions.forEach((question, index) => {
                orthographySection.appendChild(question);
                question.querySelector('.question-number').textContent = 10 + index;
            });
            
            // خلط عناصر المفردات (الصور)
            const vocabularySection = document.getElementById('vocabularySection');
            const pictureItems = Array.from(vocabularySection.querySelectorAll('.picture-item'));
            
            shuffleArray(pictureItems);
            pictureItems.forEach((item, index) => {
                vocabularySection.querySelector('.pictures-section').appendChild(item);
            });
            
            // خلط أسئلة القراءة
            const readingSection = document.getElementById('readingSection');
            const readingQuestions = Array.from(readingSection.querySelectorAll('.question'));
            
            shuffleArray(readingQuestions);
            readingQuestions.forEach((question, index) => {
                readingSection.appendChild(question);
            });
            
            // عرض رسالة نجاح
            alert("تم خلط الأسئلة بنجاح!");
        });
        
        // وظيفة خلط مصفوفة
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }
        
        // فتح نافذة تعديل الأسئلة
        editBtn.addEventListener('click', function() {
            editModal.style.display = 'flex';
        });
        
        // إغلاق نافذة تعديل الأسئلة
        closeEditModal.addEventListener('click', function() {
            editModal.style.display = 'none';
            resetEditForm();
        });
        
        // إغلاق نافذة التصدير
        closeExportModal.addEventListener('click', function() {
            exportModal.style.display = 'none';
        });
        
        // إغلاق نافذة التعديل عند النقر خارجها
        window.addEventListener('click', function(event) {
            if (event.target === editModal) {
                editModal.style.display = 'none';
                resetEditForm();
            }
            if (event.target === exportModal) {
                exportModal.style.display = 'none';
            }
        });
        
        // إلغاء التعديل
        cancelEditBtn.addEventListener('click', function() {
            editModal.style.display = 'none';
            resetEditForm();
        });
        
        // إعادة تعيين نموذج التعديل
        function resetEditForm() {
            document.getElementById('questionText').value = '';
            document.getElementById('optionA').value = '';
            document.getElementById('optionB').value = '';
            document.getElementById('optionC').value = '';
            document.getElementById('typeMultiple').checked = true;
            optionInputs.style.display = 'block';
        }
        
        // تحديث قائمة الأسئلة
        function updateQuestionList() {
            questionList.innerHTML = '';
            
            // جمع جميع الأسئلة
            const allQuestions = document.querySelectorAll('.question');
            
            allQuestions.forEach((question, index) => {
                const questionText = question.querySelector('.question-text').textContent;
                const listItem = document.createElement('div');
                listItem.className = 'question-list-item';
                listItem.innerHTML = `
                    <div class="question-list-text">${index + 1}. ${questionText.substring(0, 50)}${questionText.length > 50 ? '...' : ''}</div>
                    <div>
                        <button class="edit-question-btn" data-id="${index}"><i class="fas fa-edit"></i></button>
                        <button class="delete-question-btn" data-id="${index}"><i class="fas fa-trash"></i></button>
                    </div>
                `;
                questionList.appendChild(listItem);
            });
            
            // إضافة مستمعي الأحداث لأزرار التعديل والحذف
            document.querySelectorAll('.edit-question-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const questionId = this.getAttribute('data-id');
                    editQuestion(questionId);
                });
            });
            
            document.querySelectorAll('.delete-question-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const questionId = this.getAttribute('data-id');
                    if (confirm("هل أنت متأكد من حذف هذا السؤال؟")) {
                        deleteQuestion(questionId);
                    }
                });
            });
        }
        
        // تعديل سؤال موجود
        function editQuestion(questionId) {
            const allQuestions = document.querySelectorAll('.question');
            const question = allQuestions[questionId];
            
            if (question) {
                const questionText = question.querySelector('.question-text').textContent;
                const options = question.querySelectorAll('.option-text');
                
                document.getElementById('questionText').value = questionText;
                
                if (options.length > 0) {
                    document.getElementById('typeMultiple').checked = true;
                    optionInputs.style.display = 'block';
                    document.getElementById('optionA').value = options[0] ? options[0].value : '';
                    document.getElementById('optionB').value = options[1] ? options[1].value : '';
                    document.getElementById('optionC').value = options[2] ? options[2].value : '';
                } else if (question.querySelector('input[type="radio"]')) {
                    document.getElementById('typeTrueFalse').checked = true;
                    optionInputs.style.display = 'none';
                } else {
                    document.getElementById('typeOpen').checked = true;
                    optionInputs.style.display = 'none';
                }
                
                // تحديث زر الحفظ ليعمل على السؤال الحالي
                saveQuestionBtn.onclick = function() {
                    saveQuestionEdit(questionId);
                };
            }
        }
        
        // حفظ تعديل السؤال
        function saveQuestionEdit(questionId) {
            const allQuestions = document.querySelectorAll('.question');
            const question = allQuestions[questionId];
            
            if (question) {
                const questionText = document.getElementById('questionText').value;
                const questionType = document.querySelector('input[name="questionType"]:checked').value;
                
                // تحديث نص السؤال
                question.querySelector('.question-text').textContent = questionText;
                
                // تحديث الخيارات بناءً على النوع
                if (questionType === 'multiple') {
                    const optionA = document.getElementById('optionA').value;
                    const optionB = document.getElementById('optionB').value;
                    const optionC = document.getElementById('optionC').value;
                    
                    const optionInputs = question.querySelectorAll('.option-text');
                    if (optionInputs.length > 0) {
                        optionInputs[0].value = optionA;
                        optionInputs[1].value = optionB;
                        optionInputs[2].value = optionC;
                    }
                }
                
                // إغلاق النافذة وإعادة تعيين النموذج
                editModal.style.display = 'none';
                resetEditForm();
                updateQuestionList();
                
                alert("تم تحديث السؤال بنجاح!");
            }
        }
        
        // حذف سؤال
        // حذف سؤال
                function deleteQuestion(questionId) {
                    const allQuestions = document.querySelectorAll('.question');
                    const question = allQuestions[questionId];
                    
                    if (question) {
                        question.remove();
                        updateQuestionList();
                        alert("تم حذف السؤال بنجاح!");
                    }
                }
                
                // إضافة سؤال جديد
                addQuestionBtn.addEventListener('click', function() {
                    const section = sectionSelect.value;
                    const questionText = document.getElementById('questionText').value;
                    const questionType = document.querySelector('input[name="questionType"]:checked').value;
                    
                    if (!questionText.trim()) {
                        alert("الرجاء إدخال نص السؤال");
                        return;
                    }
                    
                    // إنشاء سؤال جديد
                    const newQuestion = document.createElement('div');
                    newQuestion.className = 'question';
                    
                    if (questionType === 'multiple') {
                        const optionA = document.getElementById('optionA').value;
                        const optionB = document.getElementById('optionB').value;
                        const optionC = document.getElementById('optionC').value;
                        
                        newQuestion.innerHTML = `
                            <div class="question-header">
                                <div class="question-number">${getNextQuestionNumber(section)}</div>
                            </div>
                            <div class="question-text">${questionText}</div>
                            <div class="options">
                                <div class="option">
                                    <div class="option-label">a.</div>
                                    <input type="text" class="option-text" value="${optionA}">
                                </div>
                                <div class="option">
                                    <div class="option-label">b.</div>
                                    <input type="text" class="option-text" value="${optionB}">
                                </div>
                                <div class="option">
                                    <div class="option-label">c.</div>
                                    <input type="text" class="option-text" value="${optionC}">
                                </div>
                            </div>
                        `;
                    } else if (questionType === 'truefalse') {
                        newQuestion.innerHTML = `
                            <div class="question-header">
                                <div class="question-number">${getNextQuestionNumber(section)}</div>
                            </div>
                            <div class="question-text">${questionText}</div>
                            <div class="true-false">
                                <div class="true-false-label"></div>
                                <div>
                                    <input type="radio" name="newQuestion" id="newQuestion-t" value="T">
                                    <label for="newQuestion-t">T</label>
                                    <input type="radio" name="newQuestion" id="newQuestion-f" value="F">
                                    <label for="newQuestion-f">F</label>
                                </div>
                            </div>
                        `;
                    } else {
                        newQuestion.innerHTML = `
                            <div class="question-header">
                                <div class="question-number">${getNextQuestionNumber(section)}</div>
                            </div>
                            <div class="question-text">${questionText}</div>
                            <div class="options">
                                <div class="option">
                                    <textarea class="option-text" placeholder="الإجابة..." style="height: 80px;"></textarea>
                                </div>
                            </div>
                        `;
                    }
                    
                    // إضافة السؤال إلى القسم المناسب
                    const targetSection = document.getElementById(`${section}Section`);
                    if (targetSection) {
                        targetSection.appendChild(newQuestion);
                    }
                    
                    // إعادة تعيين النموذج وتحديث القائمة
                    resetEditForm();
                    updateQuestionList();
                    
                    alert("تم إضافة السؤال بنجاح!");
                });
                
                // الحصول على الرقم التالي للسؤال
                function getNextQuestionNumber(section) {
                    const sectionElement = document.getElementById(`${section}Section`);
                    if (!sectionElement) return 1;
                    
                    const questions = sectionElement.querySelectorAll('.question');
                    return questions.length + 1;
                }
                
                // تصدير كملف Word
                exportWordBtn.addEventListener('click', function() {
                    exportModalTitle.textContent = "تصدير كملف Word";
                    exportModal.style.display = 'flex';
                    
                    // محاكاة عملية التحضير للتصدير
                    setTimeout(function() {
                        exportMessage.innerHTML = `
                            <p><i class="fas fa-check-circle" style="color: #28a745; font-size: 24px;"></i></p>
                            <p style="font-size: 18px; margin: 15px 0;">تم تحضير ملف Word بنجاح!</p>
                            <p>الملف جاهز للتحميل. سيتم حفظه باسم: "امتحان_الإنجليزية_معدل.docx"</p>
                        `;
                        exportModalButtons.style.display = 'flex';
                    }, 1500);
                    
                    // إعداد زر التحميل
                    downloadExportBtn.onclick = function() {
                        // هنا ستتم عملية التصدير الفعلية لملف Word
                        // في الواقع، يمكن استخدام مكتبة مثل docx.js لإنشاء ملف Word
                        alert("في التطبيق الكامل، سيتم هنا إنشاء ملف Word فعليًا للتحميل.");
                        exportModal.style.display = 'none';
                    };
                });
                
                // تصدير كملف PDF
                exportPdfBtn.addEventListener('click', function() {
                    exportModalTitle.textContent = "تصدير كملف PDF";
                    exportModal.style.display = 'flex';
                    
                    // محاكاة عملية التحضير للتصدير
                    setTimeout(function() {
                        exportMessage.innerHTML = `
                            <p><i class="fas fa-check-circle" style="color: #28a745; font-size: 24px;"></i></p>
                            <p style="font-size: 18px; margin: 15px 0;">تم تحضير ملف PDF بنجاح!</p>
                            <p>الملف جاهز للتحميل. سيتم حفظه باسم: "امتحان_الإنجليزية_معدل.pdf"</p>
                        `;
                        exportModalButtons.style.display = 'flex';
                    }, 1500);
                    
                    // إعداد زر التحميل
                    downloadExportBtn.onclick = function() {
                        // هنا ستتم عملية التصدير الفعلية لملف PDF
                        // في الواقع، يمكن استخدام مكتبة مثل jsPDF لإنشاء ملف PDF
                        alert("في التطبيق الكامل، سيتم هنا إنشاء ملف PDF فعليًا للتحميل.");
                        exportModal.style.display = 'none';
                    };
                });
                
                // زر الطباعة
                printBtn.addEventListener('click', function() {
                    // حفظ القيم الحالية للمدخلات في النص
                    const studentName = document.getElementById('studentName').value;
                    const seatNumber = document.getElementById('seatNumber').value;
                    const correctorName = document.getElementById('correctorName').value;
                    const reviewerName = document.getElementById('reviewerName').value;
                    
                    // استبدال المدخلات بالنصوص للطباعة
                    document.getElementById('studentName').style.display = 'none';
                    document.getElementById('seatNumber').style.display = 'none';
                    document.getElementById('correctorName').style.display = 'none';
                    document.getElementById('reviewerName').style.display = 'none';
                    
                    // إنشاء عناصر لعرض النصوص
                    const nameDisplay = document.createElement('div');
                    nameDisplay.textContent = studentName || '_______________';
                    nameDisplay.style.padding = '8px 0';
                    document.getElementById('studentName').parentNode.appendChild(nameDisplay);
                    
                    const seatDisplay = document.createElement('div');
                    seatDisplay.textContent = seatNumber || '_______________';
                    seatDisplay.style.padding = '8px 0';
                    document.getElementById('seatNumber').parentNode.appendChild(seatDisplay);
                    
                    const correctorDisplay = document.createElement('div');
                    correctorDisplay.textContent = correctorName || '_______________';
                    correctorDisplay.style.padding = '8px 0';
                    document.getElementById('correctorName').parentNode.appendChild(correctorDisplay);
                    
                    const reviewerDisplay = document.createElement('div');
                    reviewerDisplay.textContent = reviewerName || '_______________';
                    reviewerDisplay.style.padding = '8px 0';
                    document.getElementById('reviewerName').parentNode.appendChild(reviewerDisplay);
                    
                    // إخفاء أزرار التحكم
                    document.querySelector('.controls').style.display = 'none';
                    
                    // إخفاء أزرار التحكم في الأقسام
                    document.querySelectorAll('.section-controls').forEach(btn => {
                        btn.style.display = 'none';
                    });
                    
                    // طباعة الصفحة
                    window.print();
                    
                    // إعادة كل شيء كما كان
                    setTimeout(function() {
                        document.getElementById('studentName').style.display = 'block';
                        document.getElementById('seatNumber').style.display = 'block';
                        document.getElementById('correctorName').style.display = 'block';
                        document.getElementById('reviewerName').style.display = 'block';
                        
                        // إزالة عناصر العرض
                        nameDisplay.remove();
                        seatDisplay.remove();
                        correctorDisplay.remove();
                        reviewerDisplay.remove();
                        
                        // إظهار أزرار التحكم
                        document.querySelector('.controls').style.display = 'block';
                        document.querySelectorAll('.section-controls').forEach(btn => {
                            btn.style.display = 'flex';
                        });
                    }, 500);
                });
                
                // خلط أسئلة قسم معين
                document.querySelectorAll('.shuffle-section').forEach(btn => {
                    btn.addEventListener('click', function() {
                        const section = this.getAttribute('data-section');
                        const sectionElement = document.getElementById(`${section}Section`);
                        
                        if (section === 'vocabulary') {
                            // خلط عناصر المفردات (الصور)
                            const pictureItems = Array.from(sectionElement.querySelectorAll('.picture-item'));
                            shuffleArray(pictureItems);
                            pictureItems.forEach(item => {
                                sectionElement.querySelector('.pictures-section').appendChild(item);
                            });
                        } else {
                            // خلط الأسئلة في الأقسام الأخرى
                            const questions = Array.from(sectionElement.querySelectorAll('.question'));
                            shuffleArray(questions);
                            questions.forEach((question, index) => {
                                sectionElement.appendChild(question);
                                const questionNumber = question.querySelector('.question-number');
                                if (questionNumber) {
                                    if (section === 'grammar') {
                                        questionNumber.textContent = index + 1;
                                    } else if (section === 'orthography') {
                                        questionNumber.textContent = 10 + index;
                                    }
                                }
                            });
                        }
                        
                        alert(`تم خلط أسئلة قسم ${section} بنجاح!`);
                    });
                });
                
                // إغلاق نافذة التصدير
                closeExportBtn.addEventListener('click', function() {
                    exportModal.style.display = 'none';
                    exportMessage.innerHTML = `
                        <p>يتم تحضير الملف للتصدير، الرجاء الانتظار...</p>
                        <div style="text-align: center; margin: 30px 0;">
                            <i class="fas fa-spinner fa-spin fa-3x" style="color: #2c6bbd;"></i>
                        </div>
                    `;
                    exportModalButtons.style.display = 'none';
                });
                
                // استجابة عند تغيير قسم التحرير
                sectionSelect.addEventListener('change', function() {
                    // إعادة تعيين النموذج عند تغيير القسم
                    resetEditForm();
                });
            </script>
        </body>
        </html>
