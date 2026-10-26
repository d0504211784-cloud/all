<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>מערכת פרימיום לניהול תיקים ויעדים</title>
    <!-- אייקונים מודרניים של FontAwesome לכל הרכיבים -->
    <link rel="stylesheet" href="https://cloudflare.com">
    
    <style>
        /* משתני מערכת ועיצוב דינמי (Light Mode כברירת מחדל) */
        :root {
            --bg-gradient: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            --card-bg: rgba(255, 255, 255, 0.8);
            --card-border: rgba(255, 255, 255, 0.45);
            --primary: #3498db;
            --success: #2ecc71;
            --danger: #e74c3c;
            --excel: #27ae60;
            --warning: #f39c12;
            --text-main: #2c3e50;
            --text-muted: #7f8c8d;
            --shadow-float: 0 15px 35px rgba(0, 0, 0, 0.06);
            --radius-lg: 24px;
            --radius-md: 16px;
            --radius-sm: 8px;
        }

        /* הגדרות צבעים ייעודיות למצב לילה (Dark Mode) */
        body.dark-mode {
            --bg-gradient: linear-gradient(135deg, #0f172a 0%, #1e293b 100%);
            --card-bg: rgba(30, 41, 59, 0.7);
            --card-border: rgba(255, 255, 255, 0.08);
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --shadow-float: 0 20px 40px rgba(0, 0, 0, 0.3);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            transition: background 0.2s ease, color 0.2s ease, border-color 0.2s ease;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: var(--bg-gradient);
            min-height: 100vh;
            padding: 40px 20px;
            color: var(--text-main);
        }
        .app-header {
            text-align: center;
            margin-bottom: 25px;
        }

        .app-header h1 {
            font-size: 2.5rem;
            color: #1e3c72;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
            margin-bottom: 8px;
        }
        body.dark-mode .app-header h1 { color: #38bdf8; }

        .app-header p {
            color: var(--text-muted);
            font-size: 1.1rem;
        }

        /* סרגל כפתורי ניהול עליון */
        .action-bar {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-bottom: 35px;
        }

        .btn-top {
            padding: 12px 24px;
            border: none;
            border-radius: 30px;
            font-size: 0.95rem;
            font-weight: bold;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 10px;
            color: #ffffff;
        }

        .btn-excel {
            background: var(--excel);
            box-shadow: 0 5px 15px rgba(39, 174, 96, 0.3);
        }
        .btn-excel:hover {
            background: #219653;
            transform: translateY(-2px);
        }

        .btn-theme {
            background: #475569;
            box-shadow: 0 5px 15px rgba(71, 85, 105, 0.3);
        }
        .btn-theme:hover {
            background: #334155;
            transform: translateY(-2px);
        }
        /* לוח מנהלים עליון (Dashboard Widgets) */
        .manager-dashboard {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
            max-width: 1440px;
            margin: 0 auto 40px auto;
        }

        .widget-card {
            background: var(--card-bg);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border-radius: var(--radius-md);
            border: 1px solid var(--card-border);
            box-shadow: var(--shadow-float);
            padding: 20px;
            display: flex;
            align-items: center;
            gap: 20px;
        }

        .widget-icon {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            color: #ffffff;
        }

        .widget-info {
            display: flex;
            flex-direction: column;
            gap: 4px;
        }

        .widget-title {
            font-size: 0.85rem;
            color: var(--text-muted);
            font-weight: 600;
        }

        .widget-value {
            font-size: 1.5rem;
            font-weight: bold;
        }

        .bg-blue { background: #3498db; box-shadow: 0 4px 10px rgba(52, 152, 219, 0.3); }
        .bg-green { background: #2ecc71; box-shadow: 0 4px 10px rgba(46, 204, 113, 0.3); }
        .bg-purple { background: #9b59b6; box-shadow: 0 4px 10px rgba(155, 89, 182, 0.3); }
        /* גריד וכרטיסי יועצים */
        .container {
            max-width: 1440px;
            margin: 0 auto;
        }

        .advisors-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(380px, 1fr));
            gap: 30px;
        }

        .advisor-card {
            background: var(--card-bg);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border-radius: var(--radius-lg);
            border: 1px solid var(--card-border);
            box-shadow: var(--shadow-float);
            padding: 30px;
            display: flex;
            flex-direction: column;
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 2px solid rgba(0, 0, 0, 0.04);
            padding-bottom: 18px;
            margin-bottom: 15px;
        }

        .card-header h2 {
            font-size: 1.6rem;
            display: flex;
            align-items: center;
            gap: 12px;
            color: var(--text-main);
        }

        .icon-yaakov { color: #3498db; }
        .icon-doron { color: #9b59b6; }
        .icon-aviv { color: #1abc9c; }

        .goal-input-group {
            display: flex;
            align-items: center;
            gap: 8px;
            background: rgba(0, 0, 0, 0.04);
            padding: 6px 14px;
            border-radius: 30px;
        }

        .target-input {
            border: none;
            background: transparent;
            font-size: 1.05rem;
            font-weight: bold;
            color: var(--text-main);
            width: 85px;
            outline: none;
            text-align: center;
        }

        /* פסי התקדמות דינמיים באחוזים */
        .progress-container {
            margin-bottom: 20px;
            background: rgba(0, 0, 0, 0.05);
            border-radius: 10px;
            height: 18px;
            position: relative;
            overflow: hidden;
            display: flex;
            align-items: center;
        }

        .progress-bar {
            background: linear-gradient(90deg, #3498db, #2980b9);
            height: 100%;
            width: 0%;
            transition: width 0.4s ease, background 0.3s;
        }

        .progress-bar.completed {
            background: linear-gradient(90deg, #2ecc71, #27ae60);
        }

        .progress-text {
            position: absolute;
            width: 100%;
            text-align: center;
            font-size: 0.75rem;
            font-weight: bold;
            color: var(--text-main);
            z-index: 2;
        }
        .card-summary {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 14px;
            margin-bottom: 25px;
        }

        .stat-box {
            background: rgba(255, 255, 255, 0.4);
            padding: 14px;
            border-radius: var(--radius-md);
            border: 1px solid rgba(0, 0, 0, 0.02);
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 6px;
        }
        body.dark-mode .stat-box { background: rgba(255, 255, 255, 0.03); }

        .stat-label {
            font-size: 0.8rem;
            color: var(--text-muted);
            display: flex;
            align-items: center;
            gap: 6px;
            font-weight: 500;
        }

        .stat-value {
            font-size: 1.25rem;
            font-weight: bold;
        }

        .status-box-amount { background: rgba(52, 152, 219, 0.08); color: #2980b9; }
        .status-box-remaining { background: rgba(230, 126, 34, 0.08); color: #d35400; }
        .status-box-remaining.goal-reached {
            background: rgba(46, 204, 113, 0.15) !important;
            color: #27ae60 !important;
        }

        /* רשימת התיקים וכרטיסי תיק פנימיים */
        .cases-container {
            max-height: 420px;
            overflow-y: auto;
            margin-bottom: 25px;
            padding-left: 5px;
        }

        .cases-container::-webkit-scrollbar { width: 6px; }
        .cases-container::-webkit-scrollbar-thumb { background: rgba(0, 0, 0, 0.1); border-radius: 10px; }

        .case-item {
            background: #ffffff;
            border-radius: var(--radius-md);
            margin-bottom: 15px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.015);
            border: 1px solid rgba(0,0,0,0.03);
            position: relative;
            overflow: hidden;
        }
        body.dark-mode .case-item { background: #1e293b; }

        .case-collapsed-view {
            padding: 16px;
            padding-left: 75px;
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-weight: bold;
            transition: background 0.2s;
        }
        .case-collapsed-view:hover { background: rgba(0, 0, 0, 0.02); }

        .case-collapsed-title {
            display: flex;
            align-items: center;
            gap: 10px;
            color: var(--text-main);
            max-width: 60%;
        }

        .case-collapsed-price {
            color: var(--primary);
        }
        .case-form-content {
            padding: 16px;
            border-top: 1px solid rgba(0,0,0,0.05);
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 12px;
            background: rgba(0, 0, 0, 0.01);
        }

        .case-field {
            display: flex;
            flex-direction: column;
            gap: 5px;
        }

        .case-field.full-width {
            grid-column: span 2;
        }

        .case-field label {
            font-size: 0.75rem;
            color: var(--text-muted);
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .case-item input, .case-item select {
            width: 100%;
            padding: 8px 12px;
            border: 1px solid #e1e8ed;
            border-radius: 8px;
            font-size: 0.9rem;
            outline: none;
            color: var(--text-main);
            background: #ffffff;
        }
        body.dark-mode .case-item input, body.dark-mode .case-item select {
            border-color: #334155;
            background: #0f172a;
        }

        .case-item input:focus, .case-item select:focus {
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.15);
        }

        .btn-save-box {
            grid-column: span 2;
            padding: 10px;
            background: rgba(0, 0, 0, 0.04);
            color: var(--text-main);
            border: 1px solid rgba(0,0,0,0.05);
            border-radius: 8px;
            font-size: 0.85rem;
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        body.dark-mode .btn-save-box {
            background: rgba(255, 255, 255, 0.05);
        }

        /* 🛠️ תיקון קריטי: העלאת הכפתורים לקדמת המסך ומניעת חסימה */
        .case-actions-group {
            position: absolute;
            top: 13px;
            left: 10px;
            display: flex;
            gap: 12px;
            z-index: 20; /* שכבה עליונה ביותר מעל אזור הלחיצה המקוצר */
        }

        .btn-action-icon {
            background: transparent;
            border: none;
            cursor: pointer;
            font-size: 1rem;
            transition: transform 0.2s, color 0.2s;
            color: var(--text-muted);
            padding: 4px;
        }
        .btn-clone:hover { color: var(--primary); transform: scale(1.15); }
        .btn-delete:hover { color: var(--danger); transform: scale(1.15); }

        .btn-add-case {
            width: 100%;
            padding: 14px;
            background: var(--primary);
            color: #ffffff;
            border: none;
            border-radius: var(--radius-md);
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            margin-top: auto;
            box-shadow: 0 5px 15px rgba(52, 152, 219, 0.25);
        }
        .btn-add-case:hover { background: #2980b9; }

        @media (max-width: 480px) {
            .advisors-grid { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>

    <header class="app-header">
        <h1><i class="fa-solid fa-wallet"></i> דאשבורד ניהול תיקים פיננסיים</h1>
        <p>מעקב יעדים והפניות בזמן אמת - שמירה אוטומטית בדפדפן</p>
    </header>

    <div class="action-bar">
        <button class="btn-top btn-excel" onclick="exportToExcel()"><i class="fa-solid fa-file-excel"></i> שמירה וייצוא לאקסל</button>
        <button class="btn-top btn-theme" onclick="toggleTheme()"><i class="fa-solid fa-moon"></i> מצב לילה / בהיר</button>
    </div>

    <!-- לוח מנהלים עליון (Dashboard Widgets) -->
    <div class="manager-dashboard">
        <div class="widget-card">
            <div class="widget-icon bg-blue"><i class="fa-solid fa-folder-tree"></i></div>
            <div class="widget-info">
                <span class="widget-title">סך הכל תיקים פעילים בחברה</span>
                <span class="widget-value" id="global-active-count">0</span>
            </div>
        </div>
        <div class="widget-card">
            <div class="widget-icon bg-green"><i class="fa-solid fa-money-bill-trend-up"></i></div>
            <div class="widget-info">
                <span class="widget-title">סך הכנסה מצטברת במשרד</span>
                <span class="widget-value" id="global-total-amount">₪0</span>
            </div>
        </div>
        <div class="widget-card">
            <div class="widget-icon bg-purple"><i class="fa-solid fa-chart-line"></i></div>
            <div class="widget-info">
                <span class="widget-title">אחוז עמידה ביעדים כללי</span>
                <span class="widget-value" id="global-progress-percent">0%</span>
            </div>
        </div>
    </div>

    <main class="container">
        <div class="advisors-grid">
            <!-- כרטיס יועץ: יעקב -->
            <section class="advisor-card" id="advisor-yaakov">
                <div class="card-header">
                    <h2><i class="fa-solid fa-user-tie icon-yaakov"></i> יעקב</h2>
                    <div class="goal-input-group">
                        <label><i class="fa-solid fa-bullseye"></i> יעד חודשי:</label>
                        <input type="number" class="target-input" value="100000" oninput="updateStats('yaakov')">
                    </div>
                </div>
                
                <div class="progress-container">
                    <div class="progress-bar" id="progress-yaakov"></div>
                    <span class="progress-text" id="progress-text-yaakov">0%</span>
                </div>
                
                <div class="card-summary">
                    <div class="stat-box"><span class="stat-label"><i class="fa-solid fa-folder-open"></i> תיקים פעילים</span><span class="stat-value active-count">0</span></div>
                    <div class="stat-box"><span class="stat-label"><i class="fa-solid fa-folder-minus"></i> לא פעילים</span><span class="stat-value inactive-count">0</span></div>
                    <div class="stat-box status-box-amount"><span class="stat-label"><i class="fa-solid fa-coins"></i> סכום מצטבר</span><span class="stat-value total-amount">₪0</span></div>
                    <div class="stat-box status-box-remaining"><span class="stat-label"><i class="fa-solid fa-hourglass-half"></i> נותר ליעד</span><span class="stat-value remaining-amount">₪0</span></div>
                </div>

                <div class="cases-container" id="cases-yaakov"></div>
                <button class="btn-add-case" onclick="createNewCase('yaakov')"><i class="fa-solid fa-plus"></i> הוספת תיק חדש</button>
            </section>

            <!-- כרטיס יועץ: דורון -->
            <section class="advisor-card" id="advisor-doron">
                <div class="card-header">
                    <h2><i class="fa-solid fa-user-tie icon-doron"></i> דורון</h2>
                    <div class="goal-input-group">
                        <label><i class="fa-solid fa-bullseye"></i> יעד חודשי:</label>
                        <input type="number" class="target-input" value="120000" oninput="updateStats('doron')">
                    </div>
                </div>
                
                <div class="progress-container">
                    <div class="progress-bar" id="progress-doron"></div>
                    <span class="progress-text" id="progress-text-doron">0%</span>
                </div>
                
                <div class="card-summary">
                    <div class="stat-box"><span class="stat-label"><i class="fa-solid fa-folder-open"></i> תיקים פעילים</span><span class="stat-value active-count">0</span></div>
                    <div class="stat-box"><span class="stat-label"><i class="fa-solid fa-folder-minus"></i> לא פעילים</span><span class="stat-value inactive-count">0</span></div>
                    <div class="stat-box status-box-amount"><span class="stat-label"><i class="fa-solid fa-coins"></i> סכום מצטבר</span><span class="stat-value total-amount">₪0</span></div>
                    <div class="stat-box status-box-remaining"><span class="stat-label"><i class="fa-solid fa-hourglass-half"></i> נותר ליעד</span><span class="stat-value remaining-amount">₪0</span></div>
                </div>

                <div class="cases-container" id="cases-doron"></div>
                <button class="btn-add-case" onclick="createNewCase('doron')"><i class="fa-solid fa-plus"></i> הוספת תיק חדש</button>
            </section>

            <!-- כרטיס יועץ: אביב -->
            <section class="advisor-card" id="advisor-aviv">
                <div class="card-header">
                    <h2><i class="fa-solid fa-user-tie icon-aviv"></i> אביב</h2>
                    <div class="goal-input-group">
                        <label><i class="fa-solid fa-bullseye"></i> יעד חודשי:</label>
                        <input type="number" class="target-input" value="90000" oninput="updateStats('aviv')">
                    </div>
                </div>
                
                <div class="progress-container">
                    <div class="progress-bar" id="progress-aviv"></div>
                    <span class="progress-text" id="progress-text-aviv">0%</span>
                </div>
                
                <div class="card-summary">
                    <div class="stat-box"><span class="stat-label"><i class="fa-solid fa-folder-open"></i> תיקים פעילים</span><span class="stat-value active-count">0</span></div>
                    <div class="stat-box"><span class="stat-label"><i class="fa-solid fa-folder-minus"></i> לא פעילים</span><span class="stat-value inactive-count">0</span></div>
                    <div class="stat-box status-box-amount"><span class="stat-label"><i class="fa-solid fa-coins"></i> סכום מצטבר</span><span class="stat-value total-amount">₪0</span></div>
                    <div class="stat-box status-box-remaining"><span class="stat-label"><i class="fa-solid fa-hourglass-half"></i> נותר ליעד</span><span class="stat-value remaining-amount">₪0</span></div>
                </div>

                <div class="cases-container" id="cases-aviv"></div>
                <button class="btn-add-case" onclick="createNewCase('aviv')"><i class="fa-solid fa-plus"></i> הוספת תיק חדש</button>
            </section>

        </div>
    </main>

    <script>
        const ADVISORS = ['yaakov', 'doron', 'aviv'];
        const STORAGE_KEY = 'v8_final_premium_data';

        document.addEventListener('DOMContentLoaded', () => {
            loadData();
            if (localStorage.getItem('premium_theme') === 'dark') {
                document.body.classList.add('dark-mode');
            }
        });
        /**
         * יצירת כרטיס תיק פנימי חדש (Accordion)
         */
        function createNewCase(advisorId, data = null) {
            const container = document.getElementById(`cases-${advisorId}`);
            if (!container) return;

            const caseDiv = document.createElement('div');
            caseDiv.className = 'case-item';
            
            const values = {
                name: data ? data.name : '',
                status: data ? data.status : 'פעיל',
                price: data ? data.price : 0,
                insurance: data ? data.insurance : 'לא',
                agentName: data ? data.agentName : '',
                appraisal: data ? data.appraisal : 'לא',
                appraiserName: data ? data.appraiserName : '',
                source: data ? data.source : '',
                isCollapsed: data ? (data.isCollapsed !== false) : false
            };

            caseDiv.innerHTML = `
                <!-- קבוצת לחצני ניהול העומדים בטופ היררכיית הלחיצה -->
                <div class="case-actions-group">
                    <button class="btn-action-icon btn-clone" onclick="cloneCase('${advisorId}', this); event.stopPropagation();" title="שכפל תיק">
                        <i class="fa-solid fa-copy"></i>
                    </button>
                    <button class="btn-action-icon btn-delete" onclick="removeCase('${advisorId}', this); event.stopPropagation();" title="מחק תיק">
                        <i class="fa-solid fa-trash-can"></i>
                    </button>
                </div>

                <!-- תצוגה מקוצרת ונקייה כשהתיק סגור -->
                <div class="case-collapsed-view" onclick="toggleCaseView(this)">
                    <div class="case-collapsed-title">
                        <i class="fa-solid fa-chevron-down toggle-icon"></i>
                        <span class="collapsed-name-text">${values.name || 'לקוח חדש'}</span>
                    </div>
                    <div class="case-collapsed-price">
                        <span class="collapsed-price-text">₪${Number(values.price).toLocaleString()}</span>
                    </div>
                </div>
                <!-- טופס נתונים פנימי מלא ונפתח -->
                <div class="case-form-content" style="display: ${values.isCollapsed ? 'none' : 'grid'};">
                    <div class="case-field full-width">
                        <label><i class="fa-solid fa-user"></i> שם הלקוח</label>
                        <input type="text" class="c-name" value="${values.name}" oninput="updateCollapsedLabels(this); saveData();">
                    </div>
                    <div class="case-field">
                        <label><i class="fa-solid fa-circle-info"></i> סטטוס</label>
                        <select class="c-status" onchange="updateStats('${advisorId}')">
                            <option value="פעיל" ${values.status === 'פעיל' ? 'selected' : ''}>פעיל</option>
                            <option value="לא פעיל" ${values.status === 'לא פעיל' ? 'selected' : ''}>לא פעיל</option>
                        </select>
                    </div>
                    <div class="case-field">
                        <label><i class="fa-solid fa-shekel-sign"></i> סכום התיק</label>
                        <input type="number" class="c-price" value="${values.price}" oninput="updateCollapsedLabels(this); updateStats('${advisorId}');">
                    </div>
                    <div class="case-field">
                        <label><i class="fa-solid fa-shield-halved"></i> הפניית ביטוח</label>
                        <select class="c-ins" onchange="toggleAgentField(this); saveData();">
                            <option value="לא" ${values.insurance === 'לא' ? 'selected' : ''}>לא</option>
                            <option value="כן" ${values.insurance === 'כן' ? 'selected' : ''}>כן</option>
                        </select>
                    </div>
                    <div class="case-field c-agent-field" style="display: ${values.insurance === 'כן' ? 'flex' : 'none'};">
                        <label><i class="fa-solid fa-user-shield"></i> שם סוכן הביטוח</label>
                        <input type="text" class="c-agent-name" value="${values.agentName}" oninput="saveData()">
                    </div>
                    <div class="case-field">
                        <label><i class="fa-solid fa-calculator"></i> הפניית שמאות</label>
                        <select class="c-app" onchange="toggleAppraiserField(this); saveData();">
                            <option value="לא" ${values.appraisal === 'לא' ? 'selected' : ''}>לא</option>
                            <option value="כן" ${values.appraisal === 'כן' ? 'selected' : ''}>כן</option>
                        </select>
                    </div>
                    <div class="case-field c-appraiser-field" style="display: ${values.appraisal === 'כן' ? 'flex' : 'none'};">
                        <label><i class="fa-solid fa-gavel"></i> שם השמאי</label>
                        <input type="text" class="c-appraiser-name" value="${values.appraiserName}" oninput="saveData()">
                    </div>
                    <div class="case-field full-width">
                        <label><i class="fa-solid fa-link"></i> מקור ההפנייה</label>
                        <input type="text" class="c-src" value="${values.source}" oninput="saveData()">
                    </div>
                    <button class="btn-save-box" onclick="collapseCaseBox(this); event.preventDefault();">
                        <i class="fa-solid fa-check"></i> שמור קוביה וסגור תיק
                    </button>
                </div>
            `;

            container.appendChild(caseDiv);
            if (values.isCollapsed) {
                const icon = caseDiv.querySelector('.toggle-icon');
                if (icon) icon.className = 'fa-solid fa-chevron-left toggle-icon';
            }
            updateStats(advisorId);
        }
        /**
         * שכפול מהיר של תיק קיים על כל שדותיו
         */
        function cloneCase(advisorId, buttonElement) {
            const caseItem = buttonElement.closest('.case-item');
            const clonedData = {
                name: caseItem.querySelector('.c-name').value + ' (מועתק)',
                status: caseItem.querySelector('.c-status').value,
                price: parseFloat(caseItem.querySelector('.c-price').value) || 0,
                insurance: caseItem.querySelector('.c-ins').value,
                agentName: caseItem.querySelector('.c-agent-name')?.value || '',
                appraisal: caseItem.querySelector('.c-app').value,
                appraiserName: caseItem.querySelector('.c-appraiser-name')?.value || '',
                source: caseItem.querySelector('.c-src').value,
                isCollapsed: true // התיק המשוכפל ייווצר כשהוא סגור בצורה נקייה
            };
            createNewCase(advisorId, clonedData);
        }

        /**
         * פונקציות לניהול פתיחה וסגירה של כרטיס התיק המתקפל
         */
        function toggleCaseView(collapsedViewElement) {
            const caseItem = collapsedViewElement.closest('.case-item');
            const formContent = caseItem.querySelector('.case-form-content');
            const icon = caseItem.querySelector('.toggle-icon');
            
            if (formContent.style.display === 'none') {
                formContent.style.display = 'grid';
                icon.className = 'fa-solid fa-chevron-down toggle-icon';
            } else {
                formContent.style.display = 'none';
                icon.className = 'fa-solid fa-chevron-left toggle-icon';
            }
            saveData();
        }

        function collapseCaseBox(buttonElement) {
            const caseItem = buttonElement.closest('.case-item');
            const formContent = caseItem.querySelector('.case-form-content');
            const icon = caseItem.querySelector('.toggle-icon');
            
            formContent.style.display = 'none';
            if (icon) icon.className = 'fa-solid fa-chevron-left toggle-icon';
            saveData();
        }

        function updateCollapsedLabels(inputElement) {
            const caseItem = inputElement.closest('.case-item');
            if (inputElement.classList.contains('c-name')) {
                caseItem.querySelector('.collapsed-name-text').textContent = inputElement.value.trim() || 'לקוח חדש';
            }
            if (inputElement.classList.contains('c-price')) {
                const val = parseFloat(inputElement.value) || 0;
                caseItem.querySelector('.collapsed-price-text').textContent = `₪${val.toLocaleString()}`;
            }
        }

        function toggleAppraiserField(selectElement) {
            const item = selectElement.closest('.case-item');
            const fld = item.querySelector('.c-appraiser-field');
            if (fld) fld.style.display = selectElement.value === 'כן' ? 'flex' : 'none';
        }

        function toggleAgentField(selectElement) {
            const item = selectElement.closest('.case-item');
            const fld = item.querySelector('.c-agent-field');
            if (fld) fld.style.display = selectElement.value === 'כן' ? 'flex' : 'none';
        }

        function removeCase(advisorId, button) {
            const item = button.closest('.case-item');
            if (item) {
                item.remove();
                updateStats(advisorId);
            }
        }
        /**
         * עדכון סטטיסטיקות, חישוב פסי התקדמות ועדכון לוח מנהלים עליון
         */
        function updateStats(advisorId) {
            const card = document.getElementById(`advisor-${advisorId}`);
            if (!card) return;

            const items = card.querySelectorAll('.case-item');
            const target = parseFloat(card.querySelector('.target-input').value) || 0;

            let active = 0, inactive = 0, total = 0;

            items.forEach(item => {
                const status = item.querySelector('.c-status').value;
                const price = parseFloat(item.querySelector('.c-price').value) || 0;
                if (status === 'פעיל') { active++; total += price; } else { inactive++; }
            });

            const remaining = Math.max(0, target - total);

            card.querySelector('.active-count').textContent = active;
            card.querySelector('.inactive-count').textContent = inactive;
            card.querySelector('.total-amount').textContent = `₪${total.toLocaleString()}`;
            
            const remElement = card.querySelector('.remaining-amount');
            const remBox = card.querySelector('.status-box-remaining');

            if (total >= target && target > 0) {
                remBox.classList.add('goal-reached');
                remElement.textContent = 'היעד הושג!';
            } else {
                remBox.classList.remove('goal-reached');
                remElement.textContent = `₪${remaining.toLocaleString()}`;
            }

            // חישוב ועדכון מד ההתקדמות הגרפי באחוזים (Progress Bar)
            const percent = target > 0 ? Math.min(100, Math.round((total / target) * 100)) : 0;
            const bar = document.getElementById(`progress-${advisorId}`);
            const text = document.getElementById(`progress-text-${advisorId}`);
            
            if (bar && text) {
                bar.style.width = `${percent}%`;
                text.textContent = `${percent}%`;
                bar.classList.toggle('completed', percent >= 100);
            }

            // עדכון המדדים המשולבים בכל החברה
            updateGlobalDashboard();
            saveData();
        }

        /**
         * חישוב מרוכז ועדכון הנתונים של כל המשרד בלוח המנהלים העליון
         */
        function updateGlobalDashboard() {
            let globalActive = 0;
            let globalTotal = 0;
            let totalTargets = 0;

            ADVISORS.forEach(id => {
                const card = document.getElementById(`advisor-${id}`);
                if (!card) return;

                const target = parseFloat(card.querySelector('.target-input').value) || 0;
                totalTargets += target;

                const items = card.querySelectorAll('.case-item');
                items.forEach(item => {
                    const status = item.querySelector('.c-status').value;
                    const price = parseFloat(item.querySelector('.c-price').value) || 0;
                    if (status === 'פעיל') {
                        globalActive++;
                        globalTotal += price;
                    }
                });
            });

            const globalPercent = totalTargets > 0 ? Math.min(100, Math.round((globalTotal / totalTargets) * 100)) : 0;

            document.getElementById('global-active-count').textContent = globalActive;
            document.getElementById('global-total-amount').textContent = `₪${globalTotal.toLocaleString()}`;
            document.getElementById('global-progress-percent').textContent = `${globalPercent}%`;
        }
        /**
         * מעבר דינמי בין מצב בהיר למצב לילה יוקרתי ושמירת הבחירה
         */
        function toggleTheme() {
            const isDark = document.body.classList.toggle('dark-mode');
            localStorage.setItem('premium_theme', isDark ? 'dark' : 'light');
        }

        /**
         * שמירת כל המידע והסטטוס המעודכן ב-LocalStorage של הדפדפן
         */
        function saveData() {
            const data = {};
            ADVISORS.forEach(id => {
                const card = document.getElementById(`advisor-${id}`);
                if (!card) return;

                const items = card.querySelectorAll('.case-item');
                const cases = Array.from(items).map(item => {
                    const formContent = item.querySelector('.case-form-content');
                    return {
                        name: item.querySelector('.c-name').value,
                        status: item.querySelector('.c-status').value,
                        price: parseFloat(item.querySelector('.c-price').value) || 0,
                        insurance: item.querySelector('.c-ins').value,
                        agentName: item.querySelector('.c-agent-name')?.value || '',
                        appraisal: item.querySelector('.c-app').value,
                        appraiserName: item.querySelector('.c-appraiser-name')?.value || '',
                        source: item.querySelector('.c-src').value,
                        isCollapsed: formContent ? (formContent.style.display === 'none') : false
                    };
                });

                data[id] = {
                    target: card.querySelector('.target-input').value,
                    cases: cases
                };
            });
            localStorage.setItem(STORAGE_KEY, JSON.stringify(data));
        }

        /**
         * טעינת ושחזור הנתונים השמורים בעת פתיחה מחדש של הדף
         */
        function loadData() {
            const raw = localStorage.getItem(STORAGE_KEY);
            if (!raw) {
                ADVISORS.forEach(id => updateStats(id));
                return;
            }
            
            const data = JSON.parse(raw);
            ADVISORS.forEach(id => {
                const card = document.getElementById(`advisor-${id}`);
                if (!card) return;

                if (data[id]) {
                    card.querySelector('.target-input').value = data[id].target;
                    data[id].cases.forEach(c => createNewCase(id, c));
                }
                updateStats(id);
            });
        }

        /**
         * פונקציה לייצוא של כל הנתונים של כל היועצים לקובץ Excel (CSV) תואם עברית
         */
        function exportToExcel() {
            const raw = localStorage.getItem(STORAGE_KEY);
            if (!raw) {
                alert('אין נתונים זמינים לייצוא כרגע.');
                return;
            }

            const data = JSON.parse(raw);
            let csvContent = "יועץ,שם הלקוח,סטטוס,סכום התיק,הפנייה לביטוח,שם סוכן ביטוח,הפנייה לשמאות,שם השמאי,מקור ההפנייה\n";

            const advisorNamesHE = { yaakov: "יעקב", doron: "דורון", aviv: "אביב" };

            ADVISORS.forEach(id => {
                if (data[id] && data[id].cases) {
                    data[id].cases.forEach(c => {
                        const row = [
                            advisorNamesHE[id],
                            `"${c.name.replace(/"/g, '""')}"`,
                            c.status,
                            c.price,
                            c.insurance,
                            `"${c.agentName.replace(/"/g, '""')}"`,
                            c.appraisal,
                            `"${c.appraiserName.replace(/"/g, '""')}"`,
                            `"${c.source.replace(/"/g, '""')}"`
                        ];
                        csvContent += row.join(",") + "\n";
                    });
                }
            });

            // הוספת תו BOM כדי שאקסל יציג עברית בצורה נקייה ותקינה
            const blob = new Blob([new Uint8Array([0xEF, 0xBB, 0xBF]), csvContent], { type: "text/csv;charset=utf-8;" });
            const link = document.createElement("a");
            
            if (link.download !== undefined) {
                const url = URL.createObjectURL(blob);
                link.setAttribute("href", url);
                link.setAttribute("download", "דוח_תיקים_ויעדים_מרוכז.csv");
                link.style.visibility = 'hidden';
                document.body.appendChild(link);
                link.click();
                document.body.removeChild(link);
            }
        }
    </script>
</body>
</html>
