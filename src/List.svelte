<script>
    import Item from './Item.svelte';
    export let todo_list;
</script>

{#each todo_list as item}
    <Item {item}/>
{/each}