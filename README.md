<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حساب عمر الطفل - وزارة التعليم</title>
    <style>
        /* إعدادات التصميم العامة */
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            /* إضافة صورة الخلفية */
            background: linear-gradient(rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0.8)), 
                        url('https://img.freepik.com/free-photo/cute-little-boy-with-backpack-holding-flowers-outdoors_23-2148210345.jpg'); 
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
        }

        .container {
            background-color: rgba(255, 255, 255, 0.95);
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
            width: 90%;
            max-width: 500px;
            text-align: center;
            border-top: 8px solid #2c3e50;
        }

        .header img { width: 100px; margin-bottom: 10px; }
        h2 { color: #2c3e50; margin: 5px 0; }
        h3 { color: #34495e; font-weight: normal; margin-bottom: 20px; }

        .input-group { margin: 25px 0; }
        label { display: block; margin-bottom: 10px; font-weight: bold; }
        input[type="date"] {
            padding: 10px;
            width: 80%;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
        }

        button {
            background-color: #27ae60;
            color: white;
            border: none;
            padding: 12px 25px;
            font-size: 18px;
            border-radius: 8px;
            cursor: pointer;
            transition: 0.3s;
            margin: 5px;
        }

        button:hover { background-color: #219150; }
        .print-btn { background-color: #2980b9; }

        #result {
            margin-top: 20px;
            padding: 15px;
            border-radius: 8px;
            display: none;
            font-weight: bold;
            background: #f9f9f9;
            border: 1px solid #eee;
        }

        .footer { margin-top: 30px; font-size: 0.9em; color: #7f8c8d; }

        /* إعدادات الطباعة */
        @media print {
            body { background: white; }
            .container { box-shadow: none; border: 1px solid #000; }
            button { display: none; }
        }
    </style>
</head>
<body>

<div class="container">
    <div class="header">
        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/11/Ministry_of_Education_Saudi_Arabia_Logo.svg/1200px-Ministry_of_Education_Saudi_Arabia_Logo.svg.png" alt="شعار الوزارة">
        <h2>وزارة التعليم</h2>
        <h3>إدارة التعليم بمنطقة نجران</h3>
    </div>

    <hr>

    <h1>حساب عمر الطفل</h1>
    
    <div class="input-group">
        <label>اختر تاريخ ميلاد الطفل:</label>
        <input type="date" id="birthdate">
    </div>

    <button onclick="calculateAge()">عرض النتيجة</button>
    <button class="print-btn" onclick="window.print()">🖨️ طباعة النتيجة</button>

    <div id="result"></div>

    <div class="footer">
        <p>مديرة الروضة ومصممته:</p>
        <strong>فاطمه صالح آل بحري</strong>
    </div>
</div>

<script>
    function calculateAge() {
        const birthDateInput = document.getElementById('birthdate').value;
        const resultDiv = document.getElementById('result');
        
        if (!birthDateInput) {
            alert("يرجى اختيار التاريخ أولاً");
            return;
        }

        const birthDate = new Date(birthDateInput);
        const today = new Date();
        
        let ageYears = today.getFullYear() - birthDate.getFullYear();
        let ageMonths = today.getMonth() - birthDate.getMonth();

        if (ageMonths < 0 || (ageMonths === 0 && today.getDate() < birthDate.getDate())) {
            ageYears--;
            ageMonths += 12;
        }

        let level = "";
        if (ageYears < 3) level = "الطفل دون سن القبول";
        else if (ageYears == 3) level = "المستوى الأول (روضة 1)";
        else if (ageYears == 4) level = "المستوى الثاني (روضة 2)";
        else if (ageYears == 5) level = "المستوى الثالث (روضة 3)";
        else level = "الطفل تجاوز سن رياض الأطفال (مؤهل للمدرسة)";

        resultDiv.style.display = "block";
        resultDiv.innerHTML = `عمر الطفل: ${ageYears} سنوات و ${ageMonths} شهور <br> الفئة: ${level}`;
    }
</script>

</body>
</html>
