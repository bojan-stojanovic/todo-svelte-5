<script lang="ts">
    type Props = {
        todoNumber: number;
        activeFilter: string;
        updateActiveFilter: (filter: string) => void;
    };
    let { updateActiveFilter, todoNumber, activeFilter }: Props = $props();
</script>

<div class="filter-wrapper">
    <span>Number of todos: {todoNumber}</span>
    <div class="filters">
        <button
            class={activeFilter === "all" ? "active" : ""}
            onclick={() => updateActiveFilter("all")}>All</button
        >
        <button
            class={activeFilter === "done" ? "active" : ""}
            onclick={() => updateActiveFilter("done")}>Done</button
        >
        <button
            class={activeFilter === "open" ? "active" : ""}
            onclick={() => updateActiveFilter("open")}>Open</button
        >
        <span>Active filter {activeFilter}</span>
    </div>
</div>

<style>
    .filter-wrapper {
        display: flex;
        justify-content: space-between;
    }

    .filters {
        display: flex;
        gap: 1rem;
        flex-wrap: wrap;
        justify-content: flex-end;

        button {
            transition: all 0.3s;

            &:hover {
                background-color: #537eff;
                color: #fff;
            }

            &.active {
                background-color: #0040ff;
                color: #fff;
            }
        }

        span {
            flex: 1 0 100%;
            text-align: right;
        }
    }
</style>
