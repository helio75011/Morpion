<script>
  let board = Array(9).fill(null);
  let currentPlayer = "X";
  let scoreX = 0;
  let scoreO = 0;

  function handleClick(index) {
    if (board[index] === null) {
      board[index] = currentPlayer;

      const winner = checkWinner(board);
      if (winner) {
        if (winner === "X") {
          scoreX += 1;
        } else if (winner === "O") {
          scoreO += 1;
        }

        alert(`Le joueur ${winner} a gagné !`);
        return;
      }

      if (!board.includes(null)) {
        alert("Match nul !");
        return; // on arrête aussi la partie
      }

      currentPlayer = currentPlayer === "X" ? "O" : "X";
    }
  }

  function checkWinner(board) {
    const winningCombos = [
      [0, 1, 2], // lignes
      [3, 4, 5],
      [6, 7, 8],
      [0, 3, 6], // colonnes
      [1, 4, 7],
      [2, 5, 8],
      [0, 4, 8], // diagonales
      [2, 4, 6],
    ];

    for (const [a, b, c] of winningCombos) {
      if (board[a] && board[a] === board[b] && board[a] === board[c]) {
        return board[a]; // 'X' ou 'O'
      }
    }

    return null;
  }

  function resetGame() {
    board = Array(9).fill(null);
    currentPlayer = "X";
  }
</script>

<h1>Grille de test</h1>

<div class="scores">
  <p>Score X : {scoreX}</p>
  <p>Score O : {scoreO}</p>
</div>

<div class="grid">
  {#each board as cell, index}
    <div class="cell" on:click={() => handleClick(index)}>
      {cell}
    </div>
  {/each}
</div>

<p>Au tour de {currentPlayer}</p>

<button on:click={resetGame}> Rejouer </button>

<style>
  .grid {
    display: grid;
    grid-template-columns: repeat(3, 60px);
    gap: 8px;
    margin-top: 20px;
  }

  .cell {
    width: 60px;
    height: 60px;
    font-size: 2rem;
    text-align: center;
    line-height: 60px;
    background-color: #eee;
    border: 1px solid #ccc;
    cursor: pointer;
  }

  button {
    margin-top: 20px;
    padding: 10px 20px;
    font-size: 1rem;
    cursor: pointer;
  }

  .scores {
    display: flex;
    font-weight: bold;
    margin-bottom: 10px;
  }

  .scores p {
    margin-right: 20px;
  }
</style>
