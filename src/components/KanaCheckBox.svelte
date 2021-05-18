<script>
    export let id;
    export let code;

    let checked = true;
</script>

<style>
    div {
        position: relative;
    }

    input[type="checkbox"] {
        appearance: none;
        width: 40px;
        height: 40px;
        border: 1px solid var(--gray-1);
        border-radius: 3px;
        background-color: var(--gray-1);
        margin-bottom: 0;
        transition: 0.15s ease-in-out;
    }

    input[type="checkbox"]:checked {
        background-color: var(--red-2);
        border: 1px solid var(--red-2);
    }

    label {
        position: absolute;
        top: 4px;
        right: 50%;
        font-size: 1.25rem;
        transform: translateX(50%);
        color: var(--white);
        margin-bottom: 0;
    }
</style>

<div>
    <input type="checkbox" {id} bind:checked />
    <label for={id}>{@html code}</label>
</div>
