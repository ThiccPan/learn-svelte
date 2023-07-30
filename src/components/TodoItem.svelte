<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	import type { Todo } from '../global';

	const dispatch = createEventDispatcher();
	export let todoData: Todo;

	function updateDone() {
		todoData.isDone = !todoData.isDone;
		dispatch('done');
	}

	let updateTaskInput: string = '';
	function updateTask() {
		console.log('task updated');
		todoData.task = updateTaskInput;
		updateTaskInput = '';
		if (todoData.isDone) {
			todoData.isDone = false;
		}
	}
</script>

<div class="mb-2">
	<span class={todoData.isDone === true ? 'crossed' : ''}>{todoData.task}</span>
	<br />
	<button on:click={() => updateDone()}>done</button>
	<button on:click={() => dispatch('delete')}>delete</button>
</div>
<div class="mb-3">
	<form action="post" on:submit|preventDefault={updateTask}>
		<input type="text" name="update" id="update" bind:value={updateTaskInput} />
		<button type="submit">update</button>
	</form>
</div>

<style>
	.crossed {
		text-decoration: line-through;
	}

	.mb-2 {
		margin-bottom: 8px;
	}

	.mb-3 {
		margin-bottom: 12px;
	}
</style>
