<script lang="ts">
    import { onMount } from "svelte";
    import TodoInput from "./lib/TodoInput.svelte";
    import TodoFilter from "./lib/TodoFilter.svelte";
    import TodoList from "./lib/TodoList.svelte";

    type Todo = {
        id: string;
        message: string;
        completed: boolean;
    };

    let todos = $state<Todo[]>([]);
    let activeFilter = $state("all");
    let filteredTodos = $derived.by(() => {
        if (activeFilter === "done")
            return todos.filter((todo) => todo.completed === true);
        if (activeFilter === "open")
            return todos.filter((todo) => todo.completed === false);
        return todos;
    });

    async function fetchTodos() {
        try {
            const response = await fetch("/json-todos.json");
            const data = await response.json();

            todos = [...data];
        } catch (e) {
            console.error(e);
        }
    }

    function onAddTodo(message: string) {
        const todo = {
            id: crypto.randomUUID(),
            message,
            completed: false,
        };

        todos = [todo, ...todos];
    }

    function onFilterTodos(filter: string) {
        if (filter === activeFilter) return;

        activeFilter = filter;
    }

    function onRemoveTodo(id: string) {
        todos = todos.filter(todo => todo.id !== id);
    }

    function onTodoUpdate(id: string) {
        todos = todos.map(todo => {
            if (todo.id === id) {
                return { ...todo, completed: !todo.completed };
            }
            return todo;
        });
    }

    onMount(fetchTodos);
</script>

<div class="container">
    <h1>Todo app</h1>
    <TodoInput addTodo={onAddTodo} />

    {#if todos.length > 0}
        <TodoFilter
            updateActiveFilter={onFilterTodos}
            todoNumber={filteredTodos.length}
            {activeFilter}
        />
        <TodoList {filteredTodos} {onRemoveTodo} {onTodoUpdate} />
    {:else}
        <p>You don't have any todos yet....</p>
    {/if}
</div>

<style>
    .container {
        max-width: 70rem;
        margin: 0 auto;
        padding: 0 1rem;
        display: grid;
        gap: 2rem;

        h1 {
            margin: 0;
            text-align: center;
        }
    }
</style>
