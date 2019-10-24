<script>
  let todos = [];
  let newTodo = "";

  function addTodo() {
    if (newTodo) {
      const todo = {
        done: false,
        text: newTodo,
        id: todos.length + 1
      };
      todos = [...todos, { ...todo }];
      newTodo = "";
    }
  }

  function removeTodo(todoId) {
    todos = todos.filter(({ id }) => id !== todoId);
  }

  function toggleTodo(todoId) {
    todos = todos.map(({ id, done, ...rest }) => ({
      ...rest,
      id,
      done: todoId === id ? !done : done
    }));
  }
</script>

<style>
  .container {
    height: 100%;
    width: 500px;
    margin: 0 auto;
  }

  ul {
    list-style-type: none;
  }

  .checked {
    text-decoration: line-through;
  }

  a {
    text-decoration: none;
  }
</style>

<div class="container">
  <p>Add Todo Lists</p>
  <form on:submit|preventDefault={addTodo}>
    <input
      type="text"
      aria-label="Enter a new todo item"
      placeholder="eg. gyms"
      bind:value={newTodo} />
  </form>
  <ul class="todo-list">
    {#each todos as todo (todo.id)}
      <li>
        <a href="javascript:void(0)" on:click={() => toggleTodo(todo.id)}>
          <span class={todo.done ? 'checked' : ''}>{todo.text}</span>
        </a>
        <button on:click={() => removeTodo(todo.id)}>&times;</button>
      </li>
    {/each}
  </ul>
</div>
