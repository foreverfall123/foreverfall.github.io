<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
    export let item;
    let style = '';

    $: style = item.isComplete ? 'text-decoration: line-through' : '';

    function delete_item(){
        console.log(item.id);
        dispatch('delete_item', {
            id: item.id
        });
    }
</script>

<div>
    <input type="checkbox" bind:checked="{item.isComplete}">
    <span {style}>{item.id} {item.text}</span>
    <button on:click={delete_item}>x</button>
</div>