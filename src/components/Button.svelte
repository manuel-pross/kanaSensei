<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();

    export let text;

    function handleClick() {
        dispatch("btnClicked");
    }
</script>

<style>
    button {
        padding: 0.5rem 0.75rem;
        border: none;
        border-radius: 10px;
        background-color: var(--red-2);
        color: var(--white);
        transition: 0.25s ease-in-out;
    }

    @media only screen and (min-width: 768px) {
        button {
            cursor: pointer;
        }

        button:hover {
            background-color: var(--red-1);
        }
    }
</style>

<button on:click={handleClick}>{text}</button>
