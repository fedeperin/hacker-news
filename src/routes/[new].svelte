<script context="module">
    export async function load(ctx) {
        let newId = ctx.page.params.new
        return { props: { newId }}
    }
</script>


<script>
    import NewComment from '../components/NewComment.svelte'
    export let newId
    let newTitle = ''
    let newContent = ''

    const fetchNews = async () => {
        return await fetch(`https://node-hnapi.herokuapp.com/item/${newId}`)
        .then(r => r.json())
        .then(r => {
            newContent = r.content ? r.content : ''
            newTitle = `${r.title} -`
            return r
        })
    }
    
    let promise = fetchNews()
</script>

<svelte:head>
    <title>{newTitle} Hacker News</title>
</svelte:head>

{#await promise}
    Waiting for the new...
{:then newData}

    {#if newData.type == 'link'}
         <a href={ newData.url } target="_blank" class="title"><h1>{ newData.title }</h1></a>
         <p class="user">by { newData.user }</p>
         <p class="from">from { newData.domain }</p>
     
         <div class="points">
             <i class='bx bxs-heart' style='color:#9c0303' ></i>
             <p>{newData.points}</p>
         </div>
     
         <p class="new-content">{@html newContent}</p>
     
         <h2>{ newData.comments_count } Comments</h2>
     
         <div class="comments">
             {#each newData.comments as comment}
                 <NewComment {comment} />
             {/each}
         </div>
    {:else if newData.type == 'comment'}
        <NewComment comment={newData} />

    {:else if newData.type == 'job'}
        <a href={ newData.url } target="_blank" class="title"><h1>{ newData.title }</h1></a>
        <p>This is a job opportunity</p>
        <p class="from">from { newData.domain }</p>

        <p class="new-content">{@html newContent}</p>
    {:else if newData.type == 'ask'}
        <h1>{ newData.title }</h1>

        <p class="new-content">{@html newContent}</p>

        <h2>{ newData.comments_count } Comments</h2>
     
         <div class="comments">
             {#each newData.comments as comment}
                 <NewComment {comment} />
             {/each}
         </div>
    {/if}

{:catch error}
    <p style="color: red">{error.message}</p>
{/await}

<style>
    .title {
        color: #000;
    }

    .title h1 {
        margin-bottom: 10px;
    }

    .from {
        margin-top: 5px;
    }

    .points {
        margin-bottom: 50px;
        display: flex;
        align-items: center;
        margin-top: 5px;
    }

    .points p {
        margin-left: 5px;
    }

    h2 {
        margin-bottom: 30px;
    }

    .comments {
        display: flex;
        flex-direction: column;
    }

    .new-content {
        margin-bottom: 50px;
    }
</style>

