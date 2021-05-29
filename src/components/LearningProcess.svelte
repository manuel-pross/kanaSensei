<script>
    import { onMount } from "svelte";

    export let learningKanas = [];

    let currentKana = {};
    let answer = "";
    let isAnswerCorrect = true;

    onMount(() => {
        currentKana = learningKanas[0];
    });

    function handleKeyUp({ key }) {
        if (key !== "Enter" || answer.length === 0) return;
        checkAnswer();
    }

    function checkAnswer() {
        if (answer.toLowerCase() === currentKana.syll) {
            isAnswerCorrect = true;
            learningKanas = learningKanas.filter(
                (el) => el.id != currentKana.id
            );
            currentKana = learningKanas[0];
        } else {
            isAnswerCorrect = false;
        }
        answer = "";
    }

    function setFocus(el) {
        el.focus();
    }
</script>

<style>
    .kana {
        font-size: 1.75rem;
    }
</style>

{#if learningKanas.length > 0}
    {#if !isAnswerCorrect}
        <p>FALSCH!</p>
    {/if}
    <p class="kana">{@html currentKana.code}</p>
    <input
        type="text"
        bind:value={answer}
        on:keyup={handleKeyUp}
        use:setFocus
    />
    <button on:click={checkAnswer}>Bestätigen</button>
{:else}
    <p>FERTIG!</p>
{/if}
