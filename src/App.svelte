<script>
	import "bootstrap/dist/css/bootstrap.css";
	import { onMount } from "svelte";

	let stories = [];
	let currentItems = 1;
	let amount = 1;
	let countStories;

	async function getStories() {
		const res = await fetch("api/stories/all.json");
		stories = await res.json();
		countStories = stories.length
		// console.log(count)
		return stories;
	}

	function handleClick(amount) {
		console.log(stories);
		currentItems = currentItems + amount;
	}

</script>

<h1 class="display-1">Welcome!</h1>

{#if currentItems != 1}
	<button
		type="button"
		id="loadPrevious"
		class="btn btn-outline-primary"
		on:click={() => handleClick(-1)}
	>
		Vorige
	</button>
{:else}
	<button
		type="button"
		id="loadPreviousDeactive"
		class="btn btn-outline-disabled"
	>
		Vorige
	</button>
{/if}

{#if currentItems != countStories}
<button
	type="button"
	id="loadNext"
	class="btn btn-outline-primary"
	on:click={() => handleClick(1)}
>
	Volgende
</button>
{/if}

{#await getStories()}
	<p>loading</p>
{:then stories}
	<ul class="list-group">
		{#each stories.slice(currentItems - 1, currentItems) as story}
			<li class="list-group-item">{story.title}</li>
		{/each}
	</ul>
{:catch error}
	<p style="color: red">error</p>
{/await}
