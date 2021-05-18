<script>
    import { onMount } from "svelte";

    import KanaSelectionTable from "../components/KanaSelectionTable.svelte";
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

<div class="wrapper">
    {#if isLoading}
        <LoadingSpinner />
    {:else}
        <TabNav bind:selectedTab />
        {#if selectedTab === "Hiragana"}
            <KanaSelectionTable kana={hiragana} />
        {:else}
            <KanaSelectionTable kana={katakana} />
        {/if}
    {/if}
</div>
