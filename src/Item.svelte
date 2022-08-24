<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
    export let item;

    function delete_item(){
        console.log(item.id);
        dispatch('delete_item', {
            id: item.id
        });
    }
</script>

<div>
    <input type="checkbox" bind:checked="{item.isComplete}">
    {item.id} {item.text}
    <button on:click={delete_item}>x</button>
</div>