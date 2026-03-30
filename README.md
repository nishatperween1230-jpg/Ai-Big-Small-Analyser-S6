<!DOCTYPE html>
<html>
<head>
    <title>AI Pattern Analyzer</title>
    <style>
        body {
            font-family: Arial;
            text-align: center;
            background: linear-gradient(135deg, #000, #222);
            color: white;
        }

        h1 {
            margin-top: 20px;
        }

        button {
            padding: 15px 25px;
            margin: 10px;
            font-size: 18px;
            border-radius: 12px;
            border: none;
            cursor: pointer;
            transition: 0.2s;
        }

        button:hover {
            transform: scale(1.1);
        }

        .big { background: #00c853; }
        .small { background: #d50000; }
        .clear { background: gray; }

        .box {
            margin-top: 20px;
            font-size: 20px;
        }

        #result {
            margin-top: 20px;
            font-size: 24px;
            font-weight: bold;
        }
    </style>
</head>

<body>

<h1>🤖 AI Pattern Analyzer (Last 5)</h1>

<button class="big" onclick="add('B')">BIG</button>
<button class="small" onclick="add('S')">SMALL</button>
<button class="clear" onclick="reset()">CLEAR</button>

<div class="box">
    <h3>History:</h3>
    <p id="history"></p>
</div>

<div id="result">Enter at least 5 results</div>

<script>

let data = [];

function add(val) {
    data.push(val);
    update();
}

function reset() {
    data = [];
    update();
}

function update() {
    document.getElementById("history").innerText = data.join(" ");

    if (data.length < 5) {
        document.getElementById("result").innerText = "Enter at least 5 results";
        return;
    }

    let last5 = data.slice(-5);

    let countB = last5.filter(x => x === 'B').length;
    let countS = last5.filter(x => x === 'S').length;

    let pattern = last5.join("");

    let resultText = "";

    if (countB >= 4) {
        resultText = "🔥 90% BET → BIG";
    }
    else if (countS >= 4) {
        resultText = "🔥 90% BET → SMALL";
    }
    else if (countB === 3) {
        resultText = "⚡ 75% BET → BIG";
    }
    else if (countS === 3) {
        resultText = "⚡ 75% BET → SMALL";
    }
    else if (pattern === "BSBSB" || pattern === "SBSBS") {
        resultText = "❌ NO BET";
    }
    else {
        resultText = "⚖️ 50% RISK";
    }

    document.getElementById("result").innerText = resultText;
}

</script>

</body>
</html>
