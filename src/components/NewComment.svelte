<script>
    export let comment
</script>

<div class="comment">
    <h3>{ comment.time_ago } by { comment.user }</h3>
    {@html comment.content}
</div>

<style>
    .comment {
        border: 1px solid rgba(0, 0, 0, 0.205);
        margin-bottom: 10px;
        border-radius: 5px;
        padding: 10px;
    }

    h3 {
        margin-bottom: 5px;
    }
</style>