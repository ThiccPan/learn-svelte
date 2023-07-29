<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	import type { Todo } from '../global';

	const dispatch = createEventDispatcher();
	export let todoData: Todo;
</script>

<div>
	{todoData.task}
	<button on:click={() => dispatch('delete')}>delete</button>
</div>
