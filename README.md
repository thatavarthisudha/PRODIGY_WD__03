# PRODIGY_WD__03
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic Tac Toe Game</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-image: url('https://static.vecteezy.com/system/resources/previews/004/532/221/original/tic-tac-toe-seamless-background-on-dark-blue-illustration-vector.jpg');
            background-size: cover;
            background-position: center;
            font-family: Arial, sans-serif;
        }
        #gameBoard {
            display: grid;
            grid-template-columns: repeat(3, 150px);
            grid-template-rows: repeat(3, 150px);
            gap: 5px;
        }
        .cell {
            width: 120px;
            height: 120px;
            background-color: #ffffff;
            border-radius: 8px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 2rem;
            cursor: pointer;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
        }
        #status {
            margin-top: 20px;
            font-size: 1.2rem;
        }
        #resetButton {
            margin-top: 20px;
            padding: 20px 40px;
            font-size: 2rem;
            text-shadow: 0 0 3px #fff, -1px -1px 0 hsl(172, 70%, 35%), -2px -2px 1px hsl(172, 36%, 48%), -2px -2px 2px hsl(80, 28%, 17%);
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div>
        <div id="gameBoard"></div>
        <div id="status"></div>
        <button id="resetButton">Reset Game</button>
    </div>

    <script>
        const gameBoard = document.getElementById('gameBoard');
        const statusDisplay = document.getElementById('status');
        const resetButton = document.getElementById('resetButton');
        let board = ['', '', '', '', '', '', '', '', ''];
        let currentPlayer = '😃';
        let isGameActive = true;

        const winningConditions = [
            [0, 1, 2], [3, 4, 5], [6, 7, 8],
            [0, 3, 6], [1, 4, 7], [2, 5, 8],
            [0, 4, 8], [2, 4, 6]
        ];

        function handleClick(index) {
            if (board[index] === '' && isGameActive) {
                board[index] = currentPlayer;
                renderBoard();
                checkWinner();
                currentPlayer = currentPlayer === '😃' ? '😅' : '😃';
            }
        }

        function checkWinner() {
            for (const condition of winningConditions) {
                const [a, b, c] = condition;
                if (board[a] && board[a] === board[b] && board[a] === board[c]) {
                    statusDisplay.textContent = `Player ${board[a]} Wins!`;
                    isGameActive = false;
                    return;
                }
            }
            if (!board.includes('')) {
                statusDisplay.textContent = 'Draw!';
                isGameActive = false;
            }
        }

        function renderBoard() {
            gameBoard.innerHTML = '';
            board.forEach((cell, index) => {
                const cellElement = document.createElement('div');
                cellElement.classList.add('cell');
                cellElement.textContent = cell;
                cellElement.addEventListener('click', () => handleClick(index));
                gameBoard.appendChild(cellElement);
            });
        }

        resetButton.addEventListener('click', () => {
            board = ['', '', '', '', '', '', '', '', ''];
            isGameActive = true;
            currentPlayer = '😃';
            statusDisplay.textContent = '';
            renderBoard();
        });

        renderBoard();
    </script>
</body>
</html>
