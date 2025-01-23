<script>
	let { children } = $props();
</script>


<header>
    <h1>
        To Do App
    </h1>
</header>

{@render children()}

<style>
    header {
        flex: auto;
        justify-content: center;
        background-color: #333;
        color: white;
        padding: 1rem;
        

    }
</style>