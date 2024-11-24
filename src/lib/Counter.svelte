<script lang="ts">
  interface IAction {
    type: "decrement" | "increment";
    timestamp: number;
    previousValue: number;
    newValue: number;
  }

  let count: number = $state(0);
  let history: IAction[] = $state([]);

  const decrement = () => {
    count -= 1;
  }

  const increment = () => {
    count += 1;
  }
</script>

<p>{count}</p>

<button onclick={decrement}>
  Decrement
</button>
<button onclick={increment}>
  Increment
</button>


<style>
  p {
    font-size: 30px;
    color: black;
    font-weight: bold;
  }
</style>
