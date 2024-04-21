<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  export let lineWidth = 5;

  function handleChange(event) {
    lineWidth = parseFloat(event.target.value);
    dispatch("lineWidthChange", { lineWidth });
  }
</script>

<div class="line-width-selector">
  <label for="line-width-slider" class="line-width-label">Line Width:</label>
  <input
    class="line-width-slider"
    type="range"
    id="line-width-slider"
    min="1"
    max="20"
    bind:value={lineWidth}
    on:change={handleChange}
  />
</div>

<style>
  .line-width-selector {
    display: flex;
    align-items: center;
    justify-content: center;
    margin: auto;
    gap: 1rem;
  }
</style>
