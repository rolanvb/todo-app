<script>
	let { children } = $props();
</script>


<header>
    <h1 class="pageTitle">
        Todo bien App
    </h1>
</header>

{@render children()}

<style>
    header {
        background-color: var(--primary-color);
        color: var(--secondary-color);
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