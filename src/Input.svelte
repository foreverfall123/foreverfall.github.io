<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
    let input_val;

    function add_list(){
        dispatch('add_list', {
            text: input_val
        });
        input_val = '';
    }
</script>

<div>
    <input type="text" bind:value={input_val} />
    <button on:click={add_list}>ADD</button>
</div>