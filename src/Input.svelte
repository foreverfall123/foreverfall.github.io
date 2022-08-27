<script>
    import { createEventDispatcher } from 'svelte';
    import { onMount } from 'svelte';
    const dispatch = createEventDispatcher();
    let input_val = '';
    let input_this;

    function add_list(){
        dispatch('add_list', {
            text: input_val
        });
        input_val = '';
        focus_input();
    }

    function keydown_event(event){
        if(event.keyCode === 13) add_list();
    }

    function focus_input(){
        input_this.focus();
    }

    onMount(() => input_this.focus());
</script>

<div class='input_div'>
    <input type="text" placeholder="할 일을 입력해주세요" bind:value={input_val} on:keydown={keydown_event} bind:this={input_this}/>
    <button on:click={add_list}>ADD</button>
</div>

<style>
    .input_div{
        display: flex;
    }

    .input_div input{
        flex-grow: 1;
        border-radius: 25px;
		box-shadow: 0px 0px 10px 5px rgb(233, 233, 233);
        border: none;
        margin-right: 10px;
    }

    .input_div input::placeholder{
        color:rgb(180, 180, 180);
    }

    .input_div button{
        background-color: rgb(89, 66, 189);
        color: white;
        padding: 0px 15px;
        border-radius: 25px;
		box-shadow: 10px 10px 10px rgb(233, 233, 233);
        border: none;
    }
</style>