<script>
	import "bootstrap/dist/css/bootstrap.css";
	import { onMount } from "svelte";

	let stories = [];
	let currentItems = 1;
	let amount = 7;
	let countStories;
	let title = "A Thijs website"
	let subtitle = "This isn't even my final form 🐲";

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

<div class="jumbotron jumbotron-fluid">
	<div class="container">
		<h1 class="display-4">{title}</h1>
		<p class="lead">
			{subtitle}
		</p>
	</div>
</div>

{#await getStories()}
	<p>loading</p>
{:then stories}
	<div class="card-columns">
		{#each stories as story}
			{#if story.image && story.title}
				<div class="card">
					<img
						src={story.image}
						class="card-img-top"
						object-fit="cover"
						width="100%"
						height="200rem"
						alt={story.imageAuthor}
					/>
					<div class="card-body">
						<h5 class="card-title">{story.title}</h5>
						<p class="card-text">{story.content}</p>
					</div>
				</div>
			{:else if story.image}
				<div class="card">
					<img
						src={story.image}
						class="card-img-top"
						object-fit="cover"
						width="100%"
						height="200rem"
						alt={story.imageAuthor}
					/>
				</div>
			{:else if story.title}
				<div class="card">
					<div class="card-body">
						<h5 class="card-title">{story.title}</h5>
						<p class="card-text">{story.content}</p>
					</div>
				</div>
			{/if}
		{/each}
	</div>
{:catch error}
	<p style="color: red">error</p>
{/await}
