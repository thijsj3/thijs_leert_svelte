<script>
    import marked from "marked";
    export let title;
    export let content;
</script>

<div class="box">
    <div>
        <h2>{title}</h2>
        <p >{@html marked(content)}</p>
    </div>
</div>

<style>
    .box {
        box-sizing: border-box;
        width: 300px;
        border: 1px solid #aaa;
        border-radius: 2px;
        box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.1);
        padding: 1em;
        margin: 0 0 1em 0;
        object-fit: cover;
        width: 100%;
    }
</style>
