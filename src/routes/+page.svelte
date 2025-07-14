<script>
   let board = Array(9).fill(null);
   let currentPlayer = 'X'
   
   function handleClick(index) {
    if (board[index] === null) {
        board[index] = currentPlayer;
        currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
    }
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
