<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  function clearCanvas() {
    dispatch("clearCanvas");
  }

  function toggleEraser() {
    dispatch("toggleEraser");
  }
</script>

<button on:click={toggleEraser}>Toggle Eraser</button>
<button on:click={clearCanvas}>Clear Canvas</button>

<style>
  button {
    font-family: "Indie Flower", cursive;
    background-color: #f8f8f8;
    border: none;
    padding: 10px 20px;
    margin: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  button:hover {
    background-color: #e0e0e0;
  }
</style>
