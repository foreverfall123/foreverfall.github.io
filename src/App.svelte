<script>
import { escape } from 'svelte/internal';
import { onMount } from 'svelte';

	import Input from './Input.svelte';
	import List from './List.svelte';

	let todo_list = [];

	// onMount(() => {todo_list = loadlistbycookie(); console.log(todo_list)});

	// $: savelistbycookie(todo_list);

	function add_list(event) {
		let text = event.detail.text.trim();
		if(text == ''){
			alert("해야 할 일은 비어있을 수 없습니다.");
			return false;
		}

		alert('해야 할 일 \'' + text + '\'이(가) 추가되었습니다.');

		let last_id = todo_list.length == 0 ? 0 : todo_list[todo_list.length - 1]['id'] + 1;

		let new_item = {
			id: last_id,
			text: event.detail.text,
			isComplete: false,
		};
		todo_list[todo_list.length] = new_item;
	}

	function delete_item(event){

		alert('해야 할 일 \'' + todo_list.filter((item) => item.id == event.detail.id)[0]['text'] + '\'이(가) 삭제되었습니다.');

		todo_list = todo_list.filter((item) => item.id != event.detail.id);

		Input.fucus_input();
	}

	// function savelistbycookie(value){
	// 	console.log(value);
	// 	let todayDate = new Date();
	// 	todayDate.setDate(todayDate.getDate() + 30);
		
	// 	document.cookie = 'sym_todolist=' + value + '; path=/; expires=' + todayDate.toGMTString() + ';';
	// }

	// function loadlistbycookie(){
	// 	return new RegExp('sym_todolist' + '=([^;]*)').test(document.cookie) ? RegExp.$1 : [] ;
	// }
</script>

<main>
	<div class='wrapper'>
		<div class='container'>
			<h1>To Do List</h1>
			<Input on:add_list={add_list} />
			<List {todo_list} on:delete_item={delete_item}/>
		</div>
	</div>
</main>

<style>
	.wrapper{
		display: flex;
		justify-content: center;
		align-items: center;
		min-height: 100vh;
	}

	.container{
		width: 300px;
		padding: 40px;
		background-color: white;
		border-radius: 25px;
		box-shadow: -10px -10px 10px rgb(233, 233, 233) inset;

	}

	h1{
		font-size: 45px;
	}

	/* main :global() {
		background-image: url('/src/background.jpg');
		background-repeat: no-repeat;
		background-size: cover;
	} */
</style>