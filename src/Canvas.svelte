<script lang="ts">
  import { onMount, afterUpdate } from "svelte";
  export let color: string = "#000000";
  export let lineWidth: number = 5;
  export let isErasing: boolean = false;

  let canvas: HTMLCanvasElement;
  let ctx: CanvasRenderingContext2D;

  let drawing = false;

  function startDrawing(event: MouseEvent) {
    const pos = getMousePos(canvas, event);
    drawing = true;
    ctx.beginPath();
    ctx.moveTo(pos.x, pos.y);
  }

  function draw(event: MouseEvent) {
    if (!drawing) return;
    const pos = getMousePos(canvas, event);
    ctx.lineTo(pos.x, pos.y);
    ctx.stroke();
  }

  function stopDrawing() {
    if (drawing) {
      ctx.closePath();
      drawing = false;
    }
  }

  function getMousePos(canvasElement: HTMLCanvasElement, event: MouseEvent) {
    const rect = canvasElement.getBoundingClientRect();
    return {
      x: event.clientX - rect.left,
      y: event.clientY - rect.top,
    };
  }

  function clearCanvas() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
  }

  onMount(() => {
    ctx = canvas.getContext("2d") as CanvasRenderingContext2D;
    updateCanvasSettings();
  });

  afterUpdate(updateCanvasSettings);

  function updateCanvasSettings() {
    if (ctx) {
      ctx.globalCompositeOperation = isErasing
        ? "destination-out"
        : "source-over";
      ctx.strokeStyle = color;
      ctx.lineWidth = lineWidth;
      if (isErasing) {
        ctx.strokeStyle = "rgba(255,255,255,1)";
      }
    }
  }

  export { clearCanvas };
</script>

<canvas
  bind:this={canvas}
  width="800"
  height="600"
  on:mousedown={startDrawing}
  on:mousemove={draw}
  on:mouseup={stopDrawing}
  on:mouseleave={stopDrawing}
  style="border: 1px solid black; display: block; margin: 20px auto; background-color: white;"
>
</canvas>

<style>
  canvas {
    border: 1px solid black;
    display: block;
    margin: 20px auto;
    background-color: white;
  }
</style>
