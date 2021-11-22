<svelte:head>
    <title>Hacker News</title>
</svelte:head>

<script>
    import NewPreview from '../components/NewPreview.svelte'
    let page = 1

    const fetchNews = async () => {
		return await fetch(`https://node-hnapi.herokuapp.com/news?page=${page}`)
            .then(r => r.json())
	}

    let promise = fetchNews()

    const nextPage = () => {
        page += 1

        promise = fetchNews()
    }

    const previousPage = () => {
        page -= 1

        promise = fetchNews()
    }
</script>

{#await promise}
	<p>...waiting for news</p>
{:then news}
    <div class="news">
        {#each news as onlyNew}
            <NewPreview {onlyNew} />
        {/each}
    </div>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}

<div class="buttons">
    {#if page > 1}
        <button on:click={previousPage} >Previous Page</button>
    {/if}

    <button on:click={nextPage} >Next Page</button>
</div>

<style>
    .news {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        width: 100%;
        padding: 10px;
        grid-gap: 10px;
    }

    @media (max-width: 700px) {
        .news {
            grid-template-columns: 1fr;
        }
    }

    .buttons {
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 50px;
    }

    .buttons button {
        margin: 5px;
        padding: 5px;
        border: none;
        outline: none;
        cursor: pointer;
        font-size: 20px;
        background: #035f94;
        color: #fff;
        border-radius: 2px;
    }
</style>