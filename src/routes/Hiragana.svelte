<script>
    import { onMount } from "svelte";

    import KanaList from "../components/KanaList.svelte";
    import LoadingSpinner from "../components/LoadingSpinner.svelte";

    let hiragana = [];
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
    });
</script>

<div class="wrapper">
    {#if isLoading}
        <LoadingSpinner />
    {:else}
        <KanaList kana={hiragana} />
    {/if}
</div>
