<script>
  import Task from './Task.svelte';
  export let tasks;
  export let updateTasks;
</script>

<ul>
  {#each tasks as task (task.id)}
    <Task
      data={task}
      {updateTasks}
      on:delete
    />
  {/each}
</ul>

<style>
  ul {
    padding: 0;
    text-align: start;
    max-width: 600px;
    width: 100%;
  }
</style>
