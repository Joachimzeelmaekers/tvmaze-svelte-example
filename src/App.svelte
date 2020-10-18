<script>
	import { onMount } from "svelte";
	const url = "https://random.dog/woof.json"; // https://github.com/public-apis/public-apis

	let dogs = [];

	const amountOfCalls = [...Array(21).keys()].slice(1);

	onMount(async () => {
		dogs = await Promise.all(
			amountOfCalls.map(async (key) => {
				console.log(key);
				const res = await fetch(url);
				return res.json();
			})
		);
	});
</script>

<style>
	.dogs {
		width: 100%;
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		grid-gap: 8px;
	}

	figure,
	img {
		width: 100%;
		height: 100%;
		margin: 0;
		object-fit: contain;
	}

	figure {
		box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
	}
</style>

<main>
	<h1>What makes you happy?</h1>

	<div class="dogs">
		{#each dogs as dog}
			<figure class="shadow-xs">
				<img src={dog.url} alt={"Image not found, sorry!"} />
				<!-- <figcaption>{dog.name}</figcaption> -->
			</figure>
		{:else}
			<!-- this block renders when dogs.length === 0 -->
			<p>let me think...</p>
		{/each}
	</div>

</main>
