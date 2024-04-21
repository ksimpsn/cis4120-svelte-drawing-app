<script>
  import Canvas from "./Canvas.svelte";
  import ColorPicker from "./ColorPicker.svelte";
  import LineWidthSelector from "./LineWidthSelector.svelte";
  import Controls from "./Controls.svelte";

  let color = "#000000";
  let lineWidth = 5;
  let isErasing = false;
  let canvasComponent;

  function handleColorChange(event) {
    if (!isErasing) {
      color = event.detail.color;
    }
  }

  function handleLineWidthChange(event) {
    lineWidth = event.detail.lineWidth;
  }

  function handleToggleEraser() {
    isErasing = !isErasing;
    color = isErasing ? "rgba(0,0,0,0)" : "#000000";
  }

  function clearCanvas() {
    if (canvasComponent) {
      canvasComponent.clearCanvas();
    }
  }
</script>

<link
  href="https://fonts.googleapis.com/css2?family=Indie+Flower&display=swap"
  rel="stylesheet"
/>

<main>
  <h1>Kayla's Art Studio</h1>
  <ColorPicker bind:color on:colorChange={handleColorChange} />
  <LineWidthSelector
    bind:lineWidth
    on:lineWidthChange={handleLineWidthChange}
  />
  <Controls on:clearCanvas={clearCanvas} on:toggleEraser={handleToggleEraser} />
  <Canvas bind:this={canvasComponent} {color} {lineWidth} {isErasing} />
</main>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  main {
    font-family: "Indie Flower", cursive;
    text-align: center;
    min-height: 100vh;
    width: 100%;
  }
</style>
