<script>
    import Item from './Item.svelte';
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
    export let todo_list;
    let list_div = '';
    $: list_div = todo_list.length == 0 ? '' : 'list_div'

    function delete_item(event){
        dispatch('delete_item', {
            id: event.detail.id
        });
    }
</script>

<div class={list_div}>
    {#each todo_list as item}
        <Item {item} on:delete_item={delete_item}/>
    {:else}
        <p>{'할 일이 없습니다'}</p>
    {/each}
</div>

<style>
    .list_div{
        margin-top: 20px;
        border-radius: 25px;
		box-shadow: 0px 0px 10px 5px rgb(233, 233, 233);
        padding: 20px;
        max-height: 500px;
        overflow: auto;
    }
</style>
