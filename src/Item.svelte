<script>
    export let item;
</script>

<div>
    <input type="checkbox" bind:checked="{item.isComplete}">
    {item.id} {item.text}
    <button>x</button>
</div>