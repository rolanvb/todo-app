<script>
	let { children } = $props();
</script>


<header>
    <h1 class="pageTitle">
        To Do App
    </h1>
</header>

{@render children()}

<style>
    header {
        background-color: #2a31fb;
        color: white;
        padding: 1rem;
        margin: none;
        margin-bottom: 1rem;
        width: 100%;
    }

    .pageTitle {
        font-weight: bolder;
    }
</style>