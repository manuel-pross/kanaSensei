<script>
    import { onMount } from "svelte";

    export let learningKanas = [];

    let currentKana = {};
    let answer = "";

    $: console.log(learningKanas);

    onMount(() => {
        currentKana = learningKanas[0];
    });

    function handleKeyUp({ key }) {
        if (key !== "Enter" || answer.length === 0) return;
        checkAnswer();
    }

    function checkAnswer() {
        if (answer.toLowerCase() === currentKana.syll) {
            console.log("correct");
            learningKanas = learningKanas.filter(
                (el) => el.id != currentKana.id
            );
            currentKana = learningKanas[0];
        }
    }
</script>

{#if learningKanas.length > 0}
    <p>{@html currentKana.code}</p>
    <input type="text" bind:value={answer} on:keyup={handleKeyUp} />
    <button on:click={checkAnswer}>Bestätigen</button>
{/if}
