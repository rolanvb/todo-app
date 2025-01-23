<script>
    import { onMount } from 'svelte';

    let tasks = [];

    // Retrieve tasks from local storage on component mount
    onMount(() => {
        const storedTasks = localStorage.getItem('tasks');
        if (storedTasks) {
            tasks = JSON.parse(storedTasks);
        }
    });

    // Function to handle task addition
    function addTask(event) {
        event.preventDefault();
        const taskName = event.target.taskName.value;
        if (taskName) {
            tasks = [...tasks, { name: taskName, done: false }];
            localStorage.setItem('tasks', JSON.stringify(tasks));
            event.target.reset();
        }
    }

    // Function to toggle task completion
    function toggleTask(index) {
        tasks = tasks.map((task, i) => i === index ? { ...task, done: !task.done } : task);
        localStorage.setItem('tasks', JSON.stringify(tasks));
    }
</script>

<main>
    <section>
        <h2 class="sectionTitle">Add Task</h2>
        <form on:submit={addTask}>
            <input type="text" id="taskName" name="taskName" required>
            <button class="taskButton" type="submit">Add Task</button>
        </form>
    </section>
    
    <section class="taskList">
        <h2 class="sectionTitle">Tasks</h2>
        <ul>
            {#each tasks as task, index}
                <li><button on:click={() => toggleTask(index)} class:done={task.done} class=task>{task.name}</button></li>
            {/each}
        </ul>
    </section>
</main>


<style>
main {
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 2rem 1rem;
        max-width: 600px;
        margin: 0 auto;
        background: #fff;
        border-radius: 10px;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    }

    h2 {
        font-size: 1.5rem;
        color: #2a31fb;
        margin-bottom: 1rem;
    }

    form {
        width: 100%;
        display: flex;
        flex-direction: column;
        gap: 1rem;
        margin-bottom: 2rem;
    }

    input#taskName {
        border: 1px solid #ddd;
        border-radius: 5px;
        padding: 10px;
        font-size: 1rem;
        width: 100%;
    }

    .taskButton {
        background-color: #3135b3;
        color: #fff;
        font-weight: bold;
        padding: 10px;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        font-size: 1rem;
        transition: background-color 0.3s ease;
    }

    .taskButton:hover {
        background-color: rgb(21, 23, 134);
    }

    .taskList {
        margin-top: 10px;
        width: 100%;
    }

    ul {
        list-style: none;
        padding: 0;
    }

    li {
        display: flex;
        align-items: center;
        justify-content: space-between;
        background: whitesmoke;
        border-radius: 5px;
        margin-bottom: 0.5rem;
        padding: 10px;
        transition: background-color 0.2s ease;
    }

    li:hover {
        background-color: #e7e7e7;
    }

    button.task {
        background: none;
        border: none;
        color: #333;
        font-size: 1rem;
        text-align: left;
        cursor: pointer;
        width: 100%;
    }

    button.task:hover {
        text-decoration: underline;
    }

    button.task.done {
        text-decoration: line-through;
        color: #888;
    }

    @media (max-width: 768px) {
        main {
            padding: 1rem;
        }

        h2 {
            font-size: 1.25rem;
        }

        .taskButton, input#taskName {
            font-size: 0.9rem;
        }
    }
</style>
