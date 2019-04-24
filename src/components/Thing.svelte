<script>
    import { fade, fly } from "svelte/transition";
    export let thing = null;
    export let index = 0;
    export let onRemove = () => {};
</script>
<style>
  span.bold {
    font-weight: bold;
  }
  li.thing {
    background-color: #eeeeee;
    margin-top: 5px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border: solid 4px white;
    border-radius: 2px;
  }
  .thingy {
    margin-left: 5px;
  }
  .button {
    margin-top: 5px;
    margin-right: 5px;
  }
</style>

<li class="thing" in:fly={{ y: -100 * (index + 1), duration: 1000 }} out:fly={{ x: 300, duration: 500 }}>
    <span class="thingy">{thing}</span>
    <button class="button bold" on:click={onRemove}>x</button>
</li>

