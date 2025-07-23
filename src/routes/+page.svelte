<script>
  let board = Array(9).fill(null);
  let currentPlayer = "X";
  let scoreX = 0;
  let scoreO = 0;
  let gameOver = false;

  function handleClick(index) {
    if (gameOver || board[index] !== null) return;

    board[index] = currentPlayer;

    const winner = checkWinner(board);
    if (winner) {
      gameOver = true;
      if (winner === "X") scoreX += 1;
      else if (winner === "O") scoreO += 1;

      alert(`Le joueur ${winner} a gagné !`);
      return;
    }

    if (!board.includes(null)) {
      gameOver = true;
      alert("Match nul !");
      return;
    }

    currentPlayer = currentPlayer === "X" ? "O" : "X";
  }

  function checkWinner(board) {
    const combos = [
      [0, 1, 2],
      [3, 4, 5],
      [6, 7, 8],
      [0, 3, 6],
      [1, 4, 7],
      [2, 5, 8],
      [0, 4, 8],
      [2, 4, 6],
    ];
    for (const [a, b, c] of combos) {
      if (board[a] && board[a] === board[b] && board[a] === board[c])
        return board[a];
    }
    return null;
  }

  function resetGame() {
    board = Array(9).fill(null);
    currentPlayer = "X";
    gameOver = false;
  }
</script>

<h1>Morpion</h1>

<div class="header">
  <div class="scoreboard">
    <p><span>X</span> : {scoreX}</p>
    <p><span>O</span> : {scoreO}</p>
  </div>
  {#if !gameOver}
    <p class="turn">Au tour de <strong>{currentPlayer}</strong></p>
  {/if}
</div>

<div class="grid">
  {#each board as cell, index}
    <div class="cell" on:click={() => handleClick(index)}>
      {cell}
    </div>
  {/each}
</div>

<button class="reset" on:click={resetGame}>🔁 Rejouer</button>

<style>
  * {
    box-sizing: border-box;
  }

  h1 {
    text-align: center;
    font-family: "Segoe UI", sans-serif;
    margin-bottom: 1rem;
    font-size: 2rem;
    color: #444;
  }

  .header {
    text-align: center;
    margin-bottom: 1.5rem;
  }

  .scoreboard {
    display: flex;
    justify-content: center;
    gap: 2rem;
    font-weight: bold;
    font-size: 1.2rem;
    margin-bottom: 0.5rem;
  }

  .scoreboard span {
    font-size: 1.4rem;
    color: #4a90e2;
  }

  .turn {
    font-size: 1rem;
    color: #666;
  }

  .grid {
    display: grid;
    grid-template-columns: repeat(3, 80px);
    grid-template-rows: repeat(3, 80px);
    gap: 10px;
    justify-content: center;
    margin: 0 auto 20px;
  }

  .cell {
    display: flex;
    align-items: center;
    justify-content: center;
    background: #f7f7f7;
    border-radius: 8px;
    border: 2px solid #ccc;
    font-size: 2.5rem;
    font-weight: bold;
    cursor: pointer;
    transition:
      background 0.2s,
      transform 0.1s;
  }

  .cell:hover {
    background: #eaeaea;
    transform: scale(1.03);
  }

  .cell:active {
    transform: scale(0.97);
  }

  .reset {
    display: block;
    margin: 0 auto;
    padding: 10px 25px;
    background: #4a90e2;
    color: white;
    font-weight: bold;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-size: 1rem;
    transition: background 0.2s ease;
  }

  .reset:hover {
    background: #357ab8;
  }
</style>
