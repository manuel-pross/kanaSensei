<script>
    import { kanas } from "./../kana-stores";

    export let id;
    export let syll;
    export let code;

    // $kanas = [
    //     {
    //         id: id,
    //         syll: syll,
    //         code: code,
    //         completed: false,
    //     },
    //     ...$kanas,
    // ];

    let checked = true;
</script>

<style>
    div {
        position: relative;
        width: fit-content;
        height: fit-content;
    }

    input[type="checkbox"] {
        appearance: none;
        width: 40px;
        height: 40px;
        border: 1px solid var(--gray-1);
        border-radius: 3px;
        background-color: var(--gray-1);
        margin-bottom: 0;
        padding: 0;
        transition: 0.15s ease-in-out;
    }

    input[type="checkbox"]:checked {
        background-color: var(--red-2);
        border: 1px solid var(--red-2);
    }

    label {
        display: block;
        position: absolute;
        top: 4px;
        right: 50%;
        font-size: 1.25rem;
        transform: translateX(50%);
        color: var(--white);
        margin-bottom: 0;
    }

    @media only screen and (min-width: 768px) {
        input[type="checkbox"] {
            width: 45px;
            height: 45px;
        }

        label {
            top: 7px;
            cursor: pointer;
        }
    }
</style>

<div>
    <input type="checkbox" {id} bind:checked />
    <label for={id}>{@html code}</label>
</div>
