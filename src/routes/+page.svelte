<script lang="ts">
	import { todoStore } from '../store/store';

	let todoList: String[] = [];
	let inputTodo: string = '';

	function addTodo() {
		todoList.push(inputTodo);
		todoList = todoList;
		console.log(todoList);
	}
</script>

<h1>Simple todo app</h1>
<form method="post" on:submit|preventDefault={() => addTodo()}>
	<input type="text" bind:value={inputTodo} />
	<button type="submit">add</button>
</form>

<h2>List of todo</h2>
<ul>
	{#each todoList as todo}
		<li>
			{todo}
		</li>
	{/each}
</ul>
