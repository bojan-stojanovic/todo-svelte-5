<script lang="ts">
    type Props = {
        message: string;
        completed: boolean;
        id: string;
        removeTodo: (id: string) => void;
        todoStatus: (id: string) => void;
    };

    let { message, completed, id, removeTodo, todoStatus }: Props = $props();
</script>

<div class="todo-card {completed ? 'completed' : ''}">
    <p>{message}</p>
    <div class="todo-card__controls">
        <button class="toggle" onclick={() => todoStatus(id)}
            >Mark as done</button
        >
        <button class="remove" onclick={() => removeTodo(id)}>Remove</button>
    </div>
</div>

<style>
    .todo-card {
        display: grid;
        grid-template-columns: 1fr auto;
        border: 2px solid #ccc;
        gap: 1rem;
        padding: 1rem;
        transition: all 0.3s;

        &.completed {
            border-color: #00853e;
            background-color: rgba(0, 133, 62, 0.35);
        }

        p {
            margin: 0;
        }
    }

    .todo-card__controls {
        display: grid;
        gap: 1rem;
    }

    .remove {
        background-color: #c12727;
        color: #fff;
    }

    .toggle {
        background-color: #00853e;
        color: #fff;
    }
</style>
