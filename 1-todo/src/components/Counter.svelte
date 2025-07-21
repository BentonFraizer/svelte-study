<script>
  export let uncompletedTasks;
  export let tasks;
</script>

{#if uncompletedTasks !== 0}
  <span>Осталось {uncompletedTasks} из {tasks.length}</span>
{:else}
  <span>Все задачи завершены</span>
{/if}
