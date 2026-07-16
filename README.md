<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>تشخيص أمراض الطماطم - مستقبل الزراعة الذكية</title>
    <style>
        /* ========== متغيرات المستقبل ========== */
        :root {
            --primary-glow: #00ffaa;
            --secondary-glow: #00ccff;
            --bg-dark: #0a0f1e;
            --glass-bg: rgba(10, 20, 30, 0.6);
            --card-bg: rgba(20, 30, 50, 0.7);
            --text-primary: #f0f4fa;
            --text-secondary: #b0c0d0;
            --error-glow: #ff4d6d;
            --success-glow: #4caf50;
            --border-neon: 0 0 10px var(--primary-glow);
            --transition-smooth: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
        }

        /* ========== إعادة تعيين المستقبل ========== */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Poppins', system-ui, sans-serif;
        }

        body {
            min-height: 100vh;
            background: radial-gradient(ellipse at 30% 40%, #1a2f3f, #0b0e17);
            background-attachment: fixed;
            color: var(--text-primary);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 1.5rem;
            position: relative;
            overflow-x: hidden;
        }

        /* خلفية متحركة شبيهة بالنيون */
        body::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: repeating-linear-gradient(45deg, 
                transparent, 
                transparent 40px, 
                rgba(0, 255, 170, 0.03) 40px, 
                rgba(0, 200, 255, 0.03) 80px);
            animation: scan 30s linear infinite;
            pointer-events: none;
            z-index: 0;
        }

        @keyframes scan {
            0% { transform: translate(0, 0) rotate(0deg); }
            100% { transform: translate(50px, 50px) rotate(5deg); }
        }

        .container {
            width: 100%;
            max-width: 1300px;
            z-index: 10;
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            background: var(--glass-bg);
            border: 1px solid rgba(0, 255, 200, 0.2);
            border-radius: 3rem 3rem 2rem 2rem;
            padding: 2.5rem;
            box-shadow: 0 25px 40px -10px rgba(0, 0, 0, 0.7), 0 0 0 1px rgba(0, 255, 200, 0.2) inset;
            transition: var(--transition-smooth);
        }

        /* ========== رأس المستقبل ========== */
        .header {
            text-align: center;
            margin-bottom: 3rem;
            position: relative;
        }

        .header h1 {
            font-size: 3.2rem;
            font-weight: 700;
            background: linear-gradient(135deg, #a0f0ff, #70ffb0);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 20px rgba(0, 255, 200, 0.6);
            letter-spacing: 2px;
            margin-bottom: 0.5rem;
        }

        .header .subtitle {
            font-size: 1.2rem;
            color: var(--text-secondary);
            background: rgba(0, 255, 200, 0.1);
            display: inline-block;
            padding: 0.5rem 2rem;
            border-radius: 50px;
            border: 1px solid rgba(0, 255, 200, 0.3);
            backdrop-filter: blur(5px);
            box-shadow: 0 0 15px rgba(0, 200, 255, 0.3);
        }

        /* ========== مؤشر تحميل النموذج ========== */
        .model-loader {
            background: var(--card-bg);
            border-radius: 60px;
            padding: 1.2rem 2rem;
            margin-bottom: 2.5rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
            border: 1px solid rgba(0, 255, 200, 0.3);
            box-shadow: 0 0 30px rgba(0, 255, 200, 0.2);
            transition: var(--transition-smooth);
        }

        .loader-info {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .loader-icon {
            width: 40px;
            height: 40px;
            border: 3px solid transparent;
            border-top: 3px solid var(--primary-glow);
            border-right: 3px solid var(--secondary-glow);
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .loader-text {
            font-size: 1.2rem;
            font-weight: 500;
            color: #ccf0ff;
        }

        .loader-status {
            padding: 0.5rem 1.2rem;
            border-radius: 40px;
            background: rgba(0, 0, 0, 0.4);
            font-weight: 600;
            letter-spacing: 1px;
            border: 1px solid;
            transition: 0.3s;
        }

        .status-loading {
            border-color: #ffaa33;
            color: #ffaa33;
            box-shadow: 0 0 10px #ffaa33;
        }

        .status-ready {
            border-color: #00ffaa;
            color: #00ffaa;
            box-shadow: 0 0 15px #00ffaa;
        }

        .status-error {
            border-color: #ff4d6d;
            color: #ff4d6d;
            box-shadow: 0 0 15px #ff4d6d;
        }

        /* ========== منطقة رفع الصورة ========== */
        .upload-section {
            margin: 2.5rem 0;
        }

        .upload-area {
            background: rgba(0, 20, 30, 0.6);
            border: 2px dashed rgba(0, 255, 200, 0.5);
            border-radius: 50px;
            padding: 2.5rem;
            text-align: center;
            cursor: pointer;
            transition: var(--transition-smooth);
            backdrop-filter: blur(8px);
            box-shadow: 0 0 20px rgba(0, 255, 200, 0.2);
        }

        .upload-area:hover {
            border-color: var(--primary-glow);
            box-shadow: 0 0 35px var(--primary-glow);
            transform: scale(1.02);
            background: rgba(0, 30, 50, 0.7);
        }

        .upload-area.disabled {
            opacity: 0.4;
            pointer-events: none;
            filter: grayscale(0.6);
            border-color: #888;
        }

        .upload-icon {
            font-size: 4rem;
            margin-bottom: 1rem;
            filter: drop-shadow(0 0 10px cyan);
        }

        .upload-area h3 {
            font-size: 2rem;
            font-weight: 500;
            color: #e0f0ff;
        }

        .upload-area p {
            color: var(--text-secondary);
            font-size: 1.1rem;
        }

        /* ========== معاينة الصورة ========== */
        .preview-container {
            margin: 2rem 0;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
        }

        .image-preview {
            max-width: 350px;
            max-height: 350px;
            border-radius: 30px;
            border: 3px solid rgba(0, 255, 200, 0.7);
            box-shadow: 0 0 40px rgba(0, 255, 200, 0.5);
            object-fit: cover;
            transition: 0.4s;
            background: #111;
            display: none;
        }

        .image-preview.show {
            display: block;
        }

        /* ========== نتائج التشخيص ========== */
        .results-panel {
            background: var(--card-bg);
            border-radius: 40px;
            padding: 2rem;
            border: 1px solid rgba(0, 255, 200, 0.3);
            backdrop-filter: blur(15px);
            box-shadow: 0 0 40px rgba(0, 200, 255, 0.3);
            margin: 2rem 0;
        }

        .results-title {
            font-size: 1.8rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            margin-bottom: 1.5rem;
            color: #b5ffff;
            text-shadow: 0 0 10px cyan;
        }

        .results-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 1.2rem;
        }

        .result-card {
            background: rgba(10, 30, 50, 0.8);
            border-radius: 25px;
            padding: 1.2rem;
            border: 1px solid rgba(0, 255, 200, 0.2);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.6);
            transition: 0.2s;
            backdrop-filter: blur(5px);
        }

        .result-card:hover {
            transform: translateY(-5px);
            border-color: var(--primary-glow);
            box-shadow: 0 0 25px var(--primary-glow);
        }

        .class-name {
            font-size: 1.3rem;
            font-weight: 600;
            margin-bottom: 0.5rem;
            color: #c0f5ff;
        }

        .confidence-bar {
            width: 100%;
            height: 10px;
            background: #2a3a4a;
            border-radius: 10px;
            margin: 0.8rem 0;
            overflow: hidden;
        }

        .confidence-fill {
            height: 100%;
            background: linear-gradient(90deg, #00ccff, #a0ffc0);
            border-radius: 10px;
            box-shadow: 0 0 10px #00ffaa;
            width: 0%;
            transition: width 0.5s ease-out;
        }

        .confidence-value {
            font-size: 1.1rem;
            color: var(--text-secondary);
        }

        /* رسالة عدم وجود نتائج */
        .no-results {
            text-align: center;
            padding: 2rem;
            color: var(--text-secondary);
            font-size: 1.2rem;
            background: rgba(0,0,0,0.3);
            border-radius: 40px;
            border: 1px dashed cyan;
        }

        /* ========== تذييل المستقبل ========== */
        .footer {
            margin-top: 3rem;
            text-align: center;
            color: var(--text-secondary);
            border-top: 1px solid rgba(0, 255, 200, 0.3);
            padding-top: 2rem;
            display: flex;
            flex-direction: column;
            gap: 0.8rem;
        }

        .footer-note {
            background: rgba(0, 0, 0, 0.4);
            padding: 0.8rem 1.5rem;
            border-radius: 50px;
            display: inline-block;
            margin: 0 auto;
            border: 1px solid #ffaa3366;
            color: #ffccaa;
            font-weight: 500;
            backdrop-filter: blur(4px);
        }

        .designer-signature {
            font-size: 1.2rem;
            letter-spacing: 2px;
            text-shadow: 0 0 8px magenta;
            color: #ffb0ff;
        }

        .designer-signature span {
            font-weight: 700;
            background: linear-gradient(135deg, #f0f, #0ff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            font-size: 1.5rem;
        }

        /* ========== الأكواد الجديدة المضافة لتفاصيل المشروع التفاعلية ========== */
        .project-details-section {
            margin: 3rem 0 1.5rem 0;
            text-align: center;
        }

        .project-details-title {
            font-size: 1.6rem;
            color: var(--primary-glow);
            margin-bottom: 1.5rem;
            text-shadow: 0 0 10px rgba(0, 255, 170, 0.4);
        }

        .info-buttons-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 1.2rem;
            width: 100%;
        }

        .info-btn {
            background: rgba(15, 25, 45, 0.8);
            border: 1px solid rgba(0, 255, 170, 0.3);
            border-radius: 20px;
            padding: 1.2rem 1rem;
            color: var(--text-primary);
            font-size: 1.05rem;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition-smooth);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.4);
        }

        .info-btn:hover {
            background: rgba(0, 255, 170, 0.12);
            border-color: var(--primary-glow);
            box-shadow: 0 0 20px rgba(0, 255, 170, 0.4);
            transform: translateY(-4px);
        }

        .info-btn-icon {
            font-size: 1.8rem;
        }

        /* تصميم النافذة المنبثقة (Modal) */
        .custom-modal {
            display: none;
            position: fixed;
            z-index: 10000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            overflow: auto;
            background-color: rgba(10, 15, 30, 0.93);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            align-items: center;
            justify-content: center;
            padding: 1rem;
        }

        .custom-modal-content {
            background-color: #0d1627;
            border: 2px solid var(--primary-glow);
            box-shadow: 0 0 35px rgba(0, 255, 170, 0.4);
            border-radius: 30px;
            width: 100%;
            max-width: 650px;
            padding: 2.5rem;
            color: var(--text-primary);
            position: relative;
            animation: modalSlideIn 0.4s cubic-bezier(0.18, 0.89, 0.32, 1.15);
            direction: rtl;
            text-align: right;
        }

        @keyframes modalSlideIn {
            from { transform: translateY(-40px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        .custom-modal-close {
            color: var(--error-glow);
            position: absolute;
            left: 20px;
            top: 20px;
            font-size: 32px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.2s;
            line-height: 1;
        }

        .custom-modal-close:hover {
            color: #ff1a40;
            transform: scale(1.15);
        }

        .modal-body-content {
            font-size: 1.15rem;
            line-height: 1.8;
            margin-top: 1rem;
        }

        .modal-body-content h2 {
            color: var(--primary-glow);
            margin-bottom: 1.2rem;
            border-bottom: 1px dashed rgba(0, 255, 170, 0.3);
            padding-bottom: 0.6rem;
            font-size: 1.6rem;
        }

        .modal-body-content h3 {
            color: var(--secondary-glow);
            margin-top: 1.5rem;
            margin-bottom: 0.8rem;
            font-size: 1.3rem;
        }

        .modal-body-content p {
            margin-bottom: 1rem;
        }

        .modal-body-content ul, .modal-body-content ol {
            margin-right: 1.8rem;
            margin-bottom: 1.2rem;
        }

        .modal-body-content li {
            margin-bottom: 0.5rem;
        }

        .modal-body-content a {
            color: var(--secondary-glow);
            text-decoration: none;
            font-weight: bold;
            border-bottom: 1px dashed var(--secondary-glow);
            transition: 0.2s;
        }

        .modal-body-content a:hover {
            color: #fff;
            border-bottom-style: solid;
            text-shadow: 0 0 10px var(--secondary-glow);
        }
    </style>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@2.0.0/dist/tf.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@teachablemachine/image@0.8/dist/teachablemachine-image.min.js"></script>
</head>
<body>
    <div class="container">
        <div class="header">
            <h>مستقبل الزراعة الذكية</h1>
            <div class="subtitle">تشخيص فوري لأمراض الامراض نبات الطماطم باستخدام تقنيه ال teachablemachine</div>
        </div>

        <div class="model-loader" id="modelLoader">
            <div class="loader-info">
                <div class="loader-icon" id="loaderIcon"></div>
                <span class="loader-text" id="loaderText">جاري تهيئة النموذج العصبي...</span>
            </div>
            <div class="loader-status status-loading" id="loaderStatus">⏳ تحميل...</div>
        </div>

        <div class="upload-section">
            <div class="upload-area disabled" id="uploadArea">
                <div class="upload-icon">🌿🔬</div>
                <h3>اسحب وأفلت صورة الورقة هنا</h3>
                <p>أو انقر لاختيار ملف (JPEG, PNG)</p>
                <input type="file" id="fileInput" accept="image/*" style="display: none;" disabled>
            </div>
        </div>

        <div class="preview-container">
            <img class="image-preview" id="imagePreview" alt="معاينة الصورة">
        </div>

        <div class="results-panel" id="resultsPanel" style="display: none;">
            <div class="results-title">
                <span>📊 نتائج التحليل الطبيعي</span>
            </div>
            <div class="results-grid" id="resultsGrid"></div>
            <div id="noResultsMessage" class="no-results" style="display: none;">
                لم يتم اكتشاف أي إصابة بنسبة ثقة تذكر.
            </div>
        </div>

        <div class="project-details-section">
            <h3 class="project-details-title">📁 استكشف تفاصيل المشروع والتقنيات</h3>
            <div class="info-buttons-grid">
                <button class="info-btn" onclick="openCustomModal('btn1')">
                    <span class="info-btn-icon">📝</span>
                    <span>المقدمة</span>
                </button>
                <button class="info-btn" onclick="openCustomModal('btn2')">
                    <span class="info-btn-icon">🔬</span>
                    <span>الجانب التقني</span>
                </button>
                <button class="info-btn" onclick="openCustomModal('btn3')">
                    <span class="info-btn-icon">🌐</span>
                    <span>المنصة والمعمارية</span>
                </button>
                <button class="info-btn" onclick="openCustomModal('btn4')">
                    <span class="info-btn-icon">⚙️</span>
                    <span>محرك التشغيل</span>
                </button>
                <button class="info-btn" onclick="openCustomModal('btn5')">
                    <span class="info-btn-icon">📱</span>
                    <span>تفاصيل الواجهة</span>
                </button>
                <button class="info-btn" onclick="openCustomModal('btn6')">
                    <span class="info-btn-icon">🛠️</span>
                    <span>التحديات التقنية</span>
                </button>
            </div>
        </div>

        <div class="footer">
            <div class="footer-note">
                ⚠️ ملاحظة: هذا النموذج لا يستطيع العمل في البيئة المفتوحة بكل دقة. يرجى استخدامه في ظروف معملية.
            </div>
            <div class="designer-signature">
                تصميم <span>Larino</span> || 2026
            </div>
        </div>
    </div>

    <div id="customInfoModal" class="custom-modal">
        <div class="custom-modal-content">
            <span class="custom-modal-close" onclick="closeCustomModal()">&times;</span>
            <div id="modalBodyContent" class="modal-body-content">
                </div>
        </div>
    </div>

    <script>
        let model, maxPredictions;
        const modelURL = 'https://teachablemachine.withgoogle.com/models/CEHWThrLc/model.json';
        const metadataURL = 'https://teachablemachine.withgoogle.com/models/CEHWThrLc/metadata.json';

        const loaderIcon = document.getElementById('loaderIcon');
        const loaderText = document.getElementById('loaderText');
        const loaderStatus = document.getElementById('loaderStatus');
        const uploadArea = document.getElementById('uploadArea');
        const fileInput = document.getElementById('fileInput');
        const imagePreview = document.getElementById('imagePreview');
        const resultsPanel = document.getElementById('resultsPanel');
        const resultsGrid = document.getElementById('resultsGrid');
        const noResultsMessage = document.getElementById('noResultsMessage');

        let isModelLoaded = false;

        async function loadModel() {
            try {
                model = await tmImage.load(modelURL, metadataURL);
                maxPredictions = model.getTotalClasses();

                isModelLoaded = true;
                loaderText.innerText = 'النموذج جاهز! تم تفعيل المستشعرات.';
                loaderStatus.innerText = '✅ جاهز';
                loaderStatus.className = 'loader-status status-ready';
                loaderIcon.style.animation = 'none';
                loaderIcon.style.border = '3px solid #00ffaa';

                uploadArea.classList.remove('disabled');
                fileInput.disabled = false;
            } catch (error) {
                loaderStatus.innerText = '❌ خطأ';
                loaderStatus.className = 'loader-status status-error';
            }
        }

        window.addEventListener('load', loadModel);

        uploadArea.addEventListener('click', () => { if (isModelLoaded) fileInput.click(); });

        fileInput.addEventListener('change', (e) => {
            const file = e.target.files[0];
            if (file) handleImage(file);
        });

        function handleImage(file) {
            const reader = new FileReader();
            reader.onload = async (e) => {
                imagePreview.src = e.target.result;
                imagePreview.classList.add('show');
                await predictImage();
            };
            reader.readAsDataURL(file);
        }

        // ==========================================
        // تعديل اسم الفئة هنا (تم إصلاح منطق التحقق)
        // ==========================================
        function formatClassName(originalName) {
            const name = originalName.toLowerCase().trim();
            // يتحقق مما إذا كان الاسم يحتوي على "class 3" بمسافة أو بدونها
            if (name === 'class 3' || name === 'class3') {
                return 'عفن أوراق الطماطم';
            }
            return originalName;
        }

        async function predictImage() {
            if (!isModelLoaded) return;

            const img = new Image();
            img.src = imagePreview.src;
            img.onload = async () => {
                resultsPanel.style.display = 'block';
                const prediction = await model.predict(img);
                const sorted = prediction.sort((a, b) => b.probability - a.probability);
                
                const threshold = 0.01; 
                const significant = sorted.filter(p => p.probability > threshold);

                if (significant.length === 0) {
                    resultsGrid.innerHTML = '';
                    noResultsMessage.style.display = 'block';
                    return;
                } else {
                    noResultsMessage.style.display = 'none';
                }

                let html = '';
                significant.forEach(p => {
                    let className = formatClassName(p.className);
                    const prob = (p.probability * 100).toFixed(2);
                    html += `
                        <div class="result-card">
                            <div class="class-name">${className}</div>
                            <div class="confidence-bar">
                                <div class="confidence-fill" style="width: ${prob}%;"></div>
                            </div>
                            <div class="confidence-value">${prob}%</div>
                        </div>
                    `;
                });
                resultsGrid.innerHTML = html;
            };
        }

        // =======================================================
        // منطق النوافذ المنبثقة لعرض معلومات وأزرار المشروع
        // =======================================================
        const customInfoModal = document.getElementById('customInfoModal');
        const modalBodyContent = document.getElementById('modalBodyContent');

        const modalContents = {
            btn1: {
                html: `
                    <h2>مقدمة عن المشروع 📝</h2>
                    <p>تطبيق ويب تفاعلي يعتمد على تشخيص أمراض أوراق الطماطم فورياً باستخدام الصور المحفوظة في الجهاز. تم تصميم المشروع ليعمل بالكامل داخل متصفح المستخدم لضمان الخصوصية والسرعة.</p>
                    <p style="margin-top: 20px; font-weight: bold;">🔗 إذا كنت تريد تجربة المشروع، اضغط هنا:</p>
                    <p><a href="https://larino-sd.github.io/Tomato-chick.html/" target="_blank">رابط موقع مشروع Tomato Chick</a></p>
                `
            },
            btn2: {
                html: `
                    <h2>الجانب التقني والنموذج 🔬</h2>
                    <h3 style="color: var(--secondary-glow);">1. تدريب النموذج والبيانات (Model & Dataset)</h3>
                    <p><strong>مصدر البيانات:</strong> تم تدريب النموذج باستخدام مجموعة بيانات من منصة Kaggle تحتوي على 10,000 صورة.</p>
                    <p><strong>تصنيف الأمراض:</strong> النموذج قادر على التعرف على 9 أمراض مختلفة تصيب أوراق الطماطم بالإضافة إلى الأوراق السليمة، بمعدل 1,000 صورة لكل تصنيف لضمان التوازن والدقة أثناء التدريب.</p>
                    <h3 style="color: var(--primary-glow); margin-top: 15px;">الأمراض التي يستطيع أن يكشف عنها هي:</h3>
                    <ol style="line-height: 1.8; margin-right: 25px;">
                        <li>إصابة سوس العنكبوت الأحمر ذو البقعتين.</li>
                        <li>تبقع أوراق سبتوريا.</li>
                        <li>عفن أوراق الطماطم.</li>
                        <li>اللفحة المتأخرة.</li>
                        <li>اللفحة المبكرة.</li>
                        <li>البقعة البكتيرية.</li>
                        <li>فيروس تجعد واصفرار أوراق الطماطم.</li>
                        <li>فيروس موزاييك.</li>
                        <li>بقعة الهدف.</li>
                    </ol>
                `
            },
            btn3: {
                html: `
                    <h2>المنصة والمعمارية 🌐</h2>
                    <p>تم تدريب وتطوير النموذج باستخدام منصة <strong>Google Teachable Machine</strong> المبنية فوق نموذج <strong>MobileNet</strong>، وهي معمارية خفيفة الوزن ومصممة خصيصاً للعمل بكفاءة على الأجهزة الذكية والمتصفحات ذات الموارد المحدودة.</p>
                    <p>يعتمد نموذج MobileNet على أوزان مسبقة التدريب، ونحن نقوم بتدريب الطبقات الأخيرة من النموذج.</p>
                    <h3 style="color: var(--secondary-glow); margin-top: 20px;">🔗 رابط نموذج Teachable Machine بعد تصديره بصيغة TensorFlow.js:</h3>
                    <p style="margin-top: 10px;"><a href="https://teachablemachine.withgoogle.com/models/CEHWThrLc/" target="_blank">رابط نموذج Teachable Machine الخاص بالمشروع</a></p>
                `
            },
            btn4: {
                html: `
                    <h2>محرك التشغيل (TensorFlow.js) ⚙️</h2>
                    <h3 style="color: var(--secondary-glow);">2. محرك التشغيل TensorFlow.js وهي مكتبة مفتوحة المصدر:</h3>
                    <p>يتم تصدير وتشغيل النموذج بصيغة TensorFlow.js، مما ينقل معالجة البيانات إلى متصفح العميل.</p>
                    <p>تغلبت المكتبة على قيود سرعة لغة JavaScript من خلال:</p>
                    <ul style="line-height: 1.8; margin-right: 25px;">
                        <li><strong>تسريع وحدة الرسوميات (GPU):</strong> توجيه العمليات الحسابية المعقدة مباشرة إلى وحدة معالجة الرسومات (GPU)، مما يتيح معالجة سريعة للحسابات.</li>
                        <li><strong>تقنية WebAssembly (WASM):</strong> في حال ضعف كرت الشاشة أو عدم دعمه، يتحول التشغيل تلقائياً إلى معمارية WASM لضمان تنفيذ العمليات بسرعة ممتازة مباشرة على المعالج (CPU).</li>
                    </ul>
                `
            },
            btn5: {
                html: `
                    <h2>تفاصيل الواجهة الأمامية 📱</h2>
                    <p>أما الواجهة الأمامية التي تتفاعل مع المستخدم:</p>
                    <p style="line-height: 1.8;">صُممت واجهة الويب التفاعلية للمشروع بالاستعانة بالذكاء الاصطناعي <strong>Gemini</strong> للحصول على تصميم مقبول ومستجيب بالكامل مع الهواتف والشاشات المختلفة.</p>
                `
            },
            btn6: {
                html: `
                    <h2>تحديات تقنية وحلول مستمرة 🛠️</h2>
                    <h3 style="color: var(--error-glow);">1. مشكلة المدخلات العشوائية:</h3>
                    <p><strong>التحدي:</strong> النموذج أحياناً يميل إلى تصنيف الأشياء غير المرتبطة بالنباتات مثل الطاولات أو الأثاث كأوراق طماطم مريضة أو سليمة بناءً على أقرب احتمال حسابي.</p>
                    <p><strong>ولكن لكل مشكلة حل:</strong> نوصي المستخدمين بالتشغيل في بيئة ذات خلفية رمادية أو أي لون، شرط ألا يظهر خلفها شيء، لتحسين الإضاءة ودقة النتائج.</p>
                    <h3 style="color: var(--success-glow); margin-top: 20px;">وهنالك حل قيد الإضافة قريباً، وهو إضافة كلاسات تدريبية إضافية:</h3>
                    <ul style="line-height: 1.8; margin-right: 25px;">
                        <li>Negative</li>
                        <li>Background Classes</li>
                    </ul>
                    <p>تعني هذه الإضافة تدريب النموذج ليتجاهل الصور إذا لم يوجد ورق نبات طماطم.</p>
                `
            }
        };

        function openCustomModal(key) {
            if (modalContents[key]) {
                modalBodyContent.innerHTML = modalContents[key].html;
                customInfoModal.style.display = 'flex';
            }
        }

        function closeCustomModal() {
            customInfoModal.style.display = 'none';
        }

        // إغلاق النافذة المنبثقة عند الضغط في أي مكان خارج المربع
        window.addEventListener('click', function(event) {
            if (event.target === customInfoModal) {
                closeCustomModal();
            }
        });
    </script>
</body>
</html>
