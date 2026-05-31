<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>תסריט שיחה וניהול פניות</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Assistant:wght@300;400;600;800&display=swap');

        :root {
            --bg-color: #FDFBF7;
            --card-bg: #FFFFFF;
            --text-color: #4A4A4A;
            --btn-primary: #B5D5C5; /* Pastel Green */
            --btn-primary-hover: #A0C4B2;
            --btn-secondary: #F3D8C7; /* Pastel Peach */
            --btn-secondary-hover: #E3C5B2;
            --btn-danger: #F4C2C2; /* Pastel Red */
            --btn-danger-hover: #E5AEAE;
            --btn-info: #C5D9E8; /* Pastel Blue */
            --btn-info-hover: #B2C9DA;
        }

        body {
            margin: 0;
            padding: 0;
            font-family: 'Assistant', sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            overflow: hidden;
        }

        .slide-container {
            width: 100%;
            max-width: 900px;
            height: 80vh;
            background: var(--card-bg);
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.05);
            position: relative;
            overflow: hidden;
            display: flex;
            flex-direction: column;
        }

        .slide {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            padding: 40px;
            box-sizing: border-box;
            display: flex;
            flex-direction: column;
            opacity: 0;
            visibility: hidden;
            transition: all 0.4s ease-in-out;
            transform: translateX(20px);
        }

        .slide.active {
            opacity: 1;
            visibility: visible;
            transform: translateX(0);
        }

        h1, h2, h3 {
            color: #2C3E50;
            margin-top: 0;
        }

        h1 {
            font-size: 2.5rem;
            text-align: center;
            margin-bottom: 30px;
        }

        h2 {
            font-size: 2rem;
            margin-bottom: 20px;
            border-bottom: 3px solid var(--btn-primary);
            display: inline-block;
            padding-bottom: 5px;
        }

        p, li {
            font-size: 1.3rem;
            line-height: 1.6;
        }

        .content {
            flex-grow: 1;
            overflow-y: auto;
            padding-right: 10px;
        }

        .buttons-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }

        button {
            font-family: 'Assistant', sans-serif;
            font-size: 1.2rem;
            font-weight: 600;
            padding: 15px 20px;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            transition: transform 0.2s, background-color 0.2s;
            background-color: var(--btn-info);
            color: #333;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
        }

        button:hover {
            transform: translateY(-2px);
            background-color: var(--btn-info-hover);
        }

        button.primary {
            background-color: var(--btn-primary);
        }
        button.primary:hover { background-color: var(--btn-primary-hover); }

        button.secondary {
            background-color: var(--btn-secondary);
        }
        button.secondary:hover { background-color: var(--btn-secondary-hover); }

        button.danger {
            background-color: var(--btn-danger);
        }
        button.danger:hover { background-color: var(--btn-danger-hover); }

        .back-btn {
            position: absolute;
            bottom: 30px;
            right: 40px;
            background-color: #E0E0E0;
            padding: 10px 20px;
            font-size: 1rem;
        }

        .back-btn:hover {
            background-color: #CCCCCC;
        }

        /* Checkbox styling */
        .task-list {
            list-style: none;
            padding: 0;
            margin: 20px 0;
        }

        .task-list li {
            display: flex;
            align-items: center;
            margin-bottom: 15px;
            background: #F9F9F9;
            padding: 10px 15px;
            border-radius: 8px;
        }

        .task-list input[type="checkbox"] {
            width: 24px;
            height: 24px;
            margin-left: 15px;
            accent-color: #8BA898;
            cursor: pointer;
        }

        .input-text {
            width: 100%;
            padding: 15px;
            font-size: 1.2rem;
            font-family: 'Assistant', sans-serif;
            border: 2px solid var(--btn-info);
            border-radius: 10px;
            margin-top: 10px;
            box-sizing: border-box;
        }

    </style>
</head>
<body>

