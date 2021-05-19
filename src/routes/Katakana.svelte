<script>
    import { onMount } from "svelte";

    import KanaList from "../components/KanaList.svelte";
    import LoadingSpinner from "../components/LoadingSpinner.svelte";

    let katakana = [];
    let isLoading = true;

    onMount(() => {
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
        <KanaList kana={katakana} />
    {/if}
</div>
