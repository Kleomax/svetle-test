<script>
        import Icon from './components/Icon.svelte';
        let newItem = "";
        let todoList = [];
        function add() {
            if (newItem !== "") {
                todoList = [
                    ...todoList,
                    {
                        task: newItem,
                        completed: false
                    },
                ];
                newItem = ""
            }
        }
        function remove(index) {
            todoList.splice(index, 1);
            todoList = todoList;
        }
        
        function complete(index) {
            todoList[index].completed = !todoList[index].completed;
        }
        </script>
        <h1>My to-do list</h1>
<main>
    <form on:submit|preventDefault={add}>
    <input bind:value={newItem} placeholder="Enter to-do">
    <button class="add-todo" on:click={add}><span class="">+</span></button>
    </form>
    <div class="todos">
        {#each todoList as item, index }
        <div class="todo" class:completed ={item.completed}>
            <span class="todo-text">{item.task}</span>
            <div class="todo-buttons">
                <button class="complete" on:click={() => complete(index)}>
                    Готово
                </button>
                <button class="delete" on:click={() => remove(index)}>
                удалить
                </button>
        </div>
    </div>
    {/each}
</div>
</main>
<style>
    main {
        display: flex;
        flex-direction: column;
        align-items: center;
        min-height: 100%;
        padding: 5vmin;
        box-sizing: border-box;
        background: antiquewhite;
    }
    form {
        width: 100%;
        max-width: 500px;
        display: flex;
        align-items: center;
        margin-bottom: 1rem;
    }
    input {
        flex-grow: 1;
        width: 0;
        border: none;
        border-bottom: 1px solid black;
        background: transparent;
        box-shadow: none;
        font-size: 1.2rem;
        margin: 0;
        outline: none;
    }
    .add-todo {
        border: 1px solid black;
        border-radius: 50%;
        cursor: pointer;
        padding: 8px 13px 8px 13px;
        margin-left: 5%;
    }
    .todo {
        display: flex;
        padding: 20px;
        border-radius: 20px;
        box-shadow: 00 15px rgb(0 0 0 / 20%);
        background-color: hsla(0, 0%, 100%, 0.2);
        margin-top: 1rem;
        font-size: 1.2rem;
        gap: 65%;
        align-items: center;
    }
    .todo-buttons {
        display: flex;
        align-items: center;
    }
    .todo button {
        width: 32px;
        height: 32px;
        padding: 4px;
        margin: 0;
        flex-shrink: 0;
    }
    h1 {
        text-align: center;
        font-size: 1.5rem;
        margin: 2em 0;
    }
    button {
        background-color: transparent;
        border: none;
        cursor: pointer;
        font-size: 15px;
    }
    button.delete,
    button.delete:hover {
        color: brown;
        transition: color 100ms ease-out;
        margin-left: 25px;
    }
    button.complete,
    button.complete:hover {
        color: cadetblue;
        transition: color 100ms ease-out;
    }
    .todo.completed {
        color: slategray;
    }
    .todo.completed .todo-text {
        text-decoration: line-through;
    }
    .todo.completed button {
        color: silver;
    }
    .todos {
        width: 100%;
        max-width: 500px;
    }
</style>