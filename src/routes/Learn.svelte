<script>
    import { onMount } from "svelte";

    import { kanas } from "./../kana-stores";

    import KanaList from "../components/KanaList.svelte";
    import LoadingSpinner from "../components/LoadingSpinner.svelte";
    import TabNav from "../components/TabNav.svelte";
    import Button from "../components/Button.svelte";
    import LearningProcess from "../components/LearningProcess.svelte";

    let selectedTab = "Hiragana";
    let hiragana = [];
    let katakana = [];

    let selectedHiragana = [];
    let selectedKatakana = [];

    let isLoading = true;
    let hiraganaLoaded = false;
    let katakanaLoaded = false;

    let mode = "selecting";

    let learningKanas = [];

    $: if (hiraganaLoaded && katakanaLoaded) {
        $kanas = selectedHiragana.concat(selectedKatakana);
    }

    onMount(() => {
        fetch("./hiragana.json")
            .then((res) => {
                if (!res.ok) {
                    throw new Error(
                        "Fetching hiragana.json failed, please try again."
                    );
                }
                return res.json();
            })
            .then((data) => {
                hiragana = [...data];

                for (let i = 0; i < data.length; i++) {
                    for (let j = 0; j < data[i].length; j++) {
                        if (data[i][j].code !== "none") {
                            selectedHiragana.push(data[i][j]);
                        }
                    }
                }

                isLoading = false;
                hiraganaLoaded = true;
            })
            .catch((err) => {
                isLoading = false;
                console.log(err);
            });
        fetch("./katakana.json")
            .then((res) => {
                if (!res.ok) {
                    throw new Error(
                        "Fetching katakana.json failed, please try again."
                    );
                }
                return res.json();
            })
            .then((data) => {
                katakana = [...data];

                for (let i = 0; i < data.length; i++) {
                    for (let j = 0; j < data[i].length; j++) {
                        if (data[i][j].code !== "none") {
                            selectedKatakana.push(data[i][j]);
                        }
                    }
                }
                katakanaLoaded = true;
            })
            .catch((err) => {
                console.log(err);
            });
    });

    function handleClick() {
        mode = "learning";
        learningKanas = shuffle($kanas);
    }

    function shuffle(a) {
        for (let i = a.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [a[i], a[j]] = [a[j], a[i]];
        }
        return a;
    }
</script>

<style>
    .selection {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        width: 100%;
    }
</style>

<div class="wrapper">
    {#if isLoading}
        <LoadingSpinner />
    {:else if mode === "selecting"}
        <div class="selection">
            <TabNav bind:selectedTab />
            {#if selectedTab === "Hiragana"}
                <KanaList kana={hiragana} mode="select" />
            {:else}
                <KanaList kana={katakana} mode="select" />
            {/if}
        </div>
        <Button text={"Start"} on:btnClicked={handleClick} />
    {:else}
        <LearningProcess {learningKanas} />
    {/if}
</div>
