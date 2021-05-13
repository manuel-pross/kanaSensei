<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();

    export let tabHeading;
    export let selected;

    function handleClick(tabHeading) {
        dispatch("selectedTab", tabHeading);
    }
</script>

<style>
    button {
        font-size: 1.1rem;
        background-color: unset;
        border: none;
        border-bottom: 3px solid var(--white);
        margin: 0;
        transition: 0.25s ease-in-out;
    }

    .selected {
        border-bottom: 3px solid var(--red-2);
    }
</style>

<button class:selected on:click={handleClick(tabHeading)}>{tabHeading}</button>
