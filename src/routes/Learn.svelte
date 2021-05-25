<script>
    import { onMount } from "svelte";

    import { kanas } from "./../kana-stores";

    import KanaList from "../components/KanaList.svelte";
    import LoadingSpinner from "../components/LoadingSpinner.svelte";
    import TabNav from "../components/TabNav.svelte";
    import Button from "../components/Button.svelte";

    let selectedTab = "Hiragana";
    let hiragana = [];
    let katakana = [];

    let selectedHiragana = [];
    let selectedKatakana = [];

    let isLoading = true;
    let hiraganaLoaded = false;
    let katakanaLoaded = false;

    let mode = "selecting";

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
                hiragana = data;

                for (let i = 0; i < data.length; i++) {
                    for (let j = 0; j < data[i].length; j++) {
                        if (data[i][j].code !== "none") {
                            delete data[i][j].isLastInRow;
                            selectedHiragana.push(data[i][j]);
                        }
                    }
                }
                selectedHiragana = selectedHiragana.map((obj) => ({
                    ...obj,
                    solved: false,
                }));

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
                katakana = data;

                for (let i = 0; i < data.length; i++) {
                    for (let j = 0; j < data[i].length; j++) {
                        if (data[i][j].code !== "none") {
                            delete data[i][j].isLastInRow;
                            selectedKatakana.push(data[i][j]);
                        }
                    }
                }
                selectedKatakana = selectedKatakana.map((obj) => ({
                    ...obj,
                    solved: false,
                }));
                katakanaLoaded = true;
            })
            .catch((err) => {
                console.log(err);
            });
    });

    function handleClick() {
        mode = "learning";
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
    {:else}
        {#if mode === "selecting"}
            <div class="selection">
                <TabNav bind:selectedTab />
                {#if selectedTab === "Hiragana"}
                    <KanaList kana={hiragana} mode="select" />
                {:else}
                    <KanaList kana={katakana} mode="select" />
                {/if}
            </div>
        {:else if mode === "learning"}
            <p>hello</p>
        {/if}
        <Button text={"Start"} on:btnClicked={handleClick}/>
    {/if}
</div>
