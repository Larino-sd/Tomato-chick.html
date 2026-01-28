# Tomato-chick.html<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>المساعد الزراعي الذكي - فحص الطماطم</title>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-color: #2e7d32;
            --secondary-color: #e8f5e9;
            --text-color: #333;
            --bg-color: #f4f7f6;
        }

        body {
            font-family: 'Tajawal', sans-serif;
            background-color: var(--bg-color);
            margin: 0;
            padding: 20px;
            color: var(--text-color);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        .main-card {
            background: white;
            width: 100%;
            max-width: 600px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.08);
            overflow: hidden;
            border: 1px solid #eee;
        }

        .header {
            background: var(--primary-color);
            color: white;
            padding: 25px;
            text-align: center;
        }

        .header h1 { margin: 0; font-size: 22px; }
        .header p { margin: 5px 0 0; opacity: 0.9; font-size: 14px; }

        .content { padding: 25px; }

        /* منطقة الرفع */
        .upload-area {
            border: 2px dashed #cbd5e0;
            border-radius: 12px;
            padding: 30px;
            text-align: center;
            cursor: pointer;
            transition: 0.3s;
            background: #fafafa;
        }
        .upload-area:hover {
            border-color: var(--primary-color);
            background: var(--secondary-color);
        }
        .upload-icon { font-size: 40px; margin-bottom: 10px; }
        .upload-text { color: #555; font-weight: bold; }
        
        input[type="file"] { display: none; }

        /* منطقة النتائج */
        #result-section { display: none; margin-top: 25px; }
        
        .image-preview {
            width: 100%;
            height: 250px;
            object-fit: contain; /* تعديل لمنع مط الصورة */
            background-color: #000;
            border-radius: 8px;
            margin-bottom: 20px;
        }

        .prediction-item { margin-bottom: 15px; }
        
        .label-row {
            display: flex;
            justify-content: space-between;
            margin-bottom: 5px;
            font-size: 14px;
            font-weight: bold;
        }

        .progress-bg {
            background: #eee;
            border-radius: 10px;
            height: 10px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            border-radius: 10px;
            transition: width 0.6s ease;
        }

        /* صندوق النصائح */
        .advice-box {
            margin-top: 25px;
            background: #e3f2fd;
            border-right: 5px solid #2196f3;
            padding: 15px 20px;
            border-radius: 8px;
        }
        .advice-title {
            color: #1565c0;
            font-weight: bold;
            margin-bottom: 10px;
            font-size: 16px;
        }
        .advice-text { font-size: 14px; line-height: 1.6; color: #333; }
        .advice-text ul { padding-right: 20px; margin: 0; }
        .advice-text li { margin-bottom: 5px; }

        /* التحميل */
        .loading-spinner {
            border: 4px solid #f3f3f3;
            border-top: 4px solid var(--primary-color);
            border-radius: 50%;
            width: 30px;
            height: 30px;
            animation: spin 1s linear infinite;
            margin: 20px auto;
            display: none;
        }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
    </style>
</head>
<body>

<div class="main-card">
    <div class="header">
        <h1>كاشف أمراض الطماطم 🍅</h1>
        <p>تشخيص ذكي ونصائح زراعية فورية</p>
    </div>

    <div class="content">
        <label for="image-upload" class="upload-area">
            <div class="upload-icon">📷</div>
            <div class="upload-text">اضغط هنا لرفع صورة الورقة</div>
        </label>
        <input type="file" id="image-upload" accept="image/*" onchange="handleFileUpload(event)">

        <div id="loading" class="loading-spinner"></div>

        <div id="result-section">
            <img id="preview-image" class="image-preview" src="" alt="صورة المعاينة">
            
            <div id="predictions-container"></div>

            <div id="advice-card" class="advice-box" style="display: none;">
                <div class="advice-title">💡 التشخيص والعلاج:</div>
                <div id="advice-content" class="advice-text"></div>
            </div>
        </div>
    </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest/dist/tf.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/@teachablemachine/image@latest/dist/teachablemachine-image.min.js"></script>

<script>
    // 1. إعداد النموذج
    const URL = "https://teachablemachine.withgoogle.com/models/ZyT9_W2BT/";
    let model, maxPredictions;

    // 2. قاعدة بيانات النصائح
    // النصائح مكتوبة بطريقة عامة لتغطية احتمالات اختلاف الأسماء
    const adviceDatabase = {
        "bacterial": `
            <strong>التبقع البكتيري (Bacterial Spot)</strong><br>
            <ul>
                <li>تخلص من الأجزاء المصابة واحرقها فوراً.</li>
                <li>استخدم مركبات النحاس (Copper) للرش.</li>
                <li>تجنب الري بالرش لتقليل الرطوبة.</li>
            </ul>`,
        "early": `
            <strong>اللفحة المبكرة (Early Blight)</strong><br>
            <ul>
                <li>قم بتقليم الأوراق السفلية المصابة.</li>
                <li>استخدم مبيدات فطرية (مانكوزيب أو أزوكسي ستروبين).</li>
                <li>حافظ على برنامج تسميد قوي لتقوية النبات.</li>
            </ul>`,
        "late": `
            <strong>اللفحة المتأخرة (Late Blight) - خطير ⚠️</strong><br>
            <ul>
                <li>تخلص من النباتات المصابة بشدة فوراً.</li>
                <li>استخدم مبيدات جهازية قوية (ميتالاكسيل).</li>
                <li>أوقف الري فوراً لتقليل انتشار الفطر.</li>
            </ul>`,
        "mold": `
            <strong>عفن الأوراق (Leaf Mold)</strong><br>
            <ul>
                <li>السبب الرئيسي هو رطوبة البيوت المحمية العالية.</li>
                <li>قم بزيادة التهوية فوراً.</li>
                <li>استخدم مبيدات فطرية وقائية.</li>
            </ul>`,
        "septoria": `
            <strong>تبقع سبتوريا (Septoria)</strong><br>
            <ul>
                <li>نظف الحقل من الحشائش وبقايا النباتات.</li>
                <li>عقم الأدوات الزراعية.</li>
                <li>استخدم مبيدات الكلوروثالونيل.</li>
            </ul>`,
        "spider": `
            <strong>العنكبوت الأحمر (Spider Mites)</strong><br>
            <ul>
                <li>رش النبات بالماء لغسل العناكب (يكرهون الرطوبة).</li>
                <li>استخدم مبيد (أبامكتين) أو زيت النيم.</li>
            </ul>`,
        "target": `
            <strong>تبقع الهدف (Target Spot)</strong><br>
            <ul>
                <li>حسن التهوية بين النباتات.</li>
                <li>تأكد من سلامة الشتلات قبل الزراعة.</li>
                <li>رش وقائي بمبيدات فطرية واسعة الطيف.</li>
            </ul>`,
        "curl": `
            <strong>فيروس تجعد الأوراق (Yellow Leaf Curl)</strong><br>
            <ul>
                <li>لا يوجد علاج للفيروس، اقلع النبات واحرفه.</li>
                <li>كافح "الذبابة البيضاء" فهي الناقل للمرض.</li>
                <li>استخدم أصناف مقاومة في الموسم القادم.</li>
            </ul>`,
        "mosaic": `
            <strong>فيروس الموزاييك (Mosaic Virus)</strong><br>
            <ul>
                <li>عقم يديك وأدواتك، الفيروس ينتقل باللمس.</li>
                <li>تخلص من النباتات المصابة.</li>
                <li>امنع التدخين بالقرب من الحقل.</li>
            </ul>`,
        "healthy": `
            <strong>✅ النبات سليم</strong><br>
            استمر في العناية المعتادة (ري منتظم وتسميد متوازن).`,
        "سليم": `
            <strong>✅ النبات سليم</strong><br>
            استمر في العناية المعتادة.`
    };

    // 3. تحميل النموذج
    async function init() {
        const modelURL = URL + "model.json";
        const metadataURL = URL + "metadata.json";
        try {
            model = await tmImage.load(modelURL, metadataURL);
            maxPredictions = model.getTotalClasses();
            console.log("Model Loaded. Classes: ", model.getClassLabels()); // للتأكد من الأسماء
        } catch (e) {
            alert("فشل تحميل النموذج! تأكد من الاتصال بالإنترنت.");
        }
    }
    init();

    // 4. التعامل مع رفع الصورة
    function handleFileUpload(event) {
        const file = event.target.files[0];
        if (!file) return;

        // إظهار التحميل وإخفاء النتائج القديمة
        document.getElementById("loading").style.display = "block";
        document.getElementById("result-section").style.display = "none";
        document.getElementById("advice-card").style.display = "none";

        const reader = new FileReader();
        reader.onload = function(e) {
            const img = new Image();
            img.src = e.target.result;
            img.onload = async function() {
                document.getElementById("preview-image").src = img.src;
                await predict(img);
                document.getElementById("loading").style.display = "none";
                document.getElementById("result-section").style.display = "block";
            };
        }
        reader.readAsDataURL(file);
    }

    // 5. التنبؤ وعرض النتائج
    async function predict(image) {
        if (!model) return;
        
        const predictions = await model.predict(image);
        const container = document.getElementById("predictions-container");
        container.innerHTML = "";

        // البحث عن أعلى نتيجة
        let highestProb = 0;
        let bestClass = "";

        for (let i = 0; i < maxPredictions; i++) {
            const className = predictions[i].className;
            const probability = predictions[i].probability * 100;

            if (probability > highestProb) {
                highestProb = probability;
                bestClass = className;
            }

            // عرض الشريط فقط إذا النسبة اعلى من 5%
            if (probability > 5) {
                const div = document.createElement("div");
                div.className = "prediction-item";
                
                // تحديد اللون
                let color = "#2e7d32"; // أخضر
                if (probability > 50 && !className.toLowerCase().includes("healthy") && !className.includes("سليم")) {
                    color = "#d32f2f"; // أحمر للخطر
                }

                div.innerHTML = `
                    <div class="label-row">
                        <span>${className}</span>
                        <span>${probability.toFixed(1)}%</span>
                    </div>
                    <div class="progress-bg">
                        <div class="progress-fill" style="width: ${probability}%; background-color: ${color}"></div>
                    </div>
                `;
                container.appendChild(div);
            }
        }

        // عرض النصيحة
        getAdvice(bestClass, highestProb);
    }

    // 6. دالة النصائح الذكية (Fuzzy Search)
    function getAdvice(className, probability) {
        if (probability < 60) {
            document.getElementById("advice-card").style.display = "block";
            document.getElementById("advice-content").innerHTML = "⚠️ الصورة غير واضحة أو المرض غير معروف بدقة. يرجى المحاولة بصورة أوضح.";
            return;
        }

        // تحويل الاسم لحروف صغيرة للبحث
        const lowerName = className.toLowerCase();
        let advice = "";

        // البحث عن الكلمات المفتاحية
        if (lowerName.includes("bacterial")) advice = adviceDatabase["bacterial"];
        else if (lowerName.includes("early")) advice = adviceDatabase["early"];
        else if (lowerName.includes("late")) advice = adviceDatabase["late"];
        else if (lowerName.includes("mold")) advice = adviceDatabase["mold"];
        else if (lowerName.includes("septoria")) advice = adviceDatabase["septoria"];
        else if (lowerName.includes("spider") || lowerName.includes("mite")) advice = adviceDatabase["spider"];
        else if (lowerName.includes("target")) advice = adviceDatabase["target"];
        else if (lowerName.includes("curl") || lowerName.includes("yellow")) advice = adviceDatabase["curl"];
        else if (lowerName.includes("mosaic")) advice = adviceDatabase["mosaic"];
        else if (lowerName.includes("healthy") || lowerName.includes("سليم")) advice = adviceDatabase["healthy"];
        else {
            advice = `تم رصد: <strong>${className}</strong>.<br>لا توجد نصيحة محددة في قاعدة البيانات لهذا الاسم. يرجى مراجعة المرشد الزراعي.`;
        }

        document.getElementById("advice-card").style.display = "block";
        document.getElementById("advice-content").innerHTML = advice;
    }
</script>

</body>
</html>
