<script>
	import Story from "./Story.svelte";

	let stories = [];
	let title = "This isn't even my final form 🐲";
	let coverImage =
		"https://images.unsplash.com/photo-1522542550221-31fd19575a2d?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1950&q=80";

	async function getStories() {
		const res = await fetch("api/stories/all.json");
		stories = await res.json();
		stories = stories.reverse();
		return stories;
	}
</script>

<style>
	.title {
		font-size: 3.5rem;
    	font-weight: 300;
    	line-height: 1.2;
		text-align: center !important;
	}
</style>

<img
	src={coverImage}
	class="enough-space-for-picture rounded "
	alt="header_image by unsplash.com/@halacious" 
/>

<h1 class="title">{title}</h1>

<div />

{#await getStories()}
	<p>loading</p>
{:then stories}
	{#each stories as story}
		<Story title={story.title} content={story.content} />
	{/each}
{:catch error}
	<p style="color: red">error</p>
{/await}
