<script>
   let board = Array(9).fill(null);
   let currentPlayer = 'X'
   
   function handleClick(index) {
    if (board[index] === null) {
        board[index] = currentPlayer;

        const winner = checkWinner(board);
        if (winner) {
          alert(`Le joueur ${winner} a gagné !`);
          return; // on arrête la partie ici
        }

        currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
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
      [2, 4, 6]
    ];

    for (const [a, b, c] of winningCombos) {
      if (board[a] && board[a] === board[b] && board[a] === board[c]) {
        return board[a]; // 'X' ou 'O'
      }
    }

    return null;
   }


</script>

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
</style>

<h1>Grille de test</h1>

<div class="grid">
    {#each board as cell, index}
        <div class="cell" on:click={() => handleClick(index)}>
            {cell}
        </div>
    {/each}
</div>
