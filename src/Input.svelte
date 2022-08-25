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

    function keydown_event(event){
        if(event.keyCode === 13) add_list();
    }
</script>

<div>
    <input type="text" bind:value={input_val} on:keydown={keydown_event}/>
    <button on:click={add_list}>ADD</button>
</div>