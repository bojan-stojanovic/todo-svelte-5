<script lang="ts">
    type AddTodo = {
        addTodo: (todo: string) => void;
    };
    let { addTodo }: AddTodo = $props();

    let inputValue = $state("");
    let isEmpty = $state(false);

    function submitTodoHandler(e: SubmitEvent) {
        e.preventDefault();

        if (inputValue.trim() === "") {
            isEmpty = true;

            const timeOut = setTimeout(() => {
                isEmpty = false;

                clearTimeout(timeOut);
            }, 2000);

            return;
        }

        addTodo(inputValue);

        inputValue = "";
    }
</script>

<form class="form" onsubmit={submitTodoHandler}>
    <div>
        <label for="todoInput">Add your todo</label>
        <input
            type="text"
            id="todoInput"
            name="todoInput"
            placeholder="Add your todo"
            class="input"
            bind:value={inputValue}
        />
    </div>
    {#if isEmpty}
        <p class="error">Please add todo</p>
    {/if}

    <button class="button">Add</button>
</form>

<style>
    .form {
        display: grid;
        gap: 1rem;

        > div {
            display: grid;
            gap: 0.5rem;
        }
    }

    .input {
        width: 100%;
        padding: var(--element-padding);
    }

    .button {
        justify-self: end;
        background-color: #0040ff;
        color: #fff;
    }

    .error {
        color: red;
        font-size: 0.85rem;
    }
</style>
