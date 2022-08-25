<script>
	import Input from './Input.svelte';
	import List from './List.svelte';

	let todo_list = [];

	function add_list(event) {
		let text = event.detail.text.trim();
		if(text == ''){
			alert("해야 할 일은 비어있을 수 없습니다.");
			return false;
		}

		let last_id = todo_list.length == 0 ? 0 : todo_list[todo_list.length - 1]['id'] + 1;

		let new_item = {
			id: last_id,
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