<script>
  import TodoItem from "./TodoItem.svelte";

  let newTodoTitle = "";
  let currentFilter = "all";
  let nextId = 4;

  let todos = [
    {
      id: 1,
      title: "My first todo",
      completed: false
    },

    {
      id: 2,
      title: "My second todo",
      completed: false
    },

    {
      id: 3,
      title: "My third todo",
      completed: false
    }
  ];

  function addToDo(event) {
    if (event.key === "Enter") {
      todos = [
        ...todos,
        {
          id: nextId,
          completed: false,
          title: newToDoTitle
        }
      ];

      nextId = nextId + 1;
      newTodoTitle = "";
    }
  }

  $: todosRemaining = filteredTodos.filter(todos => !todo.completed).length;
  $: filteredTodos =
    currentFilter === "all"
      ? todos
      : currentFilter === "completed"
      ? todos.filter(todo => todo.completed)
      : todos.filter(todo => !todo.completed);

  function checkAllToDos(event) {
    todos.forEach(todo => (todo.completed = event.target.checked));
    // updating todos
    todos = todos;
  }

  function updateFilter(newFilter) {
    currentFilter = newFilter;
  }

  function clearCompleted() {
    todos = todos.filter(todo => !todo.completed);
  }

  function handleDeleteTodo(event) {
    todos = todos.filter(todos => todo.id !== event.detail.id);
  }
</script>

<!-- add templatecode -->

<div class="container">
  <h2>Svelte Todo App</h2>
  <input
    type="text"
    class="todo-input"
    placeholder="Insert todo item..."
    bind:value{newTodoTitle}
    on:
    keydown={addToDo} />

  {#each filteredTodos as todo}
    <div class="todo-item">
      <TodoItem
        {...todo}
        on:deleteTodo={handleDeleteTodo}
        on:toggleComplete={handleToggleComplete} />
    </div>
  {/each}

  <div class="inner-containe">
    <div>
      <label>
        <input
          class="inner-container-input"
          type="checkbox"
          on:change={checkAllToDos} />
        CheckAll
      </label>
    </div>
    <div>{todosRemaining}items left</div>
  </div>
  <div class="inner-container">
    <div>
      <button
        on:click={() => updateFilter('all')}
        class:active={currentFilter === 'all'}>
        All
      </button>
      }>
      <button
        on:click={() => updateFilter('active')}
        class:active={currentFilter === 'active'}>
        Active
      </button>
      }>
      <button
        on:click={() => updateFilter('completed')}
        class:active={currentFilter === 'completed'}>
        All
      </button>
      }>
    </div>
    <div>
      <button on:click={clearCompleted}>Clear Completed</button>

    </div>

  </div>
</div>
