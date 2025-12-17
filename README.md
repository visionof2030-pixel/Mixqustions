<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أداة تبديل فقرات Word باستخدام Python</title>
    <script src="https://cdn.jsdelivr.net/pyodide/v0.25.0/full/pyodide.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1a2a6c, #b21f1f, #fdbb2d);
            color: #333;
            line-height: 1.6;
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            background-color: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
            overflow: hidden;
            padding: 30px;
        }

        header {
            text-align: center;
            margin-bottom: 30px;
            padding-bottom: 20px;
            border-bottom: 3px solid #1a2a6c;
        }

        h1 {
            color: #1a2a6c;
            font-size: 2.5rem;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
        }

        h1 i {
            color: #fdbb2d;
        }

        .subtitle {
            color: #666;
            font-size: 1.1rem;
        }

        .app-description {
            background: linear-gradient(to right, #e3f2fd, #f3e5f5);
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 30px;
            border-right: 5px solid #1a2a6c;
        }

        .app-description h2 {
            color: #1a2a6c;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .steps {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .step {
            background: white;
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            border-top: 4px solid #b21f1f;
            transition: transform 0.3s;
        }

        .step:hover {
            transform: translateY(-5px);
        }

        .step-number {
            display: inline-block;
            background: #1a2a6c;
            color: white;
            width: 35px;
            height: 35px;
            border-radius: 50%;
            text-align: center;
            line-height: 35px;
            margin-bottom: 15px;
            font-weight: bold;
        }

        .step h3 {
            color: #1a2a6c;
            margin-bottom: 10px;
        }

        .editor-section {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-bottom: 30px;
        }

        @media (max-width: 768px) {
            .editor-section {
                grid-template-columns: 1fr;
            }
        }

        .input-section, .output-section {
            background: white;
            padding: 25px;
            border-radius: 15px;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.08);
        }

        .section-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid #f0f0f0;
        }

        .section-header h2 {
            color: #1a2a6c;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .button-small {
            background: #1a2a6c;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
            transition: background 0.3s;
        }

        .button-small:hover {
            background: #0d1a4a;
        }

        textarea {
            width: 100%;
            height: 300px;
            padding: 15px;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            font-family: 'Courier New', monospace;
            font-size: 14px;
            resize: vertical;
            direction: ltr;
            margin-bottom: 15px;
        }

        textarea:focus {
            outline: none;
            border-color: #1a2a6c;
        }

        .actions {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin: 30px 0;
        }

        .btn {
            padding: 15px 30px;
            border: none;
            border-radius: 50px;
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 10px;
            transition: all 0.3s;
        }

        .btn-primary {
            background: linear-gradient(to right, #1a2a6c, #b21f1f);
            color: white;
            box-shadow: 0 5px 15px rgba(26, 42, 108, 0.3);
        }

        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(26, 42, 108, 0.4);
        }

        .btn-secondary {
            background: #f8f9fa;
            color: #1a2a6c;
            border: 2px solid #1a2a6c;
        }

        .btn-secondary:hover {
            background: #e9ecef;
        }

        .python-code-section {
            background: #282c34;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 30px;
            color: white;
        }

        .python-code-section h2 {
            color: #61dafb;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .code-container {
            background: #1e1e1e;
            padding: 20px;
            border-radius: 10px;
            overflow-x: auto;
            font-family: 'Courier New', monospace;
            font-size: 14px;
            line-height: 1.5;
        }

        .status {
            background: #e8f4fd;
            padding: 20px;
            border-radius: 15px;
            margin-top: 30px;
            text-align: center;
            display: none;
        }

        .status.success {
            background: #d4edda;
            color: #155724;
            border-left: 5px solid #28a745;
        }

        .status.error {
            background: #f8d7da;
            color: #721c24;
            border-left: 5px solid #dc3545;
        }

        .status.loading {
            background: #fff3cd;
            color: #856404;
            border-left: 5px solid #ffc107;
        }

        footer {
            text-align: center;
            margin-top: 40px;
            padding-top: 20px;
            border-top: 1px solid #e0e0e0;
            color: #666;
        }

        .loading-spinner {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid rgba(255,255,255,.3);
            border-radius: 50%;
            border-top-color: white;
            animation: spin 1s ease-in-out infinite;
            margin-right: 10px;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        .example-text {
            font-size: 12px;
            color: #666;
            margin-top: 10px;
            padding: 10px;
            background: #f9f9f9;
            border-radius: 5px;
            border-right: 3px solid #1a2a6c;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1><i class="fas fa-exchange-alt"></i> أداة تبديل فقرات أسئلة Word</h1>
            <p class="subtitle">استخدم Python مباشرة في متصفحك لتبديل ترتيب فقرات الأسئلة في ملف Word</p>
        </header>

        <div class="app-description">
            <h2><i class="fas fa-info-circle"></i> حول الأداة</h2>
            <p>تستخدم هذه الأداة مكتبة Pyodide لتشغيل Python مباشرة في متصفحك. تقوم بتحليل محتوى قسم Grammar في اختبار Word وتبديل ترتيب السؤالين الأول والثاني مع الحفاظ على التنسيق الأصلي.</p>
        </div>

        <div class="steps">
            <div class="step">
                <div class="step-number">1</div>
                <h3>الصق المحتوى</h3>
                <p>افتح ملف Word وانسخ محتوى قسم Grammar كاملاً والصقه في مربع الإدخال الأيسر.</p>
            </div>
            <div class="step">
                <div class="step-number">2</div>
                <h3>تشغيل Python</h3>
                <p>اضغط على زر "تشغيل Python لتبديل الفقرات" لتنفيذ الكود البرمجي تلقائياً.</p>
            </div>
            <div class="step">
                <div class="step-number">3</div>
                <h3>انسخ النتيجة</h3>
                <p>انسخ المحتوى المعدل من مربع الإخراج الأيمن والصقه في ملف Word مكان المحتوى الأصلي.</p>
            </div>
        </div>

        <div class="editor-section">
            <div class="input-section">
                <div class="section-header">
                    <h2><i class="fas fa-keyboard"></i> المحتوى الأصلي</h2>
                    <button class="button-small" onclick="loadExample()">
                        <i class="fas fa-file-alt"></i> تحميل مثال
                    </button>
                </div>
                <textarea id="inputText" placeholder="الصق محتوى قسم Grammar من ملف Word هنا..."></textarea>
                <div class="example-text">
                    <strong>تنسيق مثال:</strong><br>
                    ***1. he _______ plays football on weekends.***<br>
                    ***a*** ***does*** ***b*** ***always*** ***c*** ***has***<br>
                    ***2. How often _______ drink coffee?***<br>
                    ***a*** ***does*** ***b*** ***did*** ***c*** ***do***
                </div>
            </div>

            <div class="output-section">
                <div class="section-header">
                    <h2><i class="fas fa-file-export"></i> المحتوى بعد التبديل</h2>
                    <button class="button-small" onclick="copyOutput()">
                        <i class="fas fa-copy"></i> نسخ
                    </button>
                </div>
                <textarea id="outputText" readonly placeholder="ستظهر هنا النتيجة بعد تبديل الفقرات..."></textarea>
                <div class="example-text">
                    <strong>بعد التبديل:</strong><br>
                    ***2. How often _______ drink coffee?***<br>
                    ***a*** ***does*** ***b*** ***did*** ***c*** ***do***<br>
                    ***1. he _______ plays football on weekends.***<br>
                    ***a*** ***does*** ***b*** ***always*** ***c*** ***has***
                </div>
            </div>
        </div>

        <div class="actions">
            <button class="btn btn-primary" id="runPythonBtn" onclick="runPythonCode()">
                <i class="fab fa-python"></i> تشغيل Python لتبديل الفقرات
            </button>
            <button class="btn btn-secondary" onclick="clearAll()">
                <i class="fas fa-broom"></i> مسح الكل
            </button>
        </div>

        <div class="python-code-section">
            <h2><i class="fas fa-code"></i> كود Python الذي سيتم تنفيذه</h2>
            <div class="code-container">
                <pre id="pythonCodeDisplay">def swap_questions(content):
    lines = content.split('\n')
    q1_start = -1
    q1_end = -1
    q2_start = -1
    q2_end = -1
    
    # البحث عن بداية ونهاية السؤالين
    for i, line in enumerate(lines):
        if line.strip().startswith('***1.'):
            q1_start = i
        elif line.strip().startswith('***2.'):
            q2_start = i
            
        # تحديد نهاية السؤال 1 (قبل بداية السؤال 2)
        if q1_start != -1 and q2_start != -1 and q1_end == -1:
            q1_end = q2_start - 1
            
        # تحديد نهاية السؤال 2 (السطر قبل السؤال 3 أو نهاية المحتوى)
        if q2_start != -1 and q2_end == -1:
            # البحث عن السؤال 3 أو نهاية المحتوى
            for j in range(i+1, len(lines)):
                if lines[j].strip().startswith('***3.'):
                    q2_end = j - 1
                    break
            if q2_end == -1:
                q2_end = len(lines) - 1
    
    # إذا وجدنا كلا السؤالين، نقوم بتبديلهما
    if q1_start != -1 and q2_start != -1:
        # استخراج محتوى السؤالين
        question1 = lines[q1_start:q1_end+1]
        question2 = lines[q2_start:q2_end+1]
        
        # بناء المحتوى الجديد مع تبديل الترتيب
        new_lines = []
        new_lines.extend(lines[:q1_start])  # ما قبل السؤال 1
        new_lines.extend(question2)         # السؤال 2 أولاً
        new_lines.extend(question1)         # ثم السؤال 1
        new_lines.extend(lines[q2_end+1:])  # ما بعد السؤال 2
        
        return '\n'.join(new_lines)
    
    # إذا لم نجد السؤالين، نرجع المحتوى كما هو
    return content

# الحصول على المحتوى المدخل من HTML
input_content = """{{USER_INPUT}}"""

# تطبيق الدالة لتبديل الأسئلة
output_content = swap_questions(input_content)

# إرجاع النتيجة لعرضها في HTML
output_content</pre>
            </div>
        </div>

        <div id="statusMessage" class="status">
            <p id="statusText"></p>
        </div>

        <footer>
            <p>تم التطوير باستخدام Pyodide لتشغيل Python في المتصفح</p>
            <p>© 2024 - أداة تبديل فقرات أسئلة Word</p>
        </footer>
    </div>

    <script>
        // حالة تهيئة Pyodide
        let pyodide = null;
        let pythonInitialized = false;

        // تهيئة Pyodide عند تحميل الصفحة
        async function initializePyodide() {
            const statusDiv = document.getElementById('statusMessage');
            const statusText = document.getElementById('statusText');
            
            statusDiv.className = 'status loading';
            statusText.innerHTML = '<span class="loading-spinner"></span> جارٍ تحميل Python في المتصفح... قد يستغرق هذا بضع لحظات';
            statusDiv.style.display = 'block';
            
            try {
                // تحميل Pyodide
                pyodide = await loadPyodide({
                    indexURL: "https://cdn.jsdelivr.net/pyodide/v0.25.0/full/"
                });
                
                pythonInitialized = true;
                
                statusDiv.className = 'status success';
                statusText.innerHTML = '<i class="fas fa-check-circle"></i> تم تحميل Python بنجاح في المتصفح! يمكنك الآن تشغيل الكود.';
                
                // إخفاء رسالة الحالة بعد 3 ثوان
                setTimeout(() => {
                    statusDiv.style.display = 'none';
                }, 3000);
                
            } catch (error) {
                console.error('Error loading Pyodide:', error);
                statusDiv.className = 'status error';
                statusText.innerHTML = `<i class="fas fa-exclamation-circle"></i> خطأ في تحميل Python: ${error.message}`;
            }
        }

        // تشغيل كود Python
        async function runPythonCode() {
            if (!pythonInitialized) {
                showStatus('برجاء الانتظار حتى يتم تحميل Python في المتصفح أولاً', 'error');
                return;
            }
            
            const inputText = document.getElementById('inputText').value.trim();
            if (!inputText) {
                showStatus('الرجاء إدخال محتوى في مربع الإدخال أولاً', 'error');
                return;
            }
            
            // تحديث كود Python بعرضه مع المحتوى المدخل
            const pythonCode = document.getElementById('pythonCodeDisplay').textContent;
            const codeWithInput = pythonCode.replace('{{USER_INPUT}}', inputText.replace(/\\/g, '\\\\').replace(/"/g, '\\"').replace(/\n/g, '\\n'));
            
            const statusDiv = document.getElementById('statusMessage');
            const statusText = document.getElementById('statusText');
            const runBtn = document.getElementById('runPythonBtn');
            
            statusDiv.className = 'status loading';
            statusText.innerHTML = '<span class="loading-spinner"></span> جارٍ تنفيذ كود Python...';
            statusDiv.style.display = 'block';
            runBtn.disabled = true;
            runBtn.innerHTML = '<span class="loading-spinner"></span> جاري التشغيل...';
            
            try {
                // تنفيذ كود Python
                const result = await pyodide.runPythonAsync(codeWithInput);
                
                // عرض النتيجة
                document.getElementById('outputText').value = result;
                
                statusDiv.className = 'status success';
                statusText.innerHTML = '<i class="fas fa-check-circle"></i> تم تبديل الفقرات بنجاح!';
                
            } catch (error) {
                console.error('Python execution error:', error);
                statusDiv.className = 'status error';
                statusText.innerHTML = `<i class="fas fa-exclamation-circle"></i> خطأ في تنفيذ Python: ${error.message}`;
            } finally {
                runBtn.disabled = false;
                runBtn.innerHTML = '<i class="fab fa-python"></i> تشغيل Python لتبديل الفقرات';
                
                // إخفاء رسالة الحالة بعد 5 ثوان
                setTimeout(() => {
                    statusDiv.style.display = 'none';
                }, 5000);
            }
        }

        // عرض رسالة حالة
        function showStatus(message, type = 'info') {
            const statusDiv = document.getElementById('statusMessage');
            const statusText = document.getElementById('statusText');
            
            statusDiv.className = `status ${type}`;
            statusText.innerHTML = message;
            statusDiv.style.display = 'block';
            
            // إخفاء رسالة الحالة بعد 5 ثوان
            setTimeout(() => {
                statusDiv.style.display = 'none';
            }, 5000);
        }

        // تحميل مثال
        function loadExample() {
            const exampleContent = `***1. he _______ plays football on weekends.***
***a***      ***does***   ***b***      ***always***   ***c***      ***has***
***2. How often _______ drink coffee?***
***a***      ***does***   ***b***      ***did***    ***c***      ***do***
***3. My friends are _______ to the museum tomorrow.***
***a***      ***go***       ***b***      ***goes***   ***c***      ***going***`;
            
            document.getElementById('inputText').value = exampleContent;
            showStatus('تم تحميل مثال بنجاح!', 'success');
        }

        // نسخ النتيجة
        function copyOutput() {
            const outputText = document.getElementById('outputText');
            if (!outputText.value.trim()) {
                showStatus('لا يوجد محتوى لنسخه', 'error');
                return;
            }
            
            outputText.select();
            document.execCommand('copy');
            
            showStatus('تم نسخ المحتوى المعدل إلى الحافظة بنجاح!', 'success');
        }

        // مسح جميع الحقول
        function clearAll() {
            document.getElementById('inputText').value = '';
            document.getElementById('outputText').value = '';
            showStatus('تم مسح جميع الحقول بنجاح!', 'success');
        }

        // تهيئة Pyodide عند تحميل الصفحة
        window.addEventListener('load', () => {
            initializePyodide();
        });
    </script>
</body>
</html>
