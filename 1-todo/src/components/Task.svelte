<script>
  export let data;
  export let updateTasks;
</script>

<li class:done={data.done}>
  <input
    type="checkbox"
    id={data.id}
    name={data.title}
    bind:checked={data.done}
    on:click={() => updateTasks(data.id, !data.done)}
  />
  <label for={data.id}>
    {data.title}
  </label>
</li>

<style>
  .done {
    text-decoration: line-through;
  }

  li {
    list-style-type: none;
  }
</style>