<div class="slide-container">

    <!-- Slide 1: פתיחת שיחה -->
    <div id="slide-start" class="slide active">
        <div class="content" style="display: flex; flex-direction: column; justify-content: center; align-items: center; text-align: center; height: 100%;">
            <h1>ברוכים הבאים למערכת תסריטי שיחה</h1>
            <p>שלום, הגעתם למוקד השירות. מדבר [שם].<br>איך אוכל לעזור לכם היום?</p>
            <button class="primary" style="margin-top: 30px; font-size: 1.5rem;" onclick="goToSlide('slide-menu')">המשך למטרת השיחה</button>
        </div>
    </div>

    <!-- Slide 2: מטרת השיחה (תפריט ראשי) -->
    <div id="slide-menu" class="slide">
        <h2>מטרת השיחה</h2>
        <div class="content">
            <p>בחר את הנושא הרלוונטי לפניית הלקוח:</p>
            <div class="buttons-grid">
                <button class="primary" onclick="goToSlide('slide-new-info')">מידע על תכנית חדשה</button>
                <button class="secondary" onclick="goToSlide('slide-add-child')">הוספת ילד</button>
                <button class="info" onclick="goToSlide('slide-change')">שינוי תכנית</button>
                <button class="danger" onclick="goToSlide('slide-cancel')">ביטול תכנית</button>
                <button class="primary" onclick="goToSlide('slide-details')">פרטי תכנית</button>
                <button class="secondary" onclick="goToSlide('slide-loan-1')">הלוואה</button>
                <button class="info" onclick="goToSlide('slide-forms')">טפסים ואישורים</button>
            </div>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-start')">חזור להתחלה</button>
    </div>

    <!-- 1. מידע על תכנית חדשה -->
    <div id="slide-new-info" class="slide">
        <h2>התכנית "חוסכים ברוגע"</h2>
        <div class="content">
            <ul style="font-size: 1.4rem;">
                <li><strong>גילאים:</strong> מתאים לילדים עד גיל 4 - מ-16 שנות המתנה ומעלה.</li>
                <li><strong>הפקדה:</strong> אחידה לכל המשפחה - 280 ש"ח על כל 100 א"ש.</li>
                <li><strong>אחוז הפקדה:</strong> 60% הפקדה.</li>
                <li><strong>החזר הלוואה:</strong> בין 181 ל-222 חודשי החזר הלוואה (תלוי בשנות ההמתנה להלוואה הראשונה).</li>
                <li><strong>פריסה:</strong> החזר בפריסת משכנתא.</li>
            </ul>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-menu')">חזור לתפריט</button>
    </div>

    <!-- 2. הוספת ילד (תפריט מסלולים) -->
    <div id="slide-add-child" class="slide">
        <h2>הוספת ילד - בחירת מסלול</h2>
        <div class="content">
            <p>באיזה מסלול תרצו להוסיף את הילד?</p>
            <div class="buttons-grid">
                <button class="primary" onclick="goToSlide('slide-add-track1')">1. אהבת חסד</button>
                <button class="secondary" onclick="goToSlide('slide-add-family')">2. משפחתי</button>
                <button class="info" onclick="goToSlide('slide-add-individual')">3. יחידני</button>
            </div>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-menu')">חזור לתפריט</button>
    </div>

    <!-- 2.1 אהבת חסד -->
    <div id="slide-add-track1" class="slide">
        <h2>הוספת ילד - אהבת חסד</h2>
        <div class="content">
            <p>יש להקריא ללקוח ולוודא הבנה (סמן V לאישור):</p>
            <ul class="task-list">
                <li><input type="checkbox"> <label>אותם תנאים כמו הילדים הקודמים בתכנית.</label></li>
                <li><input type="checkbox"> <label>מהחודש הבא ייגבה X ש"ח נוספים.</label></li>
                <li><input type="checkbox"> <label>2.4% נחלט לקופה כתרומה ולא יוחזר בשום אופן.</label></li>
                <li><input type="checkbox"> <label>החזר ההפקדה יבוצע לאחר פירעון כל ההלוואות בתכנית.</label></li>
            </ul>
            <div class="buttons-grid">
                <button class="primary" onclick="goToSlide('slide-add-yes')">הלקוח רוצה לצרף</button>
                <button class="danger" onclick="goToSlide('slide-add-no')">לא רוצה לצרף כרגע</button>
            </div>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-add-child')">חזור למסלולים</button>
    </div>

    <!-- 2.1.1 רוצה לצרף -->
    <div id="slide-add-yes" class="slide">
        <h2>הוספת ילד - הלקוח מצרף</h2>
        <div class="content">
            <p>פעולות לביצוע כעת (סמן עם השלמת הפעולה):</p>
            <ul class="task-list">
                <li><input type="checkbox"> <label>לצרף הקלטת שיחה לתוך התכנית.</label></li>
                <li><input type="checkbox"> <label>להוסיף את הילד במערכת.</label></li>
                <li><input type="checkbox"> <label>לבדוק שהוקם נכון.</label></li>
                <li><input type="checkbox"> <label>שינוי סטטוס תכנית.</label></li>
            </ul>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-add-child')">חזור למסלולים</button>
    </div>

    <!-- 2.1.2 לא רוצה לצרף -->
    <div id="slide-add-no" class="slide">
        <h2>הוספת ילד - הלקוח לא מצרף כרגע</h2>
        <div class="content">
            <p>שאל את הלקוח:</p>
            <h3>"מתי תרצו שנחזור אליכם שוב?"</h3>
            <input type="text" class="input-text" placeholder="הזן תאריך או הערה לחזרה עתידית...">
            <br><br>
            <button class="primary">שמור משימה וסיים</button>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-add-child')">חזור למסלולים</button>
    </div>

    <!-- 2.2 משפחתי -->
    <div id="slide-add-family" class="slide">
        <h2>הוספת ילד - משפחתי</h2>
        <div class="content">
            <p>מידע ללקוח:</p>
            <ul class="task-list">
                <li><input type="checkbox"> <label>2.4% נחלט לקופה כתרומה ולא יוחזר בשום אופן.</label></li>
                <li><input type="checkbox"> <label>החזר ההפקדה יבוצע לאחר פירעון כל ההלוואות בתכנית.</label></li>
            </ul>
            <div class="buttons-grid">
                <button class="primary" onclick="goToSlide('slide-add-yes')">הלקוח רוצה לצרף</button>
                <button class="danger" onclick="goToSlide('slide-add-no')">לא רוצה לצרף כרגע</button>
            </div>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-add-child')">חזור למסלולים</button>
    </div>

    <!-- 2.3 יחידני -->
    <div id="slide-add-individual" class="slide">
        <h2>הוספת ילד - יחידני</h2>
        <div class="content">
            <p>מידע ללקוח:</p>
            <ul class="task-list">
                <li><input type="checkbox"> <label>2.4% נחלט לקופה כתרומה ולא יוחזר בשום אופן.</label></li>
                <li><input type="checkbox"> <label>החזר ההפקדה יבוצע לאחר פירעון כל הלוואה בנפרד.</label></li>
            </ul>
            <div class="buttons-grid">
                <button class="primary" onclick="goToSlide('slide-add-yes')">הלקוח רוצה לצרף</button>
                <button class="danger" onclick="goToSlide('slide-add-no')">לא רוצה לצרף כרגע</button>
            </div>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-add-child')">חזור למסלולים</button>
    </div>

    <!-- 3. שינוי תכנית -->
    <div id="slide-change" class="slide">
        <h2>שינוי תכנית</h2>
        <div class="content">
            <p>בחר את סוג השינוי המבוקש:</p>
            <div class="buttons-grid">
                <button class="primary" onclick="goToSlide('slide-change-new')">1. מעבר לתכנית חדשה / ביטול קופות</button>
                <button class="secondary" onclick="goToSlide('slide-change-reduce')">2. צמצום</button>
                <button class="info" onclick="goToSlide('slide-change-loan')">3. הלוואה כנגד הסכום שהופקד</button>
            </div>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-menu')">חזור לתפריט</button>
    </div>

    <!-- פירוט שינויים -->
    <div id="slide-change-new" class="slide">
        <h2>מעבר לתכנית חדשה / ביטול קופות</h2>
        <div class="content">
            <ul>
                <li>נדרשת המתנה של לפחות 6 שנים.</li>
                <li><strong>חשוב:</strong> יש לבדוק כדאיות מול הלקוח לפני ביצוע המעבר.</li>
            </ul>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-change')">חזור לשינויים</button>
    </div>

    <div id="slide-change-reduce" class="slide">
        <h2>צמצום תכנית</h2>
        <div class="content">
            <ul>
                <li><strong>שים לב:</strong> יש לעדכן את הלקוח שיכול להיות שאחוזי ההחזר ייפגעו בעקבות הצמצום.</li>
            </ul>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-change')">חזור לשינויים</button>
    </div>

    <div id="slide-change-loan" class="slide">
        <h2>הלוואה כנגד הסכום שכבר הופקד</h2>
        <div class="content">
            <ul>
                <li>במקרה זה, נפתחת תכנית יחידנית חדשה עם לפחות 6 שנים המתנה.</li>
            </ul>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-change')">חזור לשינויים</button>
    </div>

    <!-- 4. ביטול תכנית (תפריט סיבות) -->
    <div id="slide-cancel" class="slide">
        <h2>ביטול תכנית</h2>
        <div class="content">
            <h3>למה רוצים לבטל?</h3>
            <div class="buttons-grid">
                <button class="primary" onclick="goToSlide('slide-cancel-market')">א. שוק ההון</button>
                <button class="secondary" onclick="goToSlide('slide-cancel-temp')">ב. קושי כלכלי זמני</button>
                <button class="danger" onclick="goToSlide('slide-cancel-long')">ג. קושי כלכלי ממושך</button>
            </div>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-menu')">חזור לתפריט</button>
    </div>

    <!-- סיבות ביטול והחלטה -->
    <div id="slide-cancel-market" class="slide">
        <h2>ביטול - שוק ההון</h2>
        <div class="content">
            <p><strong>הסבר ללקוח:</strong> תן הסבר על הפקדה בשוק ההון ואיך אפשר לשלב בצורה חכמה בין הקופה לשוק ההון במקום לבטל לחלוטין.</p>
            <div class="buttons-grid" style="margin-top: 40px;">
                <button class="danger" onclick="goToSlide('slide-cancel-confirm')">בכל זאת רוצה לבטל</button>
                <button class="primary" onclick="goToSlide('slide-cancel-stay')">כרגע נשאר</button>
            </div>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-cancel')">חזור לסיבות</button>
    </div>

    <div id="slide-cancel-temp" class="slide">
        <h2>ביטול - קושי כלכלי זמני</h2>
        <div class="content">
            <p><strong>הסבר ללקוח:</strong> יש אפשרות לדחיית תשלומים של עד חודשיים בשנה, ועד 10 חודשים במהלך כל התכנית. <br>בנוסף, יש אפשרות לבקש אישור מיוחד מההנהלה ליותר מחודשיים דחייה.</p>
            <div class="buttons-grid" style="margin-top: 40px;">
                <button class="danger" onclick="goToSlide('slide-cancel-confirm')">בכל זאת רוצה לבטל</button>
                <button class="primary" onclick="goToSlide('slide-cancel-stay')">כרגע נשאר</button>
            </div>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-cancel')">חזור לסיבות</button>
    </div>

    <div id="slide-cancel-long" class="slide">
        <h2>ביטול - קושי כלכלי ממושך</h2>
        <div class="content">
            <p><strong>הסבר ללקוח:</strong> אולי כדאי לצמצם את התכנית במקום לבטל לגמרי, כדי לא לאבד לחלוטין את הבסיס שנצבר לכל ילד.</p>
            <div class="buttons-grid" style="margin-top: 40px;">
                <button class="danger" onclick="goToSlide('slide-cancel-confirm')">בכל זאת רוצה לבטל</button>
                <button class="primary" onclick="goToSlide('slide-cancel-stay')">כרגע נשאר</button>
            </div>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-cancel')">חזור לסיבות</button>
    </div>

    <!-- אישור ביטול / נשאר -->
    <div id="slide-cancel-confirm" class="slide">
        <h2>הלקוח רוצה לבטל</h2>
        <div class="content">
            <ul class="task-list">
                <li><input type="checkbox"> <label>לעדכן: 2.4% נחלט.</label></li>
                <li><input type="checkbox"> <label>אם אין הקלטת שיחה - יש אפשרות לטופס בקשת החזר.</label></li>
                <li><input type="checkbox"> <label>לבקש מהלקוח לשלוח אישור ניהול חשבון או צילום שיק.</label></li>
            </ul>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-cancel')">חזור אחורה</button>
    </div>

    <div id="slide-cancel-stay" class="slide">
        <h2>הלקוח נשאר</h2>
        <div class="content">
            <p style="font-size: 1.8rem; text-align: center; margin-top: 50px;">
                לומר ללקוח:<br>
                <strong>"אז כרגע התכנית תישאר כך?"</strong>
            </p>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-cancel')">חזור אחורה</button>
    </div>

    <!-- 5. פרטי תכנית -->
    <div id="slide-details" class="slide">
        <h2>פרטי תכנית</h2>
        <div class="content">
            <p><strong>מטרה:</strong></p>
            <ul>
                <li>לעשות ללקוח את ההרגשה שיש לו את התכנית הכי טובה.</li>
                <li>לבדוק ביחד איתו אם יש משהו שניתן לשפר או לייעל עבורו.</li>
            </ul>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-menu')">חזור לתפריט</button>
    </div>

    <!-- 6. הלוואה -->
    <div id="slide-loan-1" class="slide">
        <h2>הלוואה - שלב 1</h2>
        <div class="content">
            <h3>האם יש לכם בן או בת מאורסים?</h3>
            <div class="buttons-grid">
                <button class="danger" onclick="goToSlide('slide-loan-1-no')">לא</button>
                <button class="primary" onclick="goToSlide('slide-loan-2')">כן</button>
            </div>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-menu')">חזור לתפריט</button>
    </div>

    <div id="slide-loan-1-no" class="slide">
        <h2>הלוואה - טרם אירוסין</h2>
        <div class="content">
            <p>במקרה זה הסטטוס דורש בירור מול הנהלה או העברה לייעוץ נהלים בהתאם לתקנון הקופה.</p>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-loan-1')">חזור אחורה</button>
    </div>

    <div id="slide-loan-2" class="slide">
        <h2>הלוואה - שלב 2</h2>
        <div class="content">
            <h3>האם חתמתם על הסכם זכרון דברים מוסדר בנוסח של הקופה?</h3>
            <div class="buttons-grid">
                <button class="danger" onclick="goToSlide('slide-loan-2-no')">לא</button>
                <button class="primary" onclick="goToSlide('slide-loan-3')">כן</button>
            </div>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-loan-1')">חזור אחורה</button>
    </div>

    <div id="slide-loan-2-no" class="slide">
        <h2>הלוואה - ללא זכרון דברים מוסדר</h2>
        <div class="content">
            <p>לומר ללקוח:</p>
            <p><strong>"כרגע זה מאושר, אבל בילדים הבאים לא תהיה אפשרות לכך ללא חתימה מוסדרת."</strong></p>
            <br>
            <button class="primary" onclick="goToSlide('slide-loan-3')">המשך בתהליך</button>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-loan-2')">חזור אחורה</button>
    </div>

    <div id="slide-loan-3" class="slide">
        <h2>הלוואה - שלב 3</h2>
        <div class="content">
            <h3>לצורך מה ההלוואה?</h3>
            <input type="text" class="input-text" placeholder="הזן את מטרת ההלוואה...">
            <br><br>
            <button class="primary" onclick="goToSlide('slide-loan-4')">המשך לתנאי ההלוואה</button>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-loan-2')">חזור אחורה</button>
    </div>

    <div id="slide-loan-4" class="slide">
        <h2>הלוואה - תנאי ההלוואה</h2>
        <div class="content">
            <ul>
                <li>הכסף נכנס ויוצא מחשבון הבנק של הלווה (הילד).</li>
                <li>2.4% מגובה ההלוואות נשאר כתרומה בקופה.</li>
                <li>ביטול קופות לא מקדים את תאריך הזכאות להחזר.</li>
            </ul>
            <hr style="border: 1px solid #eee; margin: 20px 0;">
            <h3>האם לפתוח פנייה?</h3>
            <div class="buttons-grid">
                <button class="primary" onclick="goToSlide('slide-loan-open-yes')">כן</button>
                <button class="secondary" onclick="goToSlide('slide-loan-open-no')">לא</button>
            </div>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-loan-3')">חזור אחורה</button>
    </div>

    <div id="slide-loan-open-yes" class="slide">
        <h2>הלוואה - פתיחת פנייה</h2>
        <div class="content">
            <p style="color: #e74c3c; font-weight: bold;">שים לב: צריך לסיים תוך חודש וחצי את תהליך בקשת ההלוואה.</p>
            <p>פעולות נדרשות:</p>
            <ul class="task-list">
                <li><input type="checkbox"> <label>בקשה ראשונית להלוואה.</label></li>
                <li><input type="checkbox"> <label>צירוף הקלטת שיחה של הנקודות החשובות.</label></li>
                <li><input type="checkbox"> <label>תיעוד בלוג שיחה של תנאי הקדמת ההלוואה.</label></li>
            </ul>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-loan-4')">חזור אחורה</button>
    </div>

    <div id="slide-loan-open-no" class="slide">
        <h2>הלוואה - לא פותחים פנייה</h2>
        <div class="content">
            <p>לומר ללקוח:</p>
            <p style="font-size: 1.5rem; font-weight: bold;">"ההצעה תקפה לחודש, ולאחר מכן תאריך הזכאות מתאפס."</p>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-loan-4')">חזור אחורה</button>
    </div>

    <!-- 7. טפסים ואישורים -->
    <div id="slide-forms" class="slide">
        <h2>טפסים ואישורים</h2>
        <div class="content">
            <p>אזור זה מיועד להורדה, שליחה ומילוי של טפסים ואישורים שונים עבור הלקוח.</p>
        </div>
        <button class="back-btn" onclick="goToSlide('slide-menu')">חזור לתפריט</button>
    </div>

</div>

<script>
    function goToSlide(slideId) {
        // הסר את הקלאס 'active' מכל השקופיות
        const slides = document.querySelectorAll('.slide');
        slides.forEach(slide => {
            slide.classList.remove('active');
        });

        // הוסף את הקלאס 'active' לשקופית המבוקשת
        const targetSlide = document.getElementById(slideId);
        if (targetSlide) {
            targetSlide.classList.add('active');
        }
    }
</script>

</body>
</html>
