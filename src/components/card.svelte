<script>
    import Star from "./star.svelte";

    export let show = {};
    const placeFiller = "...";
    const { image, name: title, rating, summary, genres, officialSite } = show;
    const shortSummary = summary.slice(0, 100) + placeFiller;

    let showFullDescription = false;

    const amountOfFilledStars = Math.round(rating.average  / 2);
    console.log(amountOfFilledStars);
    const stars = [
        ...new Array(amountOfFilledStars).fill(1),
        ...new Array((5 - amountOfFilledStars)).fill(0),
    ];

    function toggleShowFullDescription() {
        showFullDescription = !showFullDescription;
    }

    function navigateToUrl() {
        window.open(officialSite, "_blank");
    }
</script>

<style>
    .image {
        max-height: 200px;
        object-fit: contain;
    }
</style>

<div class="w-1/4 p-2">
    <div
        class="container rounded overflow-hidden shadow-lg hover:shadow-2xl cursor-pointer pt-1">
        <img
            class="w-full image"
            src={(image || {}).medium}
            height="100"
            alt={title}
            on:click={navigateToUrl} />
        <div class="px-6 py-4">
           
            <div class="font-bold text-l mb-2">
                {title}
            </div>
           
            <p class="text-gray-700 text-base">
                {#if !showFullDescription}
                    {@html shortSummary}
                {:else}
                    {@html summary}
                {/if}
            </p>
            <a
                href="/"
                on:click={toggleShowFullDescription}
                class="my-6 text-blue-500 hover:text-blue-800">
                {#if !showFullDescription}
                    Show full description
                {:else}Hide full description{/if}
            </a>
            <div class="flex items-center mt-1">
                {#each stars as star}
                    <Star filled={star} />
                {/each}
            </div>
        </div>
        
        <div class="px-6 pt-4 pb-2">
            {#each genres as genre}
                <span
                    class="inline-block bg-gray-200 rounded-full px-3 py-1 text-xs font-semibold text-gray-700 mr-1 mb-1">{genre}</span>
            {/each}
        </div>
    </div>
</div>
