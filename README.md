# Calculator-
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Calculator Pro</title>

<style>
body {
    margin: 0;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background: #0f2027;
    font-family: 'Poppins', sans-serif;
    color: white;
}

/* Layout */
.container {
    display: flex;
    gap: 20px;
}

/* Calculator */
.calculator {
    background: rgba(255,255,255,0.05);
    backdrop-filter: blur(15px);
    padding: 20px;
    border-radius: 20px;
    box-shadow: 0 0 30px rgba(0,255,255,0.2);
}

.display {
    width: 100%;
    height: 60px;
    border: none;
    outline: none;
    margin-bottom: 15px;
    border-radius: 12px;
    text-align: right;
    font-size: 1.8rem;
    padding: 10px;
    background: rgba(255,255,255,0.1);
    color: #00ffd5;
}

.buttons {
    display: grid;
    grid-template-columns: repeat(4, 70px);
    gap: 10px;
}

button {
    height: 60px;
    border: none;
    border-radius: 15px;
    font-size: 1.2rem;
    cursor: pointer;
    background: rgba(255,255,255,0.1);
    color: #fff;
    transition: 0.2s ease;
}

button:hover {
    background: rgba(255,255,255,0.25);
    transform: scale(1.05);
}

.operator { color: #00ffd5; }

.equal {
    background: #00ffd5;
    color: #000;
    font-weight: bold;
}

/* History panel */
.history {
    width: 200px;
    max-height: 350px;
    overflow-y: auto;
    background: rgba(255,255,255,0.05);
    backdrop-filter: blur(15px);
    padding: 15px;
    border-radius: 20px;
}

.history h3 {
    margin-top: 0;
    text-align: center;
}

.history-item {
    padding: 8px;
    margin: 5px 0;
    background: rgba(255,255,255,0.1);
    border-radius: 10px;
    cursor: pointer;
}

.history-item:hover {
    background: rgba(0,255,213,0.3);
}
</style>

</head>

<body>

<div class="container">

<!-- Calculator -->
<div class="calculator">
    <input type="text" id="display" class="display" disabled>

<div class="buttons">
        <button onclick="press('clear')">AC</button>
        <button onclick="press('delete')">⌫</button>
        <button class="operator" onclick="press('/')">÷</button>
  <button class="operator"onclick="press('*')">×</button>
<button onclick="press('7')">7</button>
        <button onclick="press('8')">8</button>
        <button onclick="press('9')">9</button>
        <button class="operator" onclick="press('-')">−</button>

<button onclick="press('4')">4</button>
        <button onclick="press('5')">5</button>
        <button onclick="press('6')">6</button>
        <button class="operator" onclick="press('+')">+</button>

<button onclick="press('1')">1</button>
        <button onclick="press('2')">2</button>
        <button onclick="press('3')">3</button>
        <button class="equal" onclick="press('=')">=</button>

<button onclick="press('0')" style="grid-column: span 2;">0</button>
        <button onclick="press('.')">.</button>
    </div>
</div>

<!-- History -->
<div class="history">
    <h3>History</h3>
    <div id="historyList"></div>
    <button onclick="clearHistory()">Clear</button>
</div>

</div>

<audio id="clickSound" src="https://www.fesliyanstudios.com/play-mp3/387"></audio>

<script>
let display = document.getElementById("display");
let historyList = document.getElementById("historyList");
let sound = document.getElementById("clickSound");

function playSound() {
    sound.currentTime = 0;
    sound.play();
}

function press(value) {
    playSound();

    if (value === "clear") {
        display.value = "";
    } 
    else if (value === "delete") {
        display.value = display.value.slice(0, -1);
    } 
    else if (value === "=") {
        try {
            let result = eval(display.value);
            
            // add to history
            addToHistory(display.value + " = " + result);

            display.value = result;
        } catch {
            display.value = "Error";
        }
    } 
    else {
        display.value += value;
    }
}

function addToHistory(text) {
    let div = document.createElement("div");
    div.className = "history-item";
    div.innerText = text;

    // click to reuse
    div.onclick = () => {
        display.value = text.split("=")[0].trim();
    };

    historyList.prepend(div);
}

function clearHistory() {
    historyList.innerHTML = "";
}
</script>

</body>
</html>
