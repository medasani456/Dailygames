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
        .number-buttons {
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
        img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: block;
        }
        .navigation {
            margin-top: 20px;
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
    <div class="number-buttons" id="buttons"></div>
    <button id="toggleAll">Toggle All</button>
    <div id="rowButtons"></div>
    <div id="colButtons"></div>
    
    <script>
        const gridContainer = document.getElementById("grid");
        const buttonsContainer = document.getElementById("buttons");
        const folderLoader = document.getElementById("folderLoader");
        const gameImage = document.getElementById("gameImage");
        const prevBtn = document.getElementById("prevBtn");
        const nextBtn = document.getElementById("nextBtn");
        const imageCounter = document.getElementById("imageCounter");
        const toggleAllBtn = document.getElementById("toggleAll");
        const rowButtons = document.getElementById("rowButtons");
        const colButtons = document.getElementById("colButtons");
        
        let images = [];
        let currentIndex = 0;
        let gridItems = [];

        folderLoader.addEventListener("change", function(event) {
            images = Array.from(event.target.files).map(file => URL.createObjectURL(file));
            if (images.length > 0) {
                currentIndex = 0;
                updateImage();
            }
        });

        prevBtn.addEventListener("click", function() {
            if (currentIndex > 0) {
                currentIndex--;
                updateImage();
            }
        });

        nextBtn.addEventListener("click", function() {
            if (currentIndex < images.length - 1) {
                currentIndex++;
                updateImage();
            }
        });

        function updateImage() {
            gameImage.src = images[currentIndex];
            imageCounter.textContent = `${currentIndex + 1}/${images.length}`;
        }

        for (let row = 0; row < 4; row++) {
            for (let col = 0; col < 6; col++) {
                let index = row * 6 + col;
                let tile = document.createElement("div");
                tile.classList.add("grid-item");
                tile.setAttribute("data-index", index);
                tile.textContent = index + 1;
                tile.style.top = `${row * 100}px`;
                tile.style.left = `${col * 100}px`;
                gridContainer.appendChild(tile);
                gridItems.push(tile);

                let button = document.createElement("button");
                button.textContent = index + 1;
                button.onclick = () => {
                    tile.style.display = tile.style.display === "none" ? "flex" : "none";
                };
                buttonsContainer.appendChild(button);
            }
        }

        toggleAllBtn.onclick = () => {
            gridItems.forEach(tile => {
                tile.style.display = tile.style.display === "none" ? "flex" : "none";
            });
        };

        for (let row = 0; row < 4; row++) {
            let rowBtn = document.createElement("button");
            rowBtn.textContent = `Toggle Row ${row + 1}`;
            rowBtn.onclick = () => {
                for (let col = 0; col < 6; col++) {
                    let index = row * 6 + col;
                    gridItems[index].style.display = gridItems[index].style.display === "none" ? "flex" : "none";
                }
            };
            rowButtons.appendChild(rowBtn);
        }

        for (let col = 0; col < 6; col++) {
            let colBtn = document.createElement("button");
            colBtn.textContent = `Toggle Col ${col + 1}`;
            colBtn.onclick = () => {
                for (let row = 0; row < 4; row++) {
                    let index = row * 6 + col;
                    gridItems[index].style.display = gridItems[index].style.display === "none" ? "flex" : "none";
                }
            };
            colButtons.appendChild(colBtn);
        }
    </script>
</body>
</html>