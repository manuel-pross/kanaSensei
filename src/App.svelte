<script>
    import { Router, Link, Route } from "svelte-routing";

    import Startpage from "./routes/Startpage.svelte";
    import Hiragana from "./routes/Hiragana.svelte";
    import Katakana from "./routes/Katakana.svelte";
    import Learn from "./routes/Learn.svelte";

    import BurgerIcon from "./components/BurgerIcon.svelte";
    import Sidebar from "./components/Sidebar.svelte";
    import Footer from "./components/Footer.svelte";

    export let url = "";

    let open = false;
    let current = window.location.pathname;
</script>

<style>
    /* noto-sans-jp-100 - latin */
    @font-face {
        font-family: "Noto Sans Small";
        font-style: normal;
        font-weight: 100;
        src: url("../fonts/noto-sans-jp-v28-latin-100.eot"); /* IE9 Compat Modes */
        src: local(""),
            url("../fonts/noto-sans-jp-v28-latin-100.eot?#iefix")
                format("embedded-opentype"),
            /* IE6-IE8 */ url("../fonts/noto-sans-jp-v28-latin-100.woff2")
                format("woff2"),
            /* Super Modern Browsers */
                url("../fonts/noto-sans-jp-v28-latin-100.woff") format("woff"),
            /* Modern Browsers */ url("../fonts/noto-sans-jp-v28-latin-100.ttf")
                format("truetype"),
            /* Safari, Android, iOS */
                url("../fonts/noto-sans-jp-v28-latin-100.svg#NotoSansJP")
                format("svg"); /* Legacy iOS */
    }
    /* noto-sans-jp-regular - latin */
    @font-face {
        font-family: "Noto Sans Normal";
        font-style: normal;
        font-weight: 400;
        src: url("../fonts/noto-sans-jp-v28-latin-regular.eot"); /* IE9 Compat Modes */
        src: local(""),
            url("../fonts/noto-sans-jp-v28-latin-regular.eot?#iefix")
                format("embedded-opentype"),
            /* IE6-IE8 */ url("../fonts/noto-sans-jp-v28-latin-regular.woff2")
                format("woff2"),
            /* Super Modern Browsers */
                url("../fonts/noto-sans-jp-v28-latin-regular.woff")
                format("woff"),
            /* Modern Browsers */
                url("../fonts/noto-sans-jp-v28-latin-regular.ttf")
                format("truetype"),
            /* Safari, Android, iOS */
                url("../fonts/noto-sans-jp-v28-latin-regular.svg#NotoSansJP")
                format("svg"); /* Legacy iOS */
    }
    /* noto-sans-jp-900 - latin */
    @font-face {
        font-family: "Noto Sans Bold";
        font-style: normal;
        font-weight: 900;
        src: url("../fonts/noto-sans-jp-v28-latin-900.eot"); /* IE9 Compat Modes */
        src: local(""),
            url("../fonts/noto-sans-jp-v28-latin-900.eot?#iefix")
                format("embedded-opentype"),
            /* IE6-IE8 */ url("../fonts/noto-sans-jp-v28-latin-900.woff2")
                format("woff2"),
            /* Super Modern Browsers */
                url("../fonts/noto-sans-jp-v28-latin-900.woff") format("woff"),
            /* Modern Browsers */ url("../fonts/noto-sans-jp-v28-latin-900.ttf")
                format("truetype"),
            /* Safari, Android, iOS */
                url("../fonts/noto-sans-jp-v28-latin-900.svg#NotoSansJP")
                format("svg"); /* Legacy iOS */
    }

    :root {
        --white: #ffffff;
        --red-1: #a62d2d;
        --red-2: #f25041;
        --gray-1: #9d9d9c;
    }

    :global(h1, h2, h3, h4, p) {
        margin-top: 0;
    }

    :global(h1, h2, h3, h4) {
        color: var(--red-1);
        font-family: "Noto Sans Bold";
    }

    :global(span) {
        font-size: 0.8rem;
    }

    :global(body) {
        padding: 0;
        font-family: "Noto Sans Normal";
        height: 100vh;
    }

    .main-nav {
        position: relative;
        display: flex;
        justify-content: flex-end;
        width: 100%;
        height: 75px;
        box-shadow: 0 4px 2px -2px var(--gray-1);
    }

    :global(.nav-link-wrapper) {
        display: none;
    }

    :global(.nav-item--logo, .nav-item--logo:link, .nav-item--logo:visited) {
        position: absolute;
        top: 0;
        left: 0;
        display: block !important;
        border-bottom: unset !important;
        color: var(--white);
    }

    :global(.nav-logo) {
        display: block;
        width: 75px;
        height: auto;
    }

    @media only screen and (min-width: 768px) {
        :global(.nav-link-wrapper) {
            display: flex;
            justify-content: space-around;
            justify-self: flex-end;
            width: calc(100% - 75px);
        }

        :global(.nav-item) {
            font-family: "Noto Sans Bold";
            display: flex !important;
            align-items: center;
            color: var(--gray-1) !important;
            border-bottom: 3px solid var(--gray-1);
            transition: all 0.25s ease;
        }

        :global(.nav-item:hover) {
            color: var(--red-1) !important;
            text-decoration: none;
            border-color: var(--red-1);
        }

        :global(.active) {
            color: var(--red-1) !important;
            border-color: var(--red-1);
        }
    }
</style>

<Router {url}>
    <nav class="main-nav">
        <Link
            class="nav-item nav-item--logo"
            on:click={() => (current = "/")}
            to="/"
        >
            <img
                class="nav-logo"
                src="../images/KanaTeacher_Logo.png"
                alt="Kana sensei logo"
            />
        </Link>
        <div class="nav-link-wrapper">
            <Link
                class={current === "/Hiragana" ? "nav-item active" : "nav-item"}
                to="/Hiragana"
                on:click={() => (current = "/Hiragana")}>Hiragana</Link
            >
            <Link
                class={current === "/Katakana" ? "nav-item active" : "nav-item"}
                to="/Katakana"
                on:click={() => (current = "/Katakana")}>Katakana</Link
            >
            <Link
                class={current === "/Lernen" ? "nav-item active" : "nav-item"}
                to="/Lernen"
                on:click={() => (current = "/Lernen")}>Lernen</Link
            >
        </div>
        <BurgerIcon bind:open />
        <!-- Die Variable open wird aus dem Component BurgerIcon heraus aktualisiert -->
    </nav>
    <Sidebar bind:current bind:open />
    <Route path="/"><Startpage /></Route>
    <Route path="/Hiragana"><Hiragana /></Route>
    <Route path="/Katakana"><Katakana /></Route>
    <Route path="/Lernen"><Learn /></Route>
    <Footer />
</Router>
