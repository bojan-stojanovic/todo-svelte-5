<script lang="ts">
    import TodoCard from "./TodoCard.svelte";

    type Props = {
        filteredTodos: { id: string, message: string; completed: boolean }[];
        onTodoUpdate: (id: string) => void;
        onRemoveTodo: (id: string) => void;
    };

    let { filteredTodos, onTodoUpdate, onRemoveTodo }: Props = $props();
</script>

<div class="todo-list">
    {#each filteredTodos as todo (todo.id)}
        <TodoCard
            message={todo.message}
            completed={todo.completed}
            id={todo.id}
            todoStatus={onTodoUpdate}
            removeTodo={onRemoveTodo}
        />
    {/each}
</div>

<style>
    .todo-list {
        display: grid;
        gap: 1rem;
    }
</style>
