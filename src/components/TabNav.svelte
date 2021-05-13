<script>
    import Tab from "./Tab.svelte";

    let selectedTab = "Hiragana";

    function handleClick(e) {
        selectedTab = e.detail;
    }
</script>

<style>
    .tab-list {
        width: 100%;
        border-bottom: 1px solid var(--red-2);
    }
</style>

<div class="tab-list">
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
