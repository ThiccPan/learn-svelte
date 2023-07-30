<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	import type { Todo } from '../global';

	const dispatch = createEventDispatcher();
	export let todoData: Todo;

	function doneAction() {
		todoData.isDone = !todoData.isDone;
		dispatch('done');
	}
</script>

<div>
	<span class={todoData.isDone === true ? 'crossed' : ''}>{todoData.task}</span>
	<button on:click={() => doneAction()}>done</button>
	<button on:click={() => dispatch('delete')}>delete</button>
</div>

<style>
	.crossed {
		text-decoration: line-through;
	}
</style>
