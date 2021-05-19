<script>
    import { onMount } from "svelte";

    import KanaList from "../components/KanaList.svelte";
    import LoadingSpinner from "../components/LoadingSpinner.svelte";
    import TabNav from "../components/TabNav.svelte";

    let selectedTab = "Hiragana";
    let hiragana = [];
    let katakana = [];
    let isLoading = true;

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
                isLoading = false;
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
                isLoading = false;
            })
            .catch((err) => {
                isLoading = false;
                console.log(err);
            });
    });
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
        <div class="selection">
            <TabNav bind:selectedTab />
            {#if selectedTab === "Hiragana"}
                <!-- <KanaSelectionTable kana={hiragana} /> -->
                <KanaList kana={hiragana} mode="select" />
            {:else}
                <!-- <KanaSelectionTable kana={katakana} /> -->
                <KanaList kana={katakana} mode="select" />
            {/if}
        </div>
    {/if}
</div>
