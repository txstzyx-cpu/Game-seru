<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Game Puzzle - Karya Aditiya</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #74ebd5, #ACB6E5);
      text-align: center;
      padding: 20px;
    }

    h1 {
      color: #333;
      margin-bottom: 20px;
    }

    #puzzle-container {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-gap: 5px;
      justify-content: center;
      margin: 20px auto;
    }

    .tile {
      width: 100px;
      height: 100px;
      background-color: #fff;
      border-radius: 10px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.3);
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 28px;
      font-weight: bold;
      color: #333;
      cursor: pointer;
      transition: 0.2s;
    }

    .tile:hover {
      background-color: #d1e7dd;
    }

    .empty {
      background-color: transparent;
      box-shadow: none;
      cursor: default;
    }

    footer {
      margin-top: 30px;
      font-weight: bold;
      font-size: 18px;
      color: #222;
    }
  </style>
</head>
<body>

  <h1>🧩 Game Puzzle Sederhana</h1>
  <div id="puzzle-container"></div>

  <footer>✨ Karya Aditiya ✨</footer>

  <script>
    const container = document.getElementById('puzzle-container');
    let tiles = [1,2,3,4,5,6,7,8,null]; // 3x3 puzzle

    // Acak ubin puzzle
    tiles.sort(() => Math.random() - 0.5);

    function renderPuzzle() {
      container.innerHTML = '';
      tiles.forEach((num, i) => {
        const tile = document.createElement('div');
        tile.classList.add('tile');
        if (num === null) {
          tile.classList.add('empty');
        } else {
          tile.textContent = num;
          tile.onclick = () => moveTile(i);
        }
        container.appendChild(tile);
      });
    }

    function moveTile(index) {
      const emptyIndex = tiles.indexOf(null);
      const validMoves = [index - 1, index + 1, index - 3, index + 3];

      if (validMoves.includes(emptyIndex)) {
        [tiles[index], tiles[emptyIndex]] = [tiles[emptyIndex], tiles[index]];
        renderPuzzle();
        checkWin();
      }
    }

    function checkWin() {
      const winState = [1,2,3,4,5,6,7,8,null];
      if (JSON.stringify(tiles) === JSON.stringify(winState)) {
        setTimeout(() => alert("🎉 Selamat! Puzzle selesai!"), 100);
      }
    }

    renderPuzzle();
  </script>

</body>
</html>
