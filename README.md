<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>היקף ושטח המעגל עם פיצה!</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 10px; /* מרווח קטן יותר לגוף במסכים קטנים */
            background-color: #fff0e1;
            color: #333;
        }
        .container {
            max-width: 800px;
            margin: auto;
            background-color: #fff;
            padding: 15px; /* מרווח קטן יותר בתוך הקונטיינר במסכים קטנים */
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1); /* צל עדין יותר */
        }
        h1 {
            font-size: 1.8em; /* התאמת גודל כותרת ראשית */
            text-align: center;
            border-bottom: 2px solid #e47200;
            padding-bottom: 10px;
            margin-top: 0;
        }
        h2 { font-size: 1.5em; color: #e47200; }
        h3 { font-size: 1.2em; color: #e47200; }
        
        .pizza-explanation {
            display: flex;
            flex-direction: column; /* ברירת מחדל: עמודה למובייל */
            align-items: center; /* מרכוז הפריטים בעמודה */
            gap: 15px;
            margin-bottom: 20px;
            padding: 10px;
            background-color: #fef9f0;
            border-radius: 8px;
        }
        
        .pizza-svg-container {
            width: 100%; /* תפיסת רוחב מלא זמין */
            max-width: 250px; /* הגבלת גודל מקסימלי של ה-SVG */
            height: auto; /* שמירה על יחס גובה-רוחב */
            flex-shrink: 0;
        }
        .pizza-svg {
            width: 100%;
            height: 100%;
            display: block; /* מונע רווחים מיותרים מתחת ל-SVG */
            margin: 0 auto; /* מרכוז אם יש רוחב עודף */
        }
        .pizza-svg .pizza-base { fill: #FFD700; }
        .pizza-svg .pizza-crust { fill: none; stroke: #8B4513; stroke-width: 10; }
        .pizza-svg .line-radius { stroke: #FF0000; stroke-width: 2; }
        .pizza-svg .line-diameter { stroke: #0000FF; stroke-width: 2; stroke-dasharray: 4,2; }
        .pizza-svg .text-label { font-family: Arial, sans-serif; font-size: 11px; /* גופן מעט קטן יותר למובייל */ font-weight: bold; cursor: help; }
        .pizza-svg .text-radius { fill: #FF0000; }
        .pizza-svg .text-diameter { fill: #0000FF; }
        .pizza-svg .text-circumference { fill: #008000; }
        .pizza-svg .text-area { fill: #FFA500; }
        
        .formula {
            font-weight: bold;
            color: #d63300;
            background-color: #fff8dc;
            padding: 5px;
            border-radius: 5px;
            display: inline-block;
            font-size: 0.9em; /* הקטנת גודל נוסחאות מעט */
        }
        .example, .exercise {
            margin-bottom: 20px;
            padding: 10px;
            background-color: #f9f9f9;
            border: 1px solid #ddd;
            border-radius: 8px;
        }
        .exercise h3 {
            margin-top: 0;
        }
        .options {
            list-style-type: none;
            padding: 0;
        }
        .options li {
            margin-bottom: 8px;
            padding: 10px;
            background-color: #e9ecef;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        .options li:hover {
            background-color: #ced4da;
        }
        .feedback {
            margin-top: 10px;
            padding: 10px;
            border-radius: 5px;
            font-weight: bold;
        }
        .correct {
            background-color: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }
        .incorrect {
            background-color: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }
        .explanation-detail {
            margin-top: 8px;
            font-size: 0.9em;
            border-left: 3px solid #007bff;
            padding-left: 10px;
            background-color: #e7f3ff;
        }
        .pi-value {
            font-style: italic;
            color: #555;
            margin-bottom: 15px;
            text-align: center;
            font-size: 0.9em;
        }

        /* --- Media Queries לרספונסיביות --- */
        @media (min-width: 600px) { /* סגנונות למסכים רחבים יותר (טאבלטים ומחשבים) */
            body {
                padding: 20px;
            }
            .container {
                padding: 25px;
            }
            h1 { font-size: 2.2em; }
            h2 { font-size: 1.8em; }
            h3 { font-size: 1.4em; }

            .pizza-explanation {
                flex-direction: row; /* מחזירים לפריסת שורה */
                align-items: flex-start; /* יישור להתחלה */
                gap: 20px;
            }
            .pizza-svg-container {
                width: 220px; /* גודל קבוע למסכים גדולים יותר */
                max-width: none; /* מבטל את ההגבלה הקודמת */
            }
             .pizza-svg .text-label { font-size: 12px; } /* מחזירים גודל פונט מקורי ב-SVG */
            .formula { font-size: 1em; } /* מחזירים גודל נוסחאות מקורי */
        }

    </style>
</head>
<body>
    <div class="container">
        <h1>🍕 מסע מתמטי טעים: היקף ושטח המעגל עם פיצה! 🍕</h1>

        <p>היי חברים! היום נלמד על מעגלים בצורה הכי טעימה שיש – עם פיצה! מוכנים?</p>

        <h2>מה זה בכלל מעגל? (או: אנטומיה של פיצה)</h2>
        <div class="pizza-explanation">
            <div class="pizza-svg-container">
                <svg class="pizza-svg" viewBox="0 0 220 220" xmlns="http://www.w3.org/2000/svg" preserveAspectRatio="xMidYMid meet">
                    <!-- מרכז האיור יהיה בערך ב-110,110. רדיוס הפיצה 100. -->
                    <circle class="pizza-base" cx="110" cy="110" r="100" />
                    <circle class="pizza-crust" cx="110" cy="110" r="95" />

                    <!-- רדיוס -->
                    <line class="line-radius" x1="110" y1="110" x2="210" y2="110" />
                    <text class="text-label text-radius" x="160" y="105">
                        רדיוס (r)
                        <title>הקו מהמרכז של הפיצה ועד לקצה שלה (לקראסט)</title>
                    </text>

                    <!-- קוטר -->
                    <line class="line-diameter" x1="10" y1="110" x2="210" y2="110" transform="rotate(90 110 110)" /> <!-- סיבוב הקו האופקי -->
                    <text class="text-label text-diameter" x="115" y="60" dominant-baseline="middle" text-anchor="start">
                        קוטר (d)
                        <title>הקו שעובר מקצה לקצה של הפיצה, דרך המרכז. הוא שווה לשני רדיוסים!</title>
                    </text>
                    
                    <!-- היקף -->
                    <text class="text-label text-circumference" x="25" y="30" text-anchor="start">
                        היקף (C)
                        <title>כל הקראסט מסביב לפיצה! אם נפתח אותו, זו תהיה האורך שלו.</title>
                    </text>
                     <path d="M 210,110 A 100,100 0 0 1 178,200" fill="none" stroke="#008000" stroke-width="2" stroke-dasharray="3 3" />
                     <polygon points="178,200 173,195 183,195" fill="#008000" transform="rotate(15,178,200)" />

                    <!-- שטח -->
                    <text class="text-label text-area" x="110" y="170" text-anchor="middle">
                        שטח (A)
                        <title>כל הדבר הטעים שבתוך הקראסט – הגבינה, הרוטב, התוספות! כמה פיצה בעצם אוכלים.</title>
                    </text>
                </svg>
            </div>
            <div>
                <p>דמיינו שהזמנתם פיצה עגולה. בואו נכיר כמה מושגים חשובים:</p>
                <ul>
                    <li><strong>מרכז המעגל:</strong> הנקודה האמצעית המדויקת של הפיצה.</li>
                    <li><strong>רדיוס (r):</strong> המרחק ממרכז הפיצה עד לקצה שלה (לקראסט).</li>
                    <li><strong>קוטר (d):</strong> הקו הישר שעובר מקצה אחד של הפיצה לקצה השני, בדיוק דרך המרכז. הקוטר הוא בעצם פעמיים הרדיוס (<span class="formula">d = 2r</span>).</li>
                    <li><strong>היקף (C):</strong> זה האורך של כל הקראסט מסביב לפיצה. אם היינו "פותחים" את הקראסט ומניחים אותו בקו ישר, זה היה האורך שלו.</li>
                    <li><strong>שטח (A):</strong> זה כל החלק הטעים שבתוך הקראסט – הגבינה, הרוטב, התוספות. בעצם, כמה "משטח" של פיצה אנחנו מקבלים.</li>
                    <li><strong>פאי (π):</strong> זהו מספר קסם במתמטיקה שעוזר לנו לחשב דברים שקשורים למעגלים. הוא בערך <span class="formula">3.14</span>. הוא תמיד אותו דבר, לא משנה כמה הפיצה גדולה או קטנה!</li>
                </ul>
            </div>
        </div>

        <h2>איך מחשבים היקף ושטח של פיצה (מעגל)?</h2>
        <p>כדי לחשב את ההיקף והשטח, נשתמש בנוסחאות הבאות (אל דאגה, זה יותר קל ממה שזה נראה!):</p>
        <ul>
            <li><strong>נוסחה להיקף המעגל (אורך הקראסט):</strong> <span class="formula">היקף = 2 × π × רדיוס</span>  או  <span class="formula">C = 2πr</span></li>
            <li><strong>נוסחה לשטח המעגל (כמה פיצה יש):</strong> <span class="formula">שטח = π × רדיוס × רדיוס</span>  או  <span class="formula">A = πr²</span></li>
        </ul>
        <p class="pi-value">(בכל התרגילים נשתמש בערך מקורב של פאי: π ≈ 3.14)</p>

        <div class="example">
            <h3>דוגמה: פיצה משפחתית טעימה!</h3>
            <p>נניח שהזמנו פיצה שהרדיוס שלה הוא 20 ס"מ.</p>
            <p><strong>1. חישוב היקף הפיצה (אורך הקראסט):</strong></p>
            <p>הנוסחה: <span class="formula">C = 2πr</span></p>
            <p>נציב את המספרים: <span class="formula">C = 2 × 3.14 × 20 ס"מ</span></p>
            <p>חישוב: <span class="formula">C = 6.28 × 20 ס"מ = 125.6 ס"מ</span></p>
            <p><strong>מסקנה:</strong> אורך הקראסט של הפיצה הוא 125.6 ס"מ!</p>

            <p><strong>2. חישוב שטח הפיצה (כמה פיצה נאכל):</strong></p>
            <p>הנוסחה: <span class="formula">A = πr²</span></p>
            <p>נציב את המספרים: <span class="formula">A = 3.14 × (20 ס"מ)²</span></p>
            <p>(שימו לב: קודם כל מעלים את הרדיוס בריבוע: 20 × 20 = 400)</p>
            <p>חישוב: <span class="formula">A = 3.14 × 400 סמ"ר = 1256 סמ"ר</span> (סמ"ר = סנטימטר רבוע, יחידת מידה לשטח)</p>
            <p><strong>מסקנה:</strong> יש לנו 1256 סנטימטר רבוע של פיצה טעימה לאכול!</p>
        </div>

        <h2>יאללה, בואו נתרגל! 🍕📝</h2>
        <p class="pi-value">(זכרו: בכל התרגילים נשתמש בערך מקורב של פאי: π ≈ 3.14)</p>

        <div class="exercise" id="q1">
            <h3>תרגיל 1: פיצה אישית</h3>
            <p>לפיצה אישית יש רדיוס של 10 ס"מ. מה ההיקף שלה?</p>
            <ul class="options">
                <li onclick="checkAnswer(1, 'a', 62.8)">א) 62.8 ס"מ</li>
                <li onclick="checkAnswer(1, 'b', 314)">ב) 314 ס"מ</li>
                <li onclick="checkAnswer(1, 'c', 31.4)">ג) 31.4 ס"מ</li>
                <li onclick="checkAnswer(1, 'd', 100)">ד) 100 ס"מ</li>
            </ul>
            <div class="feedback" id="feedback1"></div>
        </div>

        <div class="exercise" id="q2">
            <h3>תרגיל 2: שטח הפיצה האישית</h3>
            <p>לאותה פיצה אישית עם רדיוס של 10 ס"מ (מתרגיל 1), מה השטח שלה?</p>
            <ul class="options">
                <li onclick="checkAnswer(2, 'a', 62.8)">א) 62.8 סמ"ר</li>
                <li onclick="checkAnswer(2, 'b', 314)">ב) 314 סמ"ר</li>
                <li onclick="checkAnswer(2, 'c', 100)">ג) 100 סמ"ר</li>
                <li onclick="checkAnswer(2, 'd', 31.4)">ד) 31.4 סמ"ר</li>
            </ul>
            <div class="feedback" id="feedback2"></div>
        </div>

        <div class="exercise" id="q3">
            <h3>תרגיל 3: פיצה ענקית!</h3>
            <p>בפיצרייה "המעגל הגדול" מכינים פיצה שהקוטר שלה הוא 60 ס"מ. מה הרדיוס שלה?</p>
            <ul class="options">
                <li onclick="checkAnswer(3, 'a', 60)">א) 60 ס"מ</li>
                <li onclick="checkAnswer(3, 'b', 120)">ב) 120 ס"מ</li>
                <li onclick="checkAnswer(3, 'c', 30)">ג) 30 ס"מ</li>
                <li onclick="checkAnswer(3, 'd', 3.14)">ד) 3.14 ס"מ</li>
            </ul>
            <div class="feedback" id="feedback3"></div>
        </div>
        
        <div class="exercise" id="q4">
            <h3>תרגיל 4: היקף הפיצה הענקית</h3>
            <p>בהמשך לתרגיל 3, לפיצה שהקוטר שלה 60 ס"מ (ולכן הרדיוס שלה 30 ס"מ), מה ההיקף שלה?</p>
            <ul class="options">
                <li onclick="checkAnswer(4, 'a', 94.2)">א) 94.2 ס"מ</li>
                <li onclick="checkAnswer(4, 'b', 188.4)">ב) 188.4 ס"מ</li>
                <li onclick="checkAnswer(4, 'c', 2826)">ג) 2826 ס"מ</li>
                <li onclick="checkAnswer(4, 'd', 60)">ד) 60 ס"מ</li>
            </ul>
            <div class="feedback" id="feedback4"></div>
        </div>

        <div class="exercise" id="q5">
            <h3>תרגיל 5: שטח הפיצה הענקית</h3>
            <p>ועכשיו לשטח של הפיצה הענקית (רדיוס 30 ס"מ). מהו?</p>
            <ul class="options">
                <li onclick="checkAnswer(5, 'a', 188.4)">א) 188.4 סמ"ר</li>
                <li onclick="checkAnswer(5, 'b', 942)">ב) 942 סמ"ר</li>
                <li onclick="checkAnswer(5, 'c', 2826)">ג) 2826 סמ"ר</li>
                <li onclick="checkAnswer(5, 'd', 900)">ד) 900 סמ"ר</li>
            </ul>
            <div class="feedback" id="feedback5"></div>
        </div>

        <div class="exercise" id="q6">
            <h3>תרגיל 6: צלחת עגולה</h3>
            <p>צלחת עגולה לקורנפלקס היא בעלת רדיוס של 7 ס"מ. מה השטח של פני הצלחת?</p>
            <ul class="options">
                <li onclick="checkAnswer(6, 'a', 43.96)">א) 43.96 סמ"ר</li>
                <li onclick="checkAnswer(6, 'b', 153.86)">ב) 153.86 סמ"ר</li>
                <li onclick="checkAnswer(6, 'c', 21.98)">ג) 21.98 סמ"ר</li>
                <li onclick="checkAnswer(6, 'd', 49)">ד) 49 סמ"ר</li>
            </ul>
            <div class="feedback" id="feedback6"></div>
        </div>

        <div class="exercise" id="q7">
            <h3>תרגיל 7: גינה עגולה</h3>
            <p>שתלנו גינת פרחים עגולה שההיקף שלה הוא 31.4 מטר. מהו הרדיוס של הגינה?</p>
            <ul class="options">
                <li onclick="checkAnswer(7, 'a', 10)">א) 10 מטר</li>
                <li onclick="checkAnswer(7, 'b', 3.14)">ב) 3.14 מטר</li>
                <li onclick="checkAnswer(7, 'c', 5)">ג) 5 מטר</li>
                <li onclick="checkAnswer(7, 'd', 15.7)">ד) 15.7 מטר</li>
            </ul>
            <div class="feedback" id="feedback7"></div>
        </div>
        
        <p style="text-align:center; font-weight:bold; font-size:1.2em; color:#e47200;">כל הכבוד על המאמץ! מקווים שנהניתם ולמדתם! 🍕🎉</p>

    </div>

    <script>
        const answers = {
            1: { correct: 'a', value: 62.8, type: 'היקף', r: 10, d: null, formula: "C = 2πr = 2 × 3.14 × 10 ס\"מ = 62.8 ס\"מ" },
            2: { correct: 'b', value: 314, type: 'שטח', r: 10, d: null, formula: "A = πr² = 3.14 × (10 ס\"מ)² = 3.14 × 100 סמ\"ר = 314 סמ\"ר" },
            3: { correct: 'c', value: 30, type: 'רדיוס', r: null, d: 60, formula: "הרדיוס הוא חצי מהקוטר. r = d/2 = 60 ס\"מ / 2 = 30 ס\"מ" },
            4: { correct: 'b', value: 188.4, type: 'היקף', r: 30, d: 60, formula: "C = 2πr = 2 × 3.14 × 30 ס\"מ = 188.4 ס\"מ (או C = πd = 3.14 × 60 ס\"מ = 188.4 ס\"מ)" },
            5: { correct: 'c', value: 2826, type: 'שטח', r: 30, d: null, formula: "A = πr² = 3.14 × (30 ס\"מ)² = 3.14 × 900 סמ\"ר = 2826 סמ\"ר" },
            6: { correct: 'b', value: 153.86, type: 'שטח', r: 7, d: null, formula: "A = πr² = 3.14 × (7 ס\"מ)² = 3.14 × 49 סמ\"ר = 153.86 סמ\"ר" },
            7: { correct: 'c', value: 5, type: 'רדיוס', r: null, d: null, circumference: 31.4, formula: "נתון היקף C = 31.4 מטר. הנוסחה היא C = 2πr. לכן, 31.4 = 2 × 3.14 × r => 31.4 = 6.28 × r.  נחלק את שני האגפים ב-6.28: r = 31.4 / 6.28 = 5 מטר" }
        };

        function checkAnswer(questionNum, chosenOptionKey, chosenValue) {
            const questionData = answers[questionNum];
            const feedbackDiv = document.getElementById('feedback' + questionNum);
            let feedbackHTML = '';

            const options = document.getElementById('q' + questionNum).getElementsByTagName('li');
            for (let opt of options) {
                opt.style.pointerEvents = 'none'; 
                opt.style.opacity = '0.7'; 
            }
            event.currentTarget.style.border = '2px solid #007bff';


            if (chosenOptionKey === questionData.correct) {
                feedbackHTML = `<div class="correct">כל הכבוד! תשובה נכונה! 👍</div>`;
            } else {
                feedbackHTML = `<div class="incorrect">אוי, תשובה לא נכונה. נסו לחשוב שוב! 🤔</div>`;
            }
            
            feedbackHTML += `<div class="explanation-detail"><strong>הסבר מפורט:</strong><br>`;
            if (questionData.type === 'היקף') {
                feedbackHTML += `חיפשנו את ההיקף (אורך הקראסט). הנוסחה היא <span class="formula">C = 2πr</span>.<br>`;
                if (questionData.r) {
                    feedbackHTML += `כאשר הרדיוס (r) הוא ${questionData.r} ס"מ (או מטר), והפאי (π) הוא בערך 3.14:<br>`;
                    feedbackHTML += `${questionData.formula}.<br>`;
                } else if (questionData.d) { 
                     feedbackHTML += `כאשר הקוטר (d) הוא ${questionData.d}, הרדיוס (r) הוא ${questionData.d/2}.<br>`;
                     feedbackHTML += `${questionData.formula}.<br>`;
                }
                 feedbackHTML += `לכן התשובה הנכונה היא ${questionData.value.toLocaleString()} יחידות אורך.`;
            } else if (questionData.type === 'שטח') {
                feedbackHTML += `חיפשנו את השטח (כמה פיצה יש). הנוסחה היא <span class="formula">A = πr²</span>.<br>`;
                feedbackHTML += `כאשר הרדיוס (r) הוא ${questionData.r} ס"מ (או מטר), והפאי (π) הוא בערך 3.14:<br>`;
                feedbackHTML += `${questionData.formula}.<br>`;
                feedbackHTML += `לכן התשובה הנכונה היא ${questionData.value.toLocaleString()} יחידות שטח (סמ"ר או מ"ר).`;
            } else if (questionData.type === 'רדיוס' && questionData.d) { 
                feedbackHTML += `חיפשנו את הרדיוס, וידוע לנו הקוטר (d = ${questionData.d}).<br>`;
                feedbackHTML += `הרדיוס הוא חצי מהקוטר: <span class="formula">r = d / 2</span>.<br>`;
                feedbackHTML += `${questionData.formula}.<br>`;
                feedbackHTML += `לכן התשובה הנכונה היא ${questionData.value.toLocaleString()} יחידות אורך.`;
            } else if (questionData.type === 'רדיוס' && questionData.circumference) { 
                feedbackHTML += `חיפשנו את הרדיוס, וידוע לנו ההיקף (C = ${questionData.circumference}).<br>`;
                feedbackHTML += `הנוסחה להיקף היא <span class="formula">C = 2πr</span>. אנחנו צריכים "לחלץ" את r.<br>`;
                feedbackHTML += `נציב את הנתונים: ${questionData.circumference} = 2 × 3.14 × r<br>`;
                feedbackHTML += `${questionData.circumference} = 6.28 × r<br>`;
                feedbackHTML += `כדי למצוא את r, נחלק את ההיקף ב-6.28: r = ${questionData.circumference} / 6.28<br>`;
                feedbackHTML += `r = ${questionData.value.toLocaleString()} מטר.<br>`;
                feedbackHTML += `לכן התשובה הנכונה היא ${questionData.value.toLocaleString()} יחידות אורך.`;
            }
            feedbackHTML += `</div>`;

            feedbackDiv.innerHTML = feedbackHTML;
        }
    </script>

</body>
</html>
