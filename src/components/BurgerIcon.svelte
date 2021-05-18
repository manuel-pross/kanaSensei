<script>
    export let open = false;
</script>

<style>
    .burger-wrapper {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        right: 15px;
        width: 35px;
        height: 30px;
    }

    .nav-burger {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        width: 35px;
        height: 5px;
        background-color: var(--gray-1);
        border-radius: 2px;
        transition: all 0.25s ease;
    }

    .nav-burger::before {
        content: "";
        position: absolute;
        top: 12px;
        width: 35px;
        height: 5px;
        background-color: var(--gray-1);
        border-radius: 2px;
        transition: all 0.25s ease;
        opacity: 1;
    }

    .nav-burger::after {
        content: "";
        position: absolute;
        bottom: 12px;
        width: 35px;
        height: 5px;
        background-color: rgba(157, 157, 156, 1);
        border-radius: 2px;
        transition: all 0.25s ease;
        opacity: 1;
    }

    .open .nav-burger {
        background-color: rgba(157, 157, 156, 0);
    }

    .open .nav-burger:before {
        background-color: var(--red-1);
        transform: translateY(-12px) rotate(-45deg);
    }

    .open .nav-burger:after {
        background-color: var(--red-1);
        transform: translateY(12px) rotate(45deg);
    }

    @media only screen and (min-width: 768px) {
        :global(.burger-wrapper) {
            display: none;
        }
    }
</style>

<!-- class: ist immer für toggeling / wenn die Variable ein boolean ist kann man es so weit verkürzen 
in diesem Fall wird open einfach bei jedem Click umgekehrt
-->
<div class="burger-wrapper" class:open on:click={() => (open = !open)}>
    <div class="nav-burger" />
</div>
