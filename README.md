<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>بوابة طلاب موقع النصيحة التعليمي - الشهادات التفاعلية</title>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700;900&family=Aref+Ruqaa:wght@400;700&display=swap" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <style>
        body { 
            font-family: 'Cairo', sans-serif; 
            background: linear-gradient(135deg, #0f172a, #1e293b); 
            display: flex; 
            flex-direction: column; 
            align-items: center; 
            padding: 20px; 
            margin: 0; 
            min-height: 100vh;
            color: #fff;
            position: relative;
        }

        /* نظام التنبيهات العلوي الهادئ */
        #notification-box {
            position: fixed;
            top: 20px;
            left: 50%;
            transform: translateX(-50%) translateY(-100px);
            background: #059669;
            color: white;
            padding: 12px 26px;
            border-radius: 10px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            z-index: 1000000;
            transition: transform 0.4s ease-in-out;
            border: 2px solid #fef08a;
            text-align: center;
        }
        #notification-box.show { transform: translateX(-50%) translateY(0); }

        /* صندوق البحث العصري والجميل للطلاب */
        .portal-search-box {
            background: #ffffff;
            color: #1e293b;
            width: 100%;
            max-width: 1000px;
            padding: 30px;
            border-radius: 16px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.5);
            margin-bottom: 25px;
            margin-top: 15px;
            box-sizing: border-box;
            border: 3px solid #d4af37;
            text-align: center;
        }
        .portal-search-box h2 { margin-top: 0; color: #1e293b; font-size: 26px; font-weight: 900; }
        .portal-search-box p { color: #64748b; font-size: 16px; margin-bottom: 20px; font-weight: bold; }
        
        .search-input-group {
            display: flex;
            gap: 12px;
            justify-content: center;
            flex-wrap: wrap;
            position: relative;
        }
        .search-input {
            flex: 1;
            min-width: 320px;
            padding: 14px 20px;
            font-size: 17px;
            font-family: 'Cairo', sans-serif;
            border: 2px solid #cbd5e1;
            border-radius: 10px;
            outline: none;
            transition: 0.3s;
            background: #f8fafc;
            color: #0f172a;
        }
        .search-input:focus { border-color: #2563eb; background: #fff; box-shadow: 0 0 12px rgba(37,99,235,0.25); }

        /* نتائج البحث الفورية */
        .suggestions-list {
            position: absolute;
            top: 58px;
            right: 0;
            left: 150px;
            background: #fff;
            border: 2px solid #cbd5e1;
            border-top: none;
            border-radius: 0 0 10px 10px;
            max-height: 240px;
            overflow-y: auto;
            z-index: 100;
            text-align: right;
            display: none;
            box-shadow: 0 10px 25px rgba(0,0,0,0.15);
        }
        .suggestion-item {
            padding: 12px 18px;
            cursor: pointer;
            border-bottom: 1px solid #f1f5f9;
            color: #334155;
            font-weight: bold;
            transition: 0.2s;
        }
        .suggestion-item:hover { background: #eff6ff; color: #1d4ed8; }

        .certificate { 
            position: relative; 
            width: 1000px; 
            height: 700px; 
            background-color: #ffffff; 
            border: 4px solid #475569; 
            overflow: hidden; 
            box-shadow: 0 20px 40px rgba(0,0,0,0.4); 
            box-sizing: border-box;
        }
        
        .pattern-top, .pattern-bottom { 
            position: absolute; 
            width: 100%; 
            height: 75px; 
            background-color: #64748b; 
            background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='60' height='60' viewBox='0 0 60 60'%3E%3Cg fill='none' stroke='%23d4af37' stroke-width='1.2' opacity='0.9'%3E%3Cpath d='M30 0L60 30L30 60L0 30Z'/%3E%3Cpath d='M0 0L60 60M60 0L0 60'/%3E%3Ccircle cx='30' cy='30' r='12'/%3E%3Cpath d='M30 10L50 30L30 50L10 30Z'/%3E%3C/g%3E%3C/svg%3E");
            background-size: 60px 75px;
            z-index: 5; 
        }
        .pattern-top { top: 0; border-bottom: 3px solid #d4af37; }
        .pattern-bottom { bottom: 0; left: 0; border-top: 3px solid #d4af37; }
        
        .side-bar { 
            position: absolute; 
            right: 170px; 
            top: 75px; 
            bottom: 75px; 
            width: 70px; 
            background-color: #64748b; 
            border-left: 2px solid #cbd5e1;
            border-right: 2px solid #cbd5e1;
            z-index: 2; 
        }
        
        .photo-container { 
            position: absolute; 
            right: 50px; 
            top: 230px; 
            width: 240px; 
            height: 240px; 
            background: radial-gradient(circle, #fde047 0%, #eab308 70%, #ca8a04 100%); 
            border-radius: 50%; 
            border: 6px solid #fef08a; 
            box-shadow: 0 10px 25px rgba(0,0,0,0.3); 
            display: flex; 
            justify-content: center; 
            align-items: center; 
            text-align: center; 
            cursor: pointer; 
            z-index: 10; 
            overflow: hidden; 
            font-weight: bold; 
            color: #1e293b; 
            transition: 0.3s; 
        }
        .photo-container:hover { transform: scale(1.04); }
        .photo-container .hint-text { padding: 15px; font-size: 15px; line-height: 1.5; text-shadow: 0 1px 2px rgba(255,255,255,0.6); }
        .photo-container img { width: 100%; height: 100%; object-fit: cover; display: none; border-radius: 50%; }
        
        .content { 
            position: absolute; 
            top: 75px; 
            left: 50px; 
            right: 240px; 
            bottom: 75px; 
            text-align: center; 
            z-index: 3; 
            padding: 20px; 
            display: flex; 
            flex-direction: column; 
            justify-content: space-between; 
        }
        
        .header { display: flex; justify-content: space-between; align-items: flex-start; margin-top: 10px; }
        
        .brand { text-align: right; }
        .logo-svg-box { width: 260px; height: 85px; margin-bottom: 2px; }
        .logo-svg-box svg { width: 100%; height: 100%; display: block; }
        .teacher { color: #1e293b; font-weight: bold; font-size: 17px; margin-top: 2px; text-align: right; }
        
        .date-box { text-align: center; margin-top: 5px; }
        .date-val { font-size: 16px; font-weight: bold; color: #334155; }
        .date-lbl { color: #1e293b; font-weight: bold; font-size: 15px; border-top: 2px solid #94a3b8; padding-top: 2px; }
        
        .center-group { margin-top: -10px; }
        .basmala { font-family: 'Aref Ruqaa', serif; font-size: 32px; color: #1e293b; margin-bottom: 2px; }
        .title { color: #334155; font-size: 34px; font-weight: 900; margin-bottom: 2px; }
        .subtitle { color: #475569; font-size: 18px; margin-bottom: 12px; }
        
        .student { font-size: 38px; font-weight: 900; color: #0f172a; border-bottom: 3px solid #334155; display: inline-block; padding-bottom: 2px; margin-bottom: 15px; min-width: 320px; }
        
        .text-body { font-size: 17px; color: #1e293b; line-height: 1.6; max-width: 580px; margin: 0 auto; font-weight: 700; }
        .highlight { color: #b45309; font-weight: 900; font-size: 19px; }
        
        .controls { margin-top: 25px; display: flex; gap: 15px; justify-content: center; flex-wrap: wrap; }
        .btn { padding: 14px 30px; font-size: 18px; font-family: 'Cairo', sans-serif; font-weight: bold; border: none; border-radius: 10px; cursor: pointer; color: #fff; background: linear-gradient(135deg, #2563eb, #1d4ed8); box-shadow: 0 6px 20px rgba(37,99,235,0.4); transition: 0.2s; }
        .btn:hover { transform: scale(1.05); }
        .btn-download { background: linear-gradient(135deg, #059669, #047857); box-shadow: 0 6px 20px rgba(5,150,105,0.4); }

        @media print {
            body { background: none; padding: 0; }
            .portal-search-box, .controls { display: none !important; }
            .certificate { box-shadow: none; border: 4px solid #475569 !important; margin: 0 auto; }
        }
    </style>
</head>
<body>

    <div id="notification-box"></div>

    <div class="portal-search-box">
        <h2>🎓 بوابة طلاب موقع النصيحة التعليمي - الشهادات التفاعلية</h2>
        <p>اكتب اسمك الثلاثي أدناه لتظهر شهادتك التفاعلية الفورية مع معدلك وعلامتك:</p>
        
        <div class="search-input-group">
            <div style="position: relative; flex: 1; max-width: 480px;">
                <input type="text" id="student-search-input" class="search-input" placeholder="🔍 اكتب اسمك هنا (مثال: ابراهيم فواز...)" oninput="filterStudents(this.value)">
                <div id="suggestions-box" class="suggestions-list"></div>
            </div>
            <button class="btn" onclick="searchStudentDirect()" style="padding: 14px 28px; font-size: 16px;">بحث عن شهادتي</button>
        </div>
    </div>

    <div class="certificate" id="cert-container">
        <div class="pattern-top"></div>
        <div class="pattern-bottom"></div>
        <div class="side-bar"></div>

        <!-- صورة الطالب التفاعلية -->
        <div class="photo-container" onclick="document.getElementById('img-upload').click()" title="انقر لإضافة صورتك الشخصية">
            <div id="img-text" class="hint-text">🏅<br>اضغط هنا<br>لإضافة صورتك</div>
            <img id="student-img" src="" alt="صورة الطالب">
        </div>
        <input type="file" id="img-upload" accept="image/*" style="display: none;" onchange="loadImg(event)">

        <div class="content">
            <div class="header">
                <!-- التاريخ -->
                <div class="date-box">
                    <div class="date-val">2025/8/21</div>
                    <div class="date-lbl">التاريخ</div>
                </div>
                
                <!-- شعار موقع النصيحة -->
                <div class="brand">
                    <div class="logo-svg-box">
                        <svg viewBox="0 0 320 100" xmlns="http://www.w3.org/2000/svg">
                            <defs>
                                <style>
                                    .logo-text {
                                        font-family: 'Cairo', 'Arial Black', sans-serif;
                                        font-weight: 900;
                                    }
                                </style>
                            </defs>
                            <text x="-0.8" y="45" class="logo-text" font-size="30" fill="#00287a" text-anchor="end">التعليمي</text>
                            <g transform="translate(130, 8)">
                                <rect x="10" y="0" width="150" height="58" rx="4" fill="#efa31a" />
                                <text x="82.5" y="40" class="logo-text" font-size="34" fill="#00287a" text-anchor="middle">النصيحة</text>
                                <rect x="10" y="65" width="150" height="3" fill="#efa31a" />
                                <rect x="10" y="71" width="150" height="3" fill="#efa31a" />
                                <rect x="10" y="77" width="150" height="3" fill="#efa31a" />
                            </g>
                        </svg>
                    </div>
                    <div class="teacher">الأستاذ: ثامر قدورة</div>
                </div>
            </div>

            <div class="center-group">
                <div class="basmala">بسم الله الرحمن الرحيم</div>
                <div class="title">شهادة شكر وتقدير</div>
                <div class="subtitle">يسر موقع النصيحة التعليمي منح هذه الشهادة إلى:</div>
                
                <div class="student" id="display-name">ابراهيم فواز الزعبي</div>

                <div class="text-body">
                    وذلك تقديراً لجهوده المضنية في مرحلة الثانوية العامة، وحصوله<br>
                    على معدل <span class="highlight" id="display-avg">95.35</span> ، وعلامة <span class="highlight" id="display-mark">200/200</span> في مادة الرياضيات.<br>
                    نبارك هذا الإنجاز، ونتمنى لك مزيداً من النجاح في قادمات الأيام.
                </div>
            </div>
        </div>
    </div>

    <div class="controls" id="controls">
        <button class="btn" onclick="startGraduationCelebration()">🎓 احتفال التفوق والتخرج! 🎈</button>
        <button class="btn btn-download" onclick="downloadCertificate()">📥 تنزيل شهادتي كصورة</button>
    </div>

    <script>
        // =========================================================================
        // 👇👇 ضع رابط الـ CSV الخاص بملف Google Sheet هنا تماماً بين الإشارتين "" 👇👇
        // =========================================================================
        const GOOGLE_SHEET_CSV_URL = "https://docs.google.com/spreadsheets/d/e/2PACX-1vQWnudeiz5jn48RH_rjBV_zDPyl_LZXbbhqe0iXY-f25Uhww1T85PYIJs1OGTgqgXMHxiPS3uxZ4szW/pub?output=csv"; 

        // بيانات افتراضية تجريبية احتياطية (تعمل في حال عدم ربط الرابط بعد)
        let studentsDatabase = [
            {name: "ابراهيم فواز الزعبي", avg: "95.35", mark: "200/200"},
            {name: "محمد أحمد الكفاوين", avg: "97.40", mark: "200/200"},
            {name: "أحمد خالد العمري", avg: "98.10", mark: "200/200"}
        ];

        function showNotification(message) {
            const box = document.getElementById('notification-box');
            box.innerText = message;
            box.classList.add('show');
            setTimeout(() => {
                box.classList.remove('show');
            }, 2500);
        }

        // جلب البيانات تلقائياً وبشكل صامت من Google Sheet في الخلفية
        function fetchStudentDataFromCloud() {
            if (!GOOGLE_SHEET_CSV_URL) return;
            
            fetch(GOOGLE_SHEET_CSV_URL)
                .then(response => response.text())
                .then(csvText => {
                    const lines = csvText.split('\n');
                    let newDb = [];
                    lines.forEach(line => {
                        const parts = line.split(',');
                        if (parts.length >= 2) {
                            const name = parts[0].replace(/"/g, '').trim();
                            if (name && name !== "الاسم" && name !== "Name" && name !== "اسم الطالب") {
                                newDb.push({
                                    name: name,
                                    avg: parts[1] ? parts[1].replace(/"/g, '').trim() : "95.00",
                                    mark: parts[2] ? parts[2].replace(/"/g, '').trim() : "200/200"
                                });
                            }
                        }
                    });

                    if (newDb.length > 0) {
                        studentsDatabase = newDb;
                    }
                })
                .catch(err => {
                    // صامت تماماً في الخلفية
                });
        }

        function filterStudents(query) {
            const box = document.getElementById('suggestions-box');
            box.innerHTML = '';
            if (!query.trim()) {
                box.style.display = 'none';
                return;
            }

            const matches = studentsDatabase.filter(st => st.name.includes(query.trim()));
            if (matches.length === 0) {
                box.style.display = 'none';
                return;
            }

            matches.forEach(st => {
                const div = document.createElement('div');
                div.className = 'suggestion-item';
                div.innerText = `${st.name} (معدل: ${st.avg})`;
                div.onclick = () => {
                    selectStudent(st);
                };
                box.appendChild(div);
            });
            box.style.display = 'block';
        }

        function selectStudent(st) {
            document.getElementById('student-search-input').value = st.name;
            document.getElementById('suggestions-box').style.display = 'none';
            document.getElementById('display-name').innerText = st.name;
            document.getElementById('display-avg').innerText = st.avg;
            document.getElementById('display-mark').innerText = st.mark;
            showNotification(`🎯 أهلاً بك يا بطل: ${st.name}`);
        }

        function searchStudentDirect() {
            const query = document.getElementById('student-search-input').value.trim();
            const found = studentsDatabase.find(st => st.name === query || st.name.includes(query));
            if (found) {
                selectStudent(found);
            } else {
                showNotification('⚠️ لم يتم العثور على الاسم. تأكد من كتابة اسمك الثلاثي بدقة.');
            }
        }

        function loadImg(event) {
            const img = document.getElementById('student-img');
            const text = document.getElementById('img-text');
            if(event.target.files && event.target.files[0]) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    img.src = e.target.result;
                    img.style.display = 'block';
                    text.style.display = 'none';
                    showNotification("📷 تم إرفاق صورتك الشخصية بنجاح!");
                };
                reader.readAsDataURL(event.target.files[0]);
            }
        }

        function downloadCertificate() {
            const cert = document.getElementById('cert-container');
            const studentName = document.getElementById('display-name').innerText;
            showNotification("⏳ جاري تجهيز وتنزيل شهادتك كصورة...");
            html2canvas(cert, { scale: 2, useCORS: true, allowTaint: true }).then(canvas => {
                const link = document.createElement('a');
                link.download = `شهادة_تفوق_${studentName}.png`;
                link.href = canvas.toDataURL('image/png');
                link.click();
                showNotification("✅ تم تنزيل الشهادة بنجاح مبارك!");
            });
        }

        function startGraduationCelebration() {
            const celebrationElements = ['🎓', '🎈', '🎉', '⭐️', '🌟', '🎊', '✨', '🎈'];
            for (let i = 0; i < 90; i++) {
                const el = document.createElement('div');
                el.innerHTML = celebrationElements[Math.floor(Math.random() * celebrationElements.length)];
                el.style.position = 'fixed';
                el.style.left = Math.random() * 100 + 'vw';
                el.style.top = '-50px';
                el.style.fontSize = (Math.random() * 25 + 18) + 'px';
                el.style.zIndex = '9999';
                el.style.pointerEvents = 'none';
                
                document.body.appendChild(el);
                
                const duration = Math.random() * 3000 + 2500;
                const animation = el.animate([
                    { transform: 'translateY(0) rotate(0deg)', opacity: 1 },
                    { transform: `translateY(105vh) translateX(${Math.random() * 300 - 150}px) rotate(${Math.random() * 720 - 360}deg)`, opacity: 0 }
                ], {
                    duration: duration,
                    easing: 'ease-out'
                });
                
                animation.onfinish = () => el.remove();
            }
            showNotification("🎉 ألف مبروك التفوق والتخرج!");
        }

        window.onload = function() {
            fetchStudentDataFromCloud();
        };
    </script>
</body>
</html>
