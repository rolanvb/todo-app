<script>
    import { onMount } from 'svelte';

    let tasks = [];

    // Retrieve tasks from session storage on component mount
    onMount(() => {
        const storedTasks = sessionStorage.getItem('tasks');
        if (storedTasks) {
            tasks = JSON.parse(storedTasks);
        }
    });

    // Function to handle form submission
    function addTask(event) {
        event.preventDefault();
        const taskName = event.target.taskName.value;
        if (taskName) {
            tasks = [...tasks, taskName];
            sessionStorage.setItem('tasks', JSON.stringify(tasks));
            event.target.reset();
        }
    }
</script>

<section>
    <h2>Add Task</h2>
    <form on:submit={addTask}>
        <label for="taskName">Task Name</label>
        <input type="text" id="taskName" name="taskName" required>
        <button type="submit">Add Task</button>
    </form>
</section>

<section>
    <h2>Tasks</h2>
    <ul>
        {#each tasks as task}
            <li>{task}</li>
        {/each}
    </ul>
</section>