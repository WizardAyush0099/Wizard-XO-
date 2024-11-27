<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tic-Tac-Toe Game</title>

</head>
<body>

    <div>
        <h1>Tic-Tac-Toe</h1>
        <div class="board">
            <div class="cell" data-index="0"></div>
            <div class="cell" data-index="1"></div>
            <div class="cell" data-index="2"></div>
            <div class="cell" data-index="3"></div>
            <div class="cell" data-index="4"></div>
            <div class="cell" data-index="5"></div>
            <div class="cell" data-index="6"></div>
            <div class="cell" data-index="7"></div>
            <div class="cell" data-index="8"></div>
        </div>
        <div class="status">Turn: X</div>
        <button class="reset-btn">Reset Game</button>
    </div>
<link rel="stylesheet" href="xo.css">
<script src="xo.js">
  
</script>

</body>
</html>
<style>
    body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f4f4f4;
        }
        h1 {
            text-align: center;
        }
        .board {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            gap: 10px;
            margin: 20px auto;
        }
        .cell {
            width: 100px;
            height: 100px;
            background-color: #fff;
            border: 2px solid #000;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 2rem;
            cursor: pointer;
        }
        .cell:hover {
            background-color: #f0f0f0;
        }
        .status {
            text-align: center;
            font-size: 1.5rem;
            margin-top: 10px;
        }
        .reset-btn {
            display: block;
            margin: 10px auto;
            padding: 10px 20px;
            font-size: 1rem;
            background-color: #007BFF;
            color: white;
            border: none;
            cursor: pointer;
        }
        .reset-btn:hover {
            background-color: #0056b3;
        }
body {
    font-family: 'Arial', sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background: linear-gradient(to right, #74ebd5, #9face6); /* Beautiful gradient background */
    margin: 0;
}

h1 {
    text-align: center;
    color: #ffffff;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
    margin-bottom: 20px;
}

.board {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    gap: 10px;
    margin: 20px auto;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
}

.cell {
    width: 100px;
    height: 100px;
    background-color: #fff;
    border: 2px solid #333;
    border-radius: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 3rem;
    cursor: pointer;
    transition: background-color 0.3s, transform 0.2s; /* Animation effects */
}

.cell:hover {
    background-color: #f0f0f0;
    transform: scale(1.1);
}

.cell.x {
    color: #ff6347; /* Tomato color for X */
    text-shadow: 2px 2px 0 rgba(255, 99, 71, 0.7);
}

.cell.o {
    color: #4682b4; /* Steel blue color for O */
    text-shadow: 2px 2px 0 rgba(70, 130, 180, 0.7);
}

.status {
    text-align: center;
    font-size: 1.5rem;
    margin-top: 10px;
    color: #ffffff;
    text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
}

.reset-btn {
    display: block;
    margin: 10px auto;
    padding: 10px 20px;
    font-size: 1rem;
    background-color: #007BFF;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s, transform 0.2s; /* Animation effects */
}
body{
  border: solid red 12px;
}

</style>
<script>
    const board = document.querySelector('.board');
        const cells = document.querySelectorAll('.cell');
        const statusText = document.querySelector('.status');
        const resetBtn = document.querySelector('.reset-btn');
        let currentPlayer = 'X';
        let boardState = ["", "", "", "", "", "", "", "", ""];
        let isGameActive = true;

        const winningConditions = [
            [0, 1, 2],
            [3, 4, 5],
            [6, 7, 8],
            [0, 3, 6],
            [1, 4, 7],
            [2, 5, 8],
            [0, 4, 8],
            [2, 4, 6]
        ];

        function handleCellClick(event) {
            const cell = event.target;
            const index = cell.getAttribute('data-index');

            if (boardState[index] !== "" || !isGameActive) {
                return;
            }

            boardState[index] = currentPlayer;
            cell.textContent = currentPlayer;
            checkResult();
            switchPlayer();
        }

        function switchPlayer() {
            currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
            statusText.textContent = `Turn: ${currentPlayer}`;
        }

        function checkResult() {
            let roundWon = false;
            for (let i = 0; i < winningConditions.length; i++) {
                const [a, b, c] = winningConditions[i];
                if (boardState[a] && boardState[a] === boardState[b] && boardState[a] === boardState[c]) {
                    roundWon = true;
                    break;
                }
            }

            if (roundWon) {
                statusText.textContent = `Winner: ${currentPlayer}`;
                isGameActive = false;
                return;
            }

            if (!boardState.includes("")) {
                statusText.textContent = `Draw!`;
                isGameActive = false;
                return;
            }
        }

        function resetGame() {
            currentPlayer = 'X';
            boardState = ["", "", "", "", "", "", "", "", ""];
            isGameActive = true;
            statusText.textContent = `Turn: ${currentPlayer}`;
            cells.forEach(cell => cell.textContent = "");
        }

        cells.forEach(cell => cell.addEventListener('click', handleCellClick));
        resetBtn.addEventListener('click', resetGame);
</script>
