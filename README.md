<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حساب عمر الطفل - وزارة التعليم</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            
            /* --- إعدادات الخلفية --- */
            background-color: #e0f2f1; /* لون احتياطي في حال لم تظهر الصورة */
            background-image: linear-gradient(rgba(255, 255, 255, 0.7), rgba(255, 255, 255, 0.7)), 
                              url('https://img.freepik.com/free-photo/boy-with-backpack-flowers_23-2148210364.jpg'); 
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
            background-repeat: no-repeat;
        }

        .container {
            background-color: rgba(255, 255, 255, 0.95);
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            width: 90%;
            max-width: 450px;
            text-align: center;
            border-top: 10px solid #2e7d32; /* لون أخضر تعليمي */
        }

        .header img { width: 120px; margin-bottom: 15px; }
        h2 { color: #1b5e20; margin: 5px 0; font-size: 1.5em; }
        h3 { color: #455a64; font-weight: normal; margin-bottom: 25px; font-size: 1.1em; }

        .input-group { margin: 30px 0; background: #f1f8e9; padding: 20px; border-radius: 10px; }
        label { display: block; margin-bottom: 15px; font-weight: bold; color: #333; }
        
        input[type="date"] {
            padding: 12px;
            width: 90%;
            border: 2px solid #a5d6a7;
            border-radius: 10px;
            font-size: 18px;
            outline: none;
            text-align: center;
        }

        .btns-container { display: flex; gap: 10px; justify-content: center; flex-wrap: wrap; }
        
        button {
            background-color: #4caf50;
            color: white;
            border: none;
            padding: 15px 30px;
            font-size: 18px;
            border-radius: 10px;
            cursor: pointer;
            transition: 0.3s;
            flex: 1;
            min-width: 150px;
        }

        button:hover { background-color: #388e3c; transform: translateY(-2px); }
        .print-btn { background-color: #0288d1; }
        .print-btn:hover { background-color: #01579b; }

        #result {
            margin-top: 25px;
            padding: 20px;
            border-radius: 10px;
            display: none;
            font-size: 1.2em;
            line-height: 1.6;
            background: #fff3e0;
            border: 2px dashed #ffb74d;
            color: #e65100;
        }

        .footer { 
            margin-top: 40px; 
            padding-top: 20px;
            border-top: 1px solid #eee;
            color: #616161; 
        }

        /* تنسيق الطباعة */
        @media print {
            body { background: none !important; }
            .container { box-shadow: none; border: 2px solid #000; width: 100%; max-width: 100%; }
            button { display: none; }
        }
    </style>
</head>
<body>

<div class="container">
    <div class="header">
        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/11/Ministry_of_Education_Saudi_Arabia_Logo.svg/512px-Ministry_of_Education_Saudi_Arabia_Logo.svg.png" alt="وزارة التعليم">
        <h2>وزارة التعليم</h2>
        <h3>إدارة التعليم بمنطقة نجران</h3>
    </div>

    <h1>حساب عمر الطفل</h1>
    
    <div class="input-group">
        <label>أدخل تاريخ ميلاد الطفل:</label>
        <input type="date" id="birthdate">
    </div>

    <div class="btns-container">
        <button onclick="calculateAge()">عرض النتيجة</button>
        <button class="print-btn" onclick="window.print()">🖨️ طباعة النتيجة</button>
    </div>

    <div id="result"></div>

    <div class="footer">
        <p>مديرة الروضة ومصممته:</p>
        <strong>فاطمة صالح آل بحري</strong>
    </div>
</div>

<script>
    function calculateAge() {
        const birthInput = document.getElementById('birthdate').value;
        const resultDiv = document.getElementById('result');
        
        if (!birthInput) {
            alert("لطفاً، اختر تاريخ الميلاد أولاً");
            return;
        }

        const birthDate = new Date(birthInput);
        const today = new Date();
        
        let years = today.getFullYear() - birthDate.getFullYear();
        let months = today.getMonth() - birthDate.getMonth();

        if (months < 0 || (months === 0 && today.getDate() < birthDate.getDate())) {
            years--;
            months += 12;
        }

        let category = "";
        if (years < 3) {
            category = "عذراً، الطفل دون سن القبول";
        } else if (years === 3) {
            category = "المستوى الأول (روضة 1)";
        } else if (years === 4) {
            category = "المستوى الثاني (روضة 2)";
        } else if (years === 5) {
            category = "المستوى الثالث (روضة 3)";
        } else {
            category = "الطفل مؤهل للمرحلة الابتدائية";
        }

        resultDiv.style.display = "block";
        resultDiv.innerHTML = `
            <strong>النتيجة:</strong><br>
            عمر الطفل: ${years} سنوات و ${months} أشهر<br>
            الفئة المستحقة: ${category}
        `;
    }
</script>

</body>
</html>
