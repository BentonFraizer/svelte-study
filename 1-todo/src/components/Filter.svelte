<script>
  export let filterValue;
</script>

<div>
  <span>Отфильтровать:</span>
  <select name="filter" id="filter" bind:value={filterValue}>
    <option value="all">Все</option>
    <option value="done">Завершённые</option>
    <option value="undone">Незавершённые</option>
  </select>
</div>

<style>
  select {
    margin: 20px 0;
  }
</style>
