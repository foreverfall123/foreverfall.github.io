<script>
    import Item from './Item.svelte';
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
    export let todo_list;

    function delete_item(event){
        dispatch('delete_item', {
            id: event.detail.id
        });
    }
</script>

{#each todo_list as item}
    <Item {item} on:delete_item={delete_item}/>
{/each}