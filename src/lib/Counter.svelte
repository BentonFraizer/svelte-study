<script lang="ts">
  interface IAction {
    type: "decrement" | "increment";
    timestamp: number;
    previousValue: number;
    newValue: number;
  }

  let count: number = $state(0);
  let timestamp: number = $state(0);
  let history: IAction[] = $state([]);
  let lastHistoryActions: IAction[] = $derived(history.slice(-5).reverse());
  let average =  $derived(history.length > 0 ? history.reduce((acc, cur) => acc + cur.newValue, 0) / history.length : 0);

  const decrement = () => {
    count -= 1;
    history.push({
      type: "decrement",
      timestamp: timestamp,
      previousValue: history.length === 0 ? 0 : history[history.length - 1].newValue,
      newValue: count,
    })
    timestamp += 1;
  }

  const increment = () => {
    count += 1;
    history.push({
      type: "increment",
      timestamp: timestamp,
      previousValue: history.length === 0 ? 0 : history[history.length - 1].newValue,
      newValue: count,
    })
    timestamp += 1;
  }
</script>

<div class="controls">
  <p class="count">{count}</p>

  <button onclick={decrement}>
    Decrement
  </button>
  <button onclick={increment} style="margin-bottom: 20px">
    Increment
  </button>
  <hr />
  <p>Average value: {average.toFixed(2)}</p>
</div>


{#if lastHistoryActions.length > 0}
  <div class="history">
    <p>History</p>
    {#each lastHistoryActions as historyAction}
      <div>
        {history.indexOf(historyAction) + 1}.
        {#if historyAction.type === "increment"}
          <span class="green">Counter incremented: {historyAction.newValue}</span>
        {:else}
          <span class="red">Counter decremented: {historyAction.newValue}</span>
        {/if}
      </div>
    {/each}
  </div>
{/if}


<style>
  .controls {
    border:  5px solid #c9c9c9;
    border-radius: 15px;
    padding: 20px;
    margin-bottom: 20px;
  }

  .count {
    font-size: 30px;
    font-weight: bold;
  }

  .history  {
    border:  5px solid #c9c9c9;
    border-radius: 15px;
    padding: 0 30px;
    min-height: 223px;

    & p {
      font-size: 18px;
      font-weight: bold;
    }

    & div {
      text-align: left;
    }
  }

  span {
    font-weight: bold;

    &.green {
      color: #019a01;
    }

    &.red {
      color: red;
    }
  }
</style>
