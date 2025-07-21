<script>
  let newTitle = '';
  export let addTask;
  $: isSubmitBtnDisabled = newTitle.length === 0;
</script>

<form
  on:submit|preventDefault={() => {
    addTask(newTitle);
    newTitle = '';
  }}
>
  <input type="text" name="newTitle" bind:value={newTitle} />
  <button type="submit" disabled={isSubmitBtnDisabled}>Добавить</button>
</form>

<style>
  form {
    display: flex;
    align-items: center;
    justify-content: space-evenly;
  }

  input {
    height: 32px;
    font-size: 16px;
    line-height: 1;
  }
</style>
