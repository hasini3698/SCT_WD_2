# SCT_WD_2
stop watch web application
<!DOCTYPE html>
<html>
<head>
    <title>Stopwatch Application</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 100px;
            background-color: #f4f4f4;
        }

        #display {
            font-size: 40px;
            margin-bottom: 20px;
            font-weight: bold;
        }

        button {
            padding: 10px 15px;
            margin: 5px;
            font-size: 16px;
            cursor: pointer;
        }

        #laps {
            margin-top: 20px;
            max-height: 200px;
            overflow-y: auto;
        }
    </style>
</head>
<body>

<h1>Stopwatch</h1>
<div id="display">00:00:00:000</div>

<button onclick="start()">Start</button>
<button onclick="pause()">Pause</button>
<button onclick="reset()">Reset</button>
<button onclick="lap()">Lap</button>

<div id="laps"></div>

<script>
let startTime;
let elapsedTime = 0;
let timerInterval;
let running = false;

function formatTime(time) {
    let hrs = Math.floor(time / (1000 * 60 * 60));
    let mins = Math.floor((time % (1000 * 60 * 60)) / (1000 * 60));
    let secs = Math.floor((time % (1000 * 60)) / 1000);
    let ms = time % 1000;

    return (
        (hrs < 10 ? "0" + hrs : hrs) + ":" +
        (mins < 10 ? "0" + mins : mins) + ":" +
        (secs < 10 ? "0" + secs : secs) + ":" +
        (ms < 100 ? (ms < 10 ? "00" + ms : "0" + ms) : ms)
    );
}

function updateDisplay() {
    document.getElementById("display").innerText = formatTime(elapsedTime);
}

function start() {
    if (!running) {
        running = true;
        startTime = Date.now() - elapsedTime;

        timerInterval = setInterval(function () {
            elapsedTime = Date.now() - startTime;
            updateDisplay();
        }, 10);
    }
}

function pause() {
    if (running) {
        running = false;
        clearInterval(timerInterval);
    }
}

function reset() {
    running = false;
    clearInterval(timerInterval);
    elapsedTime = 0;
    updateDisplay();
    document.getElementById("laps").innerHTML = "";
}

function lap() {
    if (running) {
        let lapTime = document.createElement("div");
        lapTime.innerText = "Lap: " + formatTime(elapsedTime);
        document.getElementById("laps").appendChild(lapTime);
    }
}
</script>

</body>
</html>
