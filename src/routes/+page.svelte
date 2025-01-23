<script>
    import { onMount } from 'svelte';

    let tasks = [];

    // Retrieve tasks from session storage on component mount
    onMount(() => {
        const storedTasks = localStorage.getItem('tasks');
        if (storedTasks) {
            tasks = JSON.parse(storedTasks);
        }
    });

    // Function to handle form submission
    function addTask(event) {
        event.preventDefault();
        const taskName = event.target.taskName.value;
        if (taskName) {
            tasks = [...tasks, { name: taskName, done: false }];
            localStorage.setItem('tasks', JSON.stringify(tasks));
            event.target.reset();
        }
    }

    function toggleTask(index) {
        tasks = tasks.map((task, i) => i === index ? { ...task, done: !task.done } : task);
        localStorage.setItem('tasks', JSON.stringify(tasks));
    }
</script>

<section>
    <h2 class="sectionTitle">Add Task</h2>
    <form on:submit={addTask}>
        <label for="taskName">Task Name</label>
        <input type="text" id="taskName" name="taskName" required>
        <button type="submit">Add Task</button>
    </form>
</section>

<section>
    <h2 class="sectionTitle">Tasks</h2>
    <ul>
        {#each tasks as task, index}
            <li><button on:click={() => toggleTask(index)} class:done={task.done} class=task>{task.name}</button></li>
        {/each}
    </ul>
</section>

<style>
    * {
        margin: 4px;
    }

    button{
        background: none;
        color: inherit;
        border: none;
        padding: 0;
        font: inherit;
        cursor: pointer;
        outline: inherit;
    }
    li {
        list-style-type: none;
    }
    .sectionTitle {
        /* font-size: 1.5rem; */
        font-weight: bold;
    }
    .task {
        margin: 0.5rem;
        border-radius: 5px;
        list-style-type: none;
        
    }
    .task:hover {
        text-decoration: underline;
    }
    /* .task:active {
        background-color: #d4d4d4;
    } */
    .task.done {
        text-decoration: line-through;
    }
</style>