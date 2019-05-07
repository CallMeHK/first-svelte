<script>
  let list = [
    { id: 1, value: "beer" },
    { id: 2, value: "cheese" },
    { id: 3, value: "soup" }
  ];
  let id = 4;
  let todo = "";

  function submitTodo(e) {
    if (e.keyCode == 13 && todo !== "") {
      list = [{ id, value: todo }, ...list];
      todo = "";
      id += 1;
    }
  }

  function deleteTodo(todoId) {
    list = list.filter(elt => elt.id !== todoId);
  }
</script>

<div>
  <h3>Todos</h3>
  <div>
    <input
      bind:value={todo}
      on:keydown={submitTodo}
      placeholder="Enter a todo" />
  </div>
  <ul>
    {#each list as item (item.id)}
      <li>
        <span>{item.value}</span>
        <span style="cursor:pointer;" on:click={() => deleteTodo(item.id)}>
          [ delete ]
        </span>
      </li>
    {/each}
  </ul>
</div>
