<script>
    export let data;
    export let updateTasks;
    import {createEventDispatcher} from 'svelte';

    const dispatch = createEventDispatcher();

    const handleDelete = (id) => {
        dispatch('delete', {id})
    }

</script>

<li>
    <input
            type="checkbox"
            id={data.id}
            name={data.title}
            bind:checked={data.done}
            on:click={() => updateTasks(data.id, !data.done)}
    />
    <label for={data.id} class:done={data.done}>
        {data.title}
    </label>

    {#if data.done}
        <button on:click={() => handleDelete(data.id)}>Удалить</button>
    {/if}
</li>

<style>
    .done {
        text-decoration: line-through;
    }

    li {
        list-style-type: none;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
</style>
