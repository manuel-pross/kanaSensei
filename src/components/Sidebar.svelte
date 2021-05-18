<script>
    import { link } from "svelte-routing";

    export let open = false;
    export let current;

    function handleClick(currentLink) {
        current = currentLink;
        open = !open;
    }
</script>

<style>
    aside {
        position: absolute;
        left: -100%;
        transition: left 0.4s ease-in-out;
        background-color: rgba(166, 45, 45, 0.85);
        width: 100%;
        height: calc(100vh - 75px);
        z-index: 1;
    }

    .open {
        left: 0;
    }

    :global(.sidebar-item, .sidebar-item:link, .sidebar-item:visited) {
        display: block;
        align-items: center;
        color: var(--white);
        text-decoration: none;
    }

    :global(.sidebar-item) {
        padding: 0.5rem 0;
        text-align: center;
        transition: 0.25s ease-in-out;
    }

    .active {
        background-color: rgba(166, 45, 45, 0.85);
    }

    @media only screen and (min-width: 768px) {
        aside {
            display: none;
        }
    }
</style>

<aside class:open>
    <nav class="sidebar">
        <a
            class={current === "/" ? "sidebar-item active" : "sidebar-item"}
            href="/"
            on:click={() => handleClick("/")}
            use:link
            replace>Home</a
        >
        <a
            class={current === "/Hiragana"
                ? "sidebar-item active"
                : "sidebar-item"}
            href="/Hiragana"
            on:click={() => handleClick("/Hiragana")}
            use:link
            replace>Hiragana</a
        >
        <a
            class={current === "/Katakana"
                ? "sidebar-item active"
                : "sidebar-item"}
            href="/Katakana"
            on:click={() => handleClick("/Katakana")}
            use:link
            replace>Katakana</a
        >
        <a
            class={current === "/Lernen"
                ? "sidebar-item active"
                : "sidebar-item"}
            href="/Lernen"
            on:click={() => handleClick("/Lernen")}
            use:link
            replace>Lernen</a
        >
    </nav>
</aside>
