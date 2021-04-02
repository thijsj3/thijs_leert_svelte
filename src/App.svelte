<script>
	import { onMount } from "svelte";
	import "bootstrap/dist/css/bootstrap.css";

	let stories = [];
	let currentItems = 1;
	let amount = 7;
	let countStories;
	let title = "This isn't even my final form 🐲";
	let coverImage = "https://images.unsplash.com/photo-1522542550221-31fd19575a2d?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1950&q=80"

	async function getStories() {
		const res = await fetch("api/stories/all.json");
		stories = await res.json();
		countStories = stories.length;
		// console.log(count)
		return stories;
	}

	function handleClick(amount) {
		console.log(stories);
		currentItems = currentItems + amount;
	}
</script>

<img
	src={coverImage}
	class="enough-space rounded "
	alt="header_image by unsplash.com/@halacious"
/>

<h1 class="display-4 text-center">{title}</h1>

<div />

{#await getStories()}
	<p>loading</p>
{:then stories}
		{#each stories as story}
			<div class="card mb-3 text-center">
					<h2 class="card-title">{story.title}</h2>
					<p class="card-text">{story.content}</p>
			</div>
		{/each}
{:catch error}
	<p style="color: red">error</p>
{/await}
