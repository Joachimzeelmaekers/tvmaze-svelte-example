<script>
	import { onMount } from "svelte";

	const url = "http://api.tvmaze.com/shows"; // https://github.com/public-apis/public-apis

	import Nav from "./components/nav.svelte";
	import Card from "./components/card.svelte";
	import Search from "./components/search.svelte";

	let shows = [];

	const defaultShow = {
		id: 1,
		url: "http://www.tvmaze.com/shows/1/under-the-dome",
		name: "Under the Dome",
		type: "Scripted",
		language: "English",
		genres: ["Drama", "Science-Fiction", "Thriller"],
		status: "Ended",
		runtime: 60,
		premiered: "2013-06-24",
		officialSite: "http://www.cbs.com/shows/under-the-dome/",
		schedule: {
			time: "22:00",
			days: ["Thursday"],
		},
		rating: {
			average: 6.5,
		},
		weight: 97,
		network: {
			id: 2,
			name: "CBS",
			country: {
				name: "United States",
				code: "US",
				timezone: "America/New_York",
			},
		},
		webChannel: null,
		externals: {
			tvrage: 25988,
			thetvdb: 264492,
			imdb: "tt1553656",
		},
		image: {
			medium:
				"http://static.tvmaze.com/uploads/images/medium_portrait/81/202627.jpg",
			original:
				"http://static.tvmaze.com/uploads/images/original_untouched/81/202627.jpg",
		},
		summary:
			"<p><b>Under the Dome</b> is the story of a small town that is suddenly and inexplicably sealed off from the rest of the world by an enormous transparent dome. The town's inhabitants must deal with surviving the post-apocalyptic conditions while searching for answers about the dome, where it came from and if and when it will go away.</p>",
		updated: 1573667713,
		_links: {
			self: {
				href: "http://api.tvmaze.com/shows/1",
			},
			previousepisode: {
				href: "http://api.tvmaze.com/episodes/185054",
			},
		},
	};
		
	 shows.push(defaultShow);
	 shows.push(defaultShow);
	 shows.push(defaultShow);
	 shows.push(defaultShow);
	 shows.push(defaultShow);
	 shows.push(defaultShow);

	
	onMount(async () => {
//   const result = await fetch(url);
//   shows = await result.json();
//   console.log(shows);
	});
</script>

<main>
	<Nav />
	<header class="bg-white flex justify-between">
		<div class="max-w-7xl py-6 px-4 sm:px-6 lg:px-8">
			<h1 class="text-3xl font-bold leading-tight text-gray-900">
				Series
			</h1>
		</div>
		<Search />
	</header>
	<body class="antialiased font-sans flex flex-wrap mb-4">
		{#each shows as show}
			<Card show={show}/>
		{/each}
	</body>
</main>
