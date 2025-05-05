<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Guess the Number Game</title>
    <style>
        :root {
            --primary: #6c5ce7;
            --secondary: #a29bfe;
            --success: #00b894;
            --danger: #d63031;
            --light: #f8f9fa;
            --dark: #343a40;
            --border-radius: 12px;
            --box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        
        .game-container {
            background-color: white;
            border-radius: var(--border-radius);
            box-shadow: var(--box-shadow);
            width: 100%;
            max-width: 500px;
            padding: 30px;
            text-align: center;
            animation: fadeIn 0.6s ease-out;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        h1 {
            color: var(--primary);
            margin-bottom: 15px;
            font-size: 2.2rem;
        }
        
        .subtitle {
            color: var(--dark);
            margin-bottom: 30px;
            opacity: 0.8;
            font-size: 1.1rem;
        }
        
        .game-area {
            margin: 25px 0;
        }
        
        .previous-guesses {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-bottom: 20px;
            min-height: 50px;
        }
        
        .previous-guess {
            font-size: 1.8rem;
            font-weight: bold;
            color: var(--primary);
            opacity: 0.7;
            transition: all 0.3s;
        }
        
        .previous-guess:first-child {
            opacity: 1;
            transform: scale(1.2);
        }
        
        .input-group {
            display: flex;
            margin-bottom: 20px;
        }
        
        input {
            flex: 1;
            padding: 15px;
            border: 2px solid #e0e0e0;
            border-radius: var(--border-radius) 0 0 var(--border-radius);
            font-size: 1.1rem;
            outline: none;
            transition: border-color 0.3s;
        }
        
        input:focus {
            border-color: var(--primary);
        }
        
        button {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 0 25px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: bold;
            transition: all 0.3s;
        }
        
        #guessButton {
            border-radius: 0 var(--border-radius) var(--border-radius) 0;
        }
        
        #resetButton {
            border-radius: var(--border-radius);
            background-color: var(--danger);
            margin-top: 15px;
            padding: 12px 25px;
            display: none;
        }
        
        button:hover {
            filter: brightness(0.9);
        }
        
        .message {
            padding: 15px;
            border-radius: var(--border-radius);
            margin-bottom: 20px;
            font-weight: bold;
            display: none;
        }
        
        .low {
            background-color: rgba(214, 48, 49, 0.1);
            color: var(--danger);
            display: block;
        }
        
        .high {
            background-color: rgba(253, 203, 110, 0.3);
            color: #e17055;
            display: block;
        }
        
        .success {
            background-color: rgba(0, 184, 148, 0.1);
            color: var(--success);
            display: block;
            animation: celebrate 0.5s ease;
        }
        
        @keyframes celebrate {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        .attempts {
            margin-top: 20px;
            font-size: 1rem;
            color: var(--dark);
            opacity: 0.8;
        }
        
        .confetti {
            position: absolute;
            width: 10px;
            height: 10px;
            background-color: #f00;
            border-radius: 50%;
            animation: fall 3s linear infinite;
        }
        
        @keyframes fall {
            to { transform: translateY(100vh); }
        }
        
        @media (max-width: 600px) {
            .game-container {
                padding: 20px;
            }
            
            h1 {
                font-size: 1.8rem;
            }
            
            .previous-guess {
                font-size: 1.5rem;
            }
            
            .input-group {
                flex-direction: column;
            }
            
            input {
                border-radius: var(--border-radius);
                margin-bottom: 10px;
            }
            
            #guessButton {
                border-radius: var(--border-radius);
                padding: 15px;
                width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="game-container">
        <h1>🎮 Guess the Number</h1>
        <p class="subtitle">Try to guess the secret number between 1 and 100</p>
        
        <div class="game-area">
            <div class="previous-guesses" id="previousGuesses">
                <!-- Previous guesses will appear here -->
            </div>
            
            <div class="input-group">
                <input type="number" id="guessInput" placeholder="Enter your guess..." min="1" max="100">
                <button id="guessButton">Guess</button>
            </div>
            
            <div class="message" id="message"></div>
            
            <div class="attempts" id="attempts">Attempts: 0</div>
            
            <button id="resetButton">New Game</button>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            let secretNumber = Math.floor(Math.random() * 100) + 1;
            let attempts = 0;
            let previousGuesses = [];
            const guessInput = document.getElementById('guessInput');
            const guessButton = document.getElementById('guessButton');
            const resetButton = document.getElementById('resetButton');
            const message = document.getElementById('message');
            const attemptsDisplay = document.getElementById('attempts');
            const previousGuessesDisplay = document.getElementById('previousGuesses');
            
            guessButton.addEventListener('click', checkGuess);
            resetButton.addEventListener('click', resetGame);
            guessInput.addEventListener('keypress', (e) => {
                if (e.key === 'Enter') checkGuess();
            });
            
            function checkGuess() {
                const guess = parseInt(guessInput.value);
                
                if (isNaN(guess) || guess < 1 || guess > 100) {
                    message.textContent = 'Please enter a valid number between 1 and 100';
                    message.className = 'message low';
                    return;
                }
                
                attempts++;
                attemptsDisplay.textContent = `Attempts: ${attempts}`;
                
                // Add to previous guesses (keep only last 3)
                previousGuesses.unshift(guess);
                if (previousGuesses.length > 3) {
                    previousGuesses.pop();
                }
                updatePreviousGuessesDisplay();
                
                if (guess < secretNumber) {
                    message.textContent = 'Too low! Try a higher number.';
                    message.className = 'message low';
                } else if (guess > secretNumber) {
                    message.textContent = 'Too high! Try a lower number.';
                    message.className = 'message high';
                } else {
                    message.textContent = `🎉 Correct! You guessed it in ${attempts} attempts!`;
                    message.className = 'message success';
                    guessInput.disabled = true;
                    guessButton.disabled = true;
                    resetButton.style.display = 'inline-block';
                    createConfetti();
                }
                
                guessInput.value = '';
                guessInput.focus();
            }
            
            function resetGame() {
                secretNumber = Math.floor(Math.random() * 100) + 1;
                attempts = 0;
                previousGuesses = [];
                attemptsDisplay.textContent = `Attempts: 0`;
                message.textContent = '';
                message.className = 'message';
                previousGuessesDisplay.innerHTML = '';
                guessInput.disabled = false;
                guessButton.disabled = false;
                resetButton.style.display = 'none';
                guessInput.focus();
                
                // Remove any remaining confetti
                document.querySelectorAll('.confetti').forEach(el => el.remove());
            }
            
            function updatePreviousGuessesDisplay() {
                previousGuessesDisplay.innerHTML = '';
                
                // Display up to 3 previous guesses
                const displayCount = Math.min(3, previousGuesses.length);
                for (let i = 0; i < displayCount; i++) {
                    const guessElement = document.createElement('div');
                    guessElement.className = 'previous-guess';
                    guessElement.textContent = previousGuesses[i];
                    previousGuessesDisplay.appendChild(guessElement);
                }
            }
            
            function createConfetti() {
                const colors = ['#6c5ce7', '#00b894', '#fd79a8', '#fdcb6e', '#e17055', '#0984e3'];
                
                for (let i = 0; i < 100; i++) {
                    const confetti = document.createElement('div');
                    confetti.className = 'confetti';
                    confetti.style.left = `${Math.random() * 100}vw`;
                    confetti.style.top = '-10px';
                    confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                    confetti.style.animationDuration = `${Math.random() * 3 + 2}s`;
                    confetti.style.width = `${Math.random() * 10 + 5}px`;
                    confetti.style.height = confetti.style.width;
                    document.body.appendChild(confetti);
                    
                    setTimeout(() => {
                        confetti.remove();
                    }, 3000);
                }
            }
        });
    </script>
</body>
</html>