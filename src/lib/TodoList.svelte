<script lang="ts">
    import TodoCard from "./TodoCard.svelte";

    type Props = {
        filteredTodos: { message: string; completed: boolean }[];
        onTodoUpdate: (index: number) => void;
        onRemoveTodo: (index: number) => void;
    };

    let { filteredTodos, onTodoUpdate, onRemoveTodo }: Props = $props();
</script>

<div class="todo-list">
    {#each filteredTodos as todo, index (index)}
        <TodoCard
            message={todo.message}
            completed={todo.completed}
            {index}
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
