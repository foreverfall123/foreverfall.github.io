<script>
import { text } from 'svelte/internal';

	import Input from './Input.svelte';
	import List from './List.svelte';

	let todo_list = [{
		id: 1,
		text: '첫번째',
		isComplete: false,
	}];

	function add_list(event) {
		let new_item = {
			id: todo_list.length + 1,
			text: event.detail.text,
			isComplete: false,
		};
		todo_list[todo_list.length] = new_item;
		
	}

	function delete_item(event){
		todo_list = todo_list.filter((item) => item.id != event.detail.id);
	}
</script>

<main>
	<div>
		<p>To Do List</p>
		<Input on:add_list={add_list} />
		<List {todo_list} on:delete_item={delete_item}/>
	</div>
</main>