<!DOCTYPE html>
<html>
<head>
    <title>电路基础测试</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 20px auto;
            line-height: 1.6;
        }
        .question {
            margin-bottom: 20px;
            padding: 10px;
            border-left: 4px solid #4CAF50;
            background-color: #f9f9f9;
        }
        input {
            width: 150px;
            margin-right: 10px;
            padding: 5px;
            font-size: 16px;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        #result {
            margin-top: 30px;
            padding: 20px;
            border: 2px solid #4CAF50;
            background-color: #e8f5e9;
        }
        .correct { color: green; }
        .incorrect { color: red; }
        .rating { font-weight: bold; }
    </style>
</head>
<body>
    <h1 style="text-align:center;">电路基础测试</h1>
    
    <!-- 10道题目 -->
    <div class="question">
        <strong>1.</strong> 2Ω和3Ω并联，总电阻是多少？（单位：Ω）<br>
        <input type="text" id="q1">
    </div>

    <div class="question">
        <strong>2.</strong> 电动势12V内阻0.5Ω，外电路5Ω，路端电压？<br>
        <input type="text" id="q2">
    </div>

    <div class="question">
        <strong>3.</strong> 0.5H线圈电流0.2s从2A降到0，自感电动势？<br>
        <input type="text" id="q3">
    </div>

    <div class="question">
        <strong>4.</strong> R=3Ω，L=0.1H，50Hz交流阻抗Z？<br>
        <input type="text" id="q4">
    </div>

    <div class="question">
        <strong>5.</strong> 三个6Ω电阻（两并联+一串联），总电阻？<br>
        <input type="text" id="q5">
    </div>

    <div class="question">
        <strong>6.</strong> 测得-5V表示什么物理意义？<br>
        <input type="text" id="q6">
    </div>

    <div class="question">
        <strong>7.</strong> 2H和3H电感串联，总电感？<br>
        <input type="text" id="q7">
    </div>

    <div class="question">
        <strong>8.</strong> C=10μF和L=1mH并联，谐振频率？<br>
        <input type="text" id="q8">
    </div>

    <div class="question">
        <strong>9.</strong> 220V时电流0.22A，380V时电流？<br>
        <input type="text" id="q9">
    </div>

    <div class="question">
        <strong>10.</strong> 电感磁能与什么量成正比？<br>
        <input type="text" id="q10">
    </div>

    <button onclick="checkAnswers()">提交答案</button>
    
    <div id="result"></div>

    <script>
        const answers = {
            q1: "1.2",          
            q2: "11.43",        
            q3: "5",            
            q4: "10.38",        
            q5: "9",            
            q6: "电位差方向",  
            q7: "5",            
            q8: "5040/π",       
            q9: "0.38",         
            q10: "电流平方"     
        };

        const topics = {
            q1: "并联电阻计算",
            q2: "闭合电路欧姆定律",
            q3: "法拉第电磁感应定律",
            q4: "RL串联阻抗计算",
            q5: "混合连接电阻计算",
            q6: "电压极性理解",
            q7: "电感串联计算",
            q8: "LC谐振频率计算",
            q9: "欧姆定律应用",
            q10: "电感储能公式"
        };

        function checkAnswers() {
            let resultText = "<h3>测试结果：</h3>";
            let score = 0;
            let feedback = [];

            for (let i = 1; i <= 10; i++) {
                const qid = "q" + i;
                const userAns = document.getElementById(qid).value.trim();
                const correctAns = answers[qid];

                const isNumeric = !isNaN(parseFloat(userAns));
                let isCorrect = false;

                if (isNumeric && !isNaN(correctAns)) {
                    isCorrect = Math.abs(parseFloat(userAns) - parseFloat(correctAns)) < 0.01;
                } else {
                    isCorrect = userAns.toLowerCase() === correctAns.toLowerCase();
                }

                if (isCorrect) {
                    resultText += `<span class="correct">✅ 第${i}题 正确</span><br>`;
                    score++;
                } else {
                    resultText += `<span class="incorrect">❌ 第${i}题 错误（正确答案：${correctAns}）</span><br>`;
                    feedback.push(`<strong>需复习：</strong>【${topics[qid]}】`);
                }
            }

            resultText += `<h4>得分：${score}/10</h4>`;
            resultText += `<p class="rating">${getRating(score)}</p>`;
            if (feedback.length > 0) {
                resultText += feedback.join("<br>");
            } else {
                resultText += "<p class='correct'>🎉 全部正确！继续保持！</p>";
            }

            document.getElementById('result').innerHTML = resultText;
        }

        function getRating(score) {
            if (score >= 9) {
                return "🌟 优：你对电路基础掌握得非常扎实！继续保持！";
            } else if (score >= 6) {
                return "👍 良：大多数知识点掌握不错，但仍有提升空间。";
            } else {
                return "⚠️ 差：建议从基础开始系统学习，多做练习题。";
            }
        }
    </script>
</body>
</html>
