<script>
  import AddForm from './components/AddForm.svelte';
  import Counter from './components/Counter.svelte';
  import Filter from './components/Filter.svelte';
  import TasksList from './components/TasksList.svelte';

  let filterValue = 'all';

  let tasks = [
    {
      id: 1,
      title: 'Забрать заказ в яндекс маркет',
      done: false,
    },
    {
      id: 2,
      title: 'Сходить в перекрёсток за продуктами',
      done: true,
    },
    {
      id: 3,
      title: 'Провести немного времени на свежем воздухе',
      done: false,
    },
  ];

  let filteredTasks = tasks;

  $: if (filterValue === 'all') {
    filteredTasks = tasks;
  } else if (filterValue === 'done') {
    filteredTasks = tasks.filter((task) => task.done === true);
  } else {
    filteredTasks = tasks.filter((task) => task.done === false);
  }

  const updateTasks = (id, done) => {
    tasks = tasks.map((todo) => {
      if (todo.id === id) {
        todo.done = done;
      }
      return todo;
    });
  };

  const addTask = (title) => {
    tasks.unshift({
      id: tasks.length + 1,
      done: false,
      title: title,
    });

    tasks = tasks;
  };

  $: uncompletedTasks = tasks.filter((todo) => todo.done === false).length;
</script>

<main>
  <h1>Todo list</h1>

  <Filter bind:filterValue />

  <AddForm {addTask} />

  <TasksList tasks={filteredTasks} {updateTasks} />

  <Counter {uncompletedTasks} {tasks} />
</main>
