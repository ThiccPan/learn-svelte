<script lang="ts">
	import { onMount } from 'svelte';
	export const ssr = false;
	import TodoItem from '../components/TodoItem.svelte';
	import type { Todo } from '../global';
	import { todoStore } from '../store/store';

	let todoList: Todo[] = [];
	$: currId = 0;
	let inputTask: string = '';

	function addTodo() {
		todoList.push({
			task: inputTask,
			isDone: false,
			id: currId.toString(),
		});
		currId++;
		todoList = todoList;
	}

	function deleteTodo(id: string) {
		console.log(id);
		todoList = todoList.filter((todo) => todo.id !== id);
	}

	function saveToStorage() {
		localStorage.setItem('data', JSON.stringify(todoList));
	}

	onMount(loadData)

	function loadData() {
		let data = localStorage.getItem('data');
		if (typeof data === "string") {
			let parsed = JSON.parse(data)
			todoList = parsed!
			currId = parseInt(todoList[todoList.length-1].id)
			console.log(todoList)
		}
	}
</script>

<h1>Simple todo app</h1>
<form method="post" on:submit|preventDefault={() => addTodo()}>
	<input type="text" bind:value={inputTask} />
	<button type="submit">add</button>
</form>
<button on:click={saveToStorage}>save</button>
<button on:click={loadData}>load</button>

<h2>List of todo</h2>
<ul>
	{#each todoList as todo}
		<li>
			<TodoItem todoData={todo} on:delete={() => deleteTodo(todo.id)} />
		</li>
	{/each}
</ul>
