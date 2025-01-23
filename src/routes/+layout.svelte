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
        background-color: #3135b3;
        color: #f9f9f9;
        padding: 1rem;
        margin: none;
        margin-bottom: 1rem;
        width: 100%;
    }

    .pageTitle {
        font-weight: bolder;
        font-size: 2rem;
        display: flex;
        justify-content: center;
    }
</style>