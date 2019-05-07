<script>
  import Counter from "./comps/Counter.svelte";
  import MagicApi from "./comps/MagicApi.svelte";
  import Todos from "./comps/Todos.svelte";
  import setUpRouter from "./router.js";
  // Route function to pass to setuprouter
  let page = "home";
  function updatePage(newPage) {
    page = newPage;
  }
  const routes = {
    "": function() {
      return updatePage("home");
    },
    counter: function() {
      return updatePage("counter");
    },
    magic: function() {
      return updatePage("magic");
    },
    todos: function() {
      return updatePage("todos");
    }
  };

  // Sets up router
  setUpRouter(routes, () => updatePage("error"));

  export let name;
</script>

<style>
  h1 {
    color: purple;
  }
</style>

<div>
  <h1>Hello {name}!</h1>
  <div>-----------------------------------</div>
  <ul>
    <li>
      <a href="./#/">HOME</a>
    </li>
    <li>
      <a href="./#/counter">COUNTER</a>
    </li>
    <li>
      <a href="./#/todos">TODOS</a>
    </li>
    <li>
      <a href="./#/magic">MAGIC API</a>
    </li>
  </ul>
  <div>-----------------------------------</div>
  <div>
    {#if page === 'home'}
      <h3>Home</h3>
    {:else if page === 'counter'}
      <Counter />
    {:else if page === 'todos'}
      <Todos />
    {:else if page === 'magic'}
      <MagicApi />
    {:else}
      <h3>Error</h3>
    {/if}
  </div>
</div>
