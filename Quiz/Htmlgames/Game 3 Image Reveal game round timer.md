<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Image Reveal Game</title>
    <style>
        body {
            text-align: center;
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            background-color: #ffebee;
            color: #b71c1c;
        }
        .image-container {
            position: relative;
            width: 600px;
            height: 400px;
            overflow: hidden;
            border: 5px solid #d32f2f;
            border-radius: 10px;
        }
        .grid-container {
            display: grid;
            grid-template-columns: repeat(6, 100px);
            grid-template-rows: repeat(4, 100px);
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }
        .grid-item {
            width: 100px;
            height: 100px;
            background-color: #b71c1c;
            position: absolute;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            font-weight: bold;
            color: white;
            border: 1px solid #d32f2f;
        }
        img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: block;
        }
        .navigation, .timer-controls {
            margin-top: 20px;
        }
        button {
            margin: 5px;
            padding: 10px;
            font-size: 16px;
            cursor: pointer;
            background-color: #d32f2f;
            color: white;
            border: none;
            border-radius: 5px;
        }
        button:hover {
            background-color: #b71c1c;
        }
    </style>
</head>
<body>
    <h1>Image Reveal Game</h1>
    <input type="file" id="folderLoader" webkitdirectory directory multiple accept="image/*">
    <div class="image-container">
        <img id="gameImage" src="https://via.placeholder.com/1920x1080" alt="Hidden Image">
        <div class="grid-container" id="grid"></div>
    </div>
    <div class="navigation">
        <button id="prevBtn">Previous</button>
        <span id="imageCounter">1/1</span>
        <button id="nextBtn">Next</button>
    </div>
    <div class="timer-controls">
        <input type="number" id="timerInterval" placeholder="Interval (ms)" min="1" value="2000">
        <select id="tileCount">
            <option value="1">1</option>
            <option value="2">2</option>
            <option value="3">3</option>
            <option value="4">4</option>
            <option value="5">5</option>
            <option value="6">6</option>
            <option value="7">7</option>
            <option value="8">8</option>
            <option value="9">9</option>
            <option value="10">10</option>
            <option value="11">11</option>
            <option value="12">12</option>
            <option value="13">13</option>
            <option value="14">14</option>
            <option value="15">15</option>
            <option value="16">16</option>
            <option value="17">17</option>
            <option value="18">18</option>
            <option value="19">19</option>
            <option value="20">20</option>
            <option value="21">21</option>
            <option value="22">22</option>
            <option value="23">23</option>
            <option value="24">24</option>
        </select>
        <button id="startTimer">Start Timer</button>
        <button id="stopTimer">Stop Timer</button>
        <button id="resetGame">Reset</button>
    </div>
    <script>
        const gridContainer = document.getElementById("grid");
        const resetBtn = document.getElementById("resetGame");
        const gridItems = [];

        function createGrid() {
            gridContainer.innerHTML = "";
            for (let i = 0; i < 24; i++) {
                let tile = document.createElement("div");
                tile.classList.add("grid-item");
                tile.textContent = i + 1;
                tile.style.display = "flex";
                gridContainer.appendChild(tile);
                gridItems.push(tile);
            }
        }

        resetBtn.addEventListener("click", () => {
            gridItems.forEach(tile => tile.style.display = "flex");
        });

        createGrid();
    </script>
</body>
</html>
