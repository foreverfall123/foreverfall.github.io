<script>
import { onMount } from 'svelte';

	import Input from './Input.svelte';
	import List from './List.svelte';

	let todo_list = [];
	let input_this;

	onMount(() => {
		todo_list = loadlistbycookie();
		input_this.focus();
	});

	// 해당 조건을 걸 경우 쿠키를 불러오기 전에 빈값으로 저장해버려서 불러오기 안댐
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

		savelistbycookie(todo_list);

		input_this.focus();
	}

	function delete_item(event){

		alert('해야 할 일 \'' + todo_list.filter((item) => item.id == event.detail.id)[0]['text'] + '\'이(가) 삭제되었습니다.');

		todo_list = todo_list.filter((item) => item.id != event.detail.id);

		savelistbycookie(todo_list);

		input_this.focus();
	}

	function savelistbycookie(value){
		console.log(JSON.stringify(value));
		let todayDate = new Date();
		todayDate.setDate(todayDate.getDate() + 30);
		
		document.cookie = 'sym_todolist=' + JSON.stringify(value) + '; path=/; expires=' + todayDate.toGMTString() + ';';
	}

	function loadlistbycookie(){
		return new RegExp('sym_todolist' + '=([^;]*)').test(document.cookie) ? JSON.parse(RegExp.$1) : [] ;
	}
</script>

<main>
	<div class='wrapper'>
		<div class='container'>
			<h1>To Do List</h1>
			<Input on:add_list={add_list} bind:input_this={input_this}/>
			<List {todo_list} on:delete_item={delete_item}/>
		</div>
	</div>
</main>

<style>
	main{
		height: 100%;
	}

	.wrapper{
		display: flex;
		justify-content: center;
		align-items: center;
		height: 100%;
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
</style>