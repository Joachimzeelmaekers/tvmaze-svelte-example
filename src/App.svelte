<script>
	import { onMount } from "svelte";

	const BASE_URL = "http://api.tvmaze.com"; // https://github.com/public-apis/public-apis

	import Nav from "./components/nav.svelte";
	import Card from "./components/card.svelte";
	import Search from "./components/search.svelte";
	import Loader from "./components/loader.svelte";

	let shows = [];
	let isLoading = false;

	async function fetchShows(urlToFetch) {
		isLoading = true;
		const result = await fetch(urlToFetch);
		const value = await result.json();
		isLoading = false;
		return value;
	}

	onMount(async () => {
		shows = await fetchShows(BASE_URL + "/shows");
	});

	async function handleSearch(event) {
		let query = `${BASE_URL}/search/shows?q=${event.detail.value}`;
		const result = await fetchShows(query);
		shows = result.map((match) => match.show);
	}
</script>

<main>
	<Nav />
	<header class="bg-white flex justify-between align-center">
		<div class="max-w-7xl py-6 px-4 sm:px-6 lg:px-8">
			<h1 class="text-3xl font-bold leading-tight text-gray-900">
				Series
			</h1>
		</div>
		{#if !isLoading}
			<Search on:search={handleSearch} />
		{/if}
	</header>
	{#if !isLoading}
		<body class="antialiased font-sans flex flex-wrap mb-4">
			{#each shows as show (show.id)}
				<Card {show} />
			{/each}
		</body>
	{:else}
		<Loader />
	{/if}
</main>
