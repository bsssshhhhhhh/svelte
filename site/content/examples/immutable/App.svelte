<svelte:options immutable/>

<script>
	import ImmutableTodo from './ImmutableTodo.svelte';
	import MutableTodo from './MutableTodo.svelte';

	export let todos;

	function toggle(id) {
		todos = todos.map(todo => {
			if (todo.id === id) {
				// return a new object
				return {
					id,
					done: !todo.done,
					text: todo.text
				};
			}

			// return the same object
			return todo;
		});
	}
</script>

<h2>Immutable</h2>
{#each todos as todo}
	<label on:click="{() => toggle(todo.id)}">
		<span>{todo.done ? "😎": "☹️"}</span>
		<ImmutableTodo {todo}/>
	</label>
{/each}

<h2>Mutable</h2>
{#each todos as todo}
	<label on:click="{() => toggle(todo.id)}">
		<span>{todo.done ? "😎": "☹️"}</span>
		<MutableTodo {todo}/>
	</label>
{/each}
