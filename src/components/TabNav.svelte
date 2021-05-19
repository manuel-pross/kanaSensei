<script>
    import Tab from "./Tab.svelte";

    export let selectedTab = "Hiragana";

    function handleClick(e) {
        selectedTab = e.detail;
    }
</script>

<style>
    div {
        width: 100%;
        border-bottom: 1px solid var(--red-2);
    }

    @media only screen and (min-width: 768px) {
        div {
            max-width: 900px;
        }
    }
</style>

<div>
    <Tab
        tabHeading={"Hiragana"}
        on:selectedTab={handleClick}
        selected={selectedTab === "Hiragana" ? true : false}
    />
    <Tab
        tabHeading={"Katakana"}
        on:selectedTab={handleClick}
        selected={selectedTab === "Katakana" ? true : false}
    />
</div>
