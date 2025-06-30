<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Hare Krishna vs Shri Radha - Tic Tac Toe</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background: #f9f9f9;
      text-align: center;
      padding-top: 40px;
    }

    h1 {
      color: #8b0000;
    }

    #board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      gap: 5px;
      justify-content: center;
      margin: 20px auto;
    }

    .cell {
      width: 100px;
      height: 100px;
      font-size: 13px;
      font-weight: bold;
      background-color: #fff;
      border: 2px solid #8b0000;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      padding: 10px;
      text-align: center;
    }

    .harekrishna {
      color: #006400;
    }

    .shriradha {
      color: #8b008b;
    }

    button {
      padding: 10px 20px;
      background-color: #006400;
      color: white;
      border: none;
      font-size: 16px;
      cursor: pointer;
      margin-top: 20px;
    }

    button:hover {
      background-color: #004d00;
    }
  </style>
</head>
<body>
  <h1>Tic Tac Toe: Hare Krishna vs Shri Radha</h1>
  <div id="board"></div>
  <button onclick="restartGame()">Restart Game</button>

  <audio id="krishnaMusic" src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3"></audio>

  <script>
    const board = document.getElementById("board");
    const music = document.getElementById("krishnaMusic");
    let currentPlayer = "Hare Krishna";
    let gameActive = true;
    let cells = [];

    function createBoard() {
      board.innerHTML = "";
      cells = Array(9).fill("");
      for (let i = 0; i < 9; i++) {
        const cell = document.createElement("div");
        cell.classList.add("cell");
        cell.addEventListener("click", () => makeMove(i, cell));
        board.appendChild(cell);
      }
    }

    function makeMove(index, cell) {
      if (!gameActive || cells[index] !== "") return;

      cells[index] = currentPlayer;
      cell.textContent = currentPlayer;
      cell.classList.add(currentPlayer === "Hare Krishna" ? "harekrishna" : "shriradha");

      if (checkWinner()) {
        music.currentTime = 0;
        music.play();
        setTimeout(() => alert(`🎉 Congratulations! ${currentPlayer} wins the game!`), 100);
        gameActive = false;
        return;
      }

      if (!cells.includes("")) {
        setTimeout(() => alert("It's a draw!"), 100);
        gameActive = false;
        return;
      }

      currentPlayer = currentPlayer === "Hare Krishna" ? "Shri Radha" : "Hare Krishna";
    }

    function checkWinner() {
      const wins = [
        [0,1,2], [3,4,5], [6,7,8],
        [0,3,6], [1,4,7], [2,5,8],
        [0,4,8], [2,4,6]
      ];

      return wins.some(pattern => {
        const [a, b, c] = pattern;
        return cells[a] && cells[a] === cells[b] && cells[b] === cells[c];
      });
    }

    function restartGame() {
      gameActive = true;
      currentPlayer = "Hare Krishna";
      music.pause();
      music.currentTime = 0;
      createBoard();
    }

    createBoard();
  </script>
</body>
</html>
