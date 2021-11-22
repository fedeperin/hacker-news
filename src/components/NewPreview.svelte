<script>
    export let onlyNew

    if(onlyNew.points == null) {
        onlyNew.points = 0
    }
</script>

<div class="new">
    <a href={ `./${ onlyNew.id }` }><h2>{ onlyNew.title }</h2></a>
    <p class="time-ago">{ onlyNew.time_ago }</p>

    <div class="comments-points">
        {#if onlyNew.comments_count !== 0}
            <div class="comments">
                <i class='bx bxs-comment' style='color:#ffffff'></i>
                <p>{onlyNew.comments_count}</p>
            </div>
        {/if}

        {#if onlyNew.points !== 0}
            <div class="points">
                <i class='bx bxs-heart' style='color:#9c0303' ></i>
                <p>{onlyNew.points}</p>
            </div>
        {/if}
    </div>
</div>

<style>
    .new {
        background: #111;
        padding: 10px;
        border-radius: 3px;
    }

    .new * {
        color: #fff;
    }

    a {
        text-decoration: none;
    }

    .time-ago {
        color: #ffffffb7;
    }

    .comments-points {
        margin-top: 10px;
        display: flex;
        align-items: center;
    }

    .comments-points p {
        margin-left: 5px;
    }

    .comments, .points {
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .points {
        margin-left: 10px;
    }
</style>