<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  let color = "#000000";

  function handleChange(event) {
    color = event.target.value;
    dispatch("colorChange", { color });
  }
</script>

<label for="color-picker">Color:</label>
<input type="color" id="color-picker" value={color} on:change={handleChange} />

<style>
  input[type="color"] {
    cursor: pointer;
  }
</style>
