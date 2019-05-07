<script>
  export let count = 0;
  $: squared = count * count;
</script>

<div>
  <p>The count is currently {count}</p>
  <p>The count squared is {squared}</p>
  <div>
    <button on:click={() => (count = count + 1)}>Increase the count!</button>
  </div>
</div>
