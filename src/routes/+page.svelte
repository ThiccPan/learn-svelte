<script lang="ts">
	import { json } from '@sveltejs/kit';
	import TodoItem from '../components/TodoItem.svelte';
	import type { Todo } from '../global';
	import { todoStore } from '../store/store';

	let todoList: Todo[] = [];
	let currId: number = 0;
	let inputTask: string = '';

	function addTodo() {
		todoList.push({
			task: inputTask,
			id: currId.toString()
		});
		currId++;
		todoList = todoList;
	}

	function deleteTodo(id: string) {
		console.log(id);
		todoList = todoList.filter((todo) => todo.id !== id);
	}

	function saveToStorage() {
		localStorage.setItem("data", JSON.stringify(todoList))
	}
</script>

<h1>Simple todo app</h1>
<form method="post" on:submit|preventDefault={() => addTodo()}>
	<input type="text" bind:value={inputTask} />
	<button type="submit">add</button>
	<button on:click={saveToStorage}>save to local storage</button>
</form>

<h2>List of todo</h2>
<ul>
	{#each todoList as todo}
		<li>
			<TodoItem todoData={todo} on:delete={() => deleteTodo(todo.id)} />
		</li>
	{/each}
</ul>
