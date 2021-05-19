<script>
    import Footer from "../components/Footer.svelte";
</script>

<style>
    :global(.wrapper) {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: calc(100% - (75px + 48px));
        padding: 0 2rem;
    }

    .sub-heading {
        text-align: center;
    }

    .description {
        text-align: center;
        margin-bottom: 2rem;
    }
</style>

<div class="wrapper">
    <h1 class="main-heading">Kana sensei</h1>
    <h2 class="sub-heading">Lerne jetzt Hiragana und Katakana</h2>
    <p class="description">Einfach, kostenlos und ohne Anmeldung</p>
</div>
