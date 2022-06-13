<script>
    let todos = [...Array(10000)].map((_, index) => {
            return {
                task: `Task ${index} です`,
                isCompleted: false,
            }
        });

    const handleAddTask = () => {
        if (!newTaskInput.value) return;

        const newTask = {
            task: newTaskInput.value,
            isCompleted: false,
        }
        todos = [...todos, newTask];
        newTaskInput.value = '';
    }

    const handleRemoveTask = (index) => {
        todos.splice(index, 1);
        todos = todos;
    }

    let newTaskInput = null;
</script>

<h1>ToDo List</h1>
Add Task : <input placeholder="Add New Task" bind:this={newTaskInput}/>
<button on:click={handleAddTask}>Add</button>
<ul>
    {#each todos as todo, index}
        <li key={index}
            style="text-decoration-line: {todo.isCompleted ? 'line-through' : 'none'}">
            <input type="checkbox" bind:value={todo.isCompleted}/>
            {todo.task}&nbsp;
            <span 
                on:click={() => handleRemoveTask(index)}
                style="cursor: pointer">
                X
            </span>
        </li>
    {/each}
</ul>