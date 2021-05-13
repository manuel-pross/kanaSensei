<script>
  export let kana = "";
  export let syll = "";
  export let shown = false;

  export function show() {
    shown = true;
  }

  export function hide() {
    shown = false;
  }

  function handleEscape(event) {
    if (event.key === "Escape") shown = false;
  }
</script>

<style>
  .modal-wrapper {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background-color: rgba(0, 0, 0, 0.8);
  }

  .modal-btn-exit {
    position: absolute;
    top: 1.3rem;
    right: 1rem;
    text-align: center;
    vertical-align: middle;
    border: 2px solid var(--gray-1);
    margin: 0;
    padding: 0;
    width: 34px;
    height: 34px;
    border-radius: 17px;
    transition: all 0.25s ease;
  }

  .modal-btn-exit::before {
    content: "";
    position: absolute;
    top: 50%;
    right: 50%;
    display: block;
    width: 15px;
    height: 3px;
    transform: translate(50%, -50%) rotate(-45deg);
    background-color: var(--gray-1);
    transition: all 0.25s ease;
  }

  .modal-btn-exit::after {
    content: "";
    position: absolute;
    top: 50%;
    right: 50%;
    display: block;
    width: 15px;
    height: 3px;
    transform: translate(50%, -50%) rotate(45deg);
    background-color: var(--gray-1);
    transition: all 0.25s ease;
  }

  .modal-inner-wrapper {
    position: absolute;
    top: 50%;
    right: 50%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    transform: translate(50%, -50%);
    width: 80%;
    height: 50%;
    background-color: var(--white);
  }

  .modal-kana {
    display: block;
    z-index: 1;
    font-size: 10rem;
  }

  .modal-syll {
    font-family: "Noto Sans Bold";
    display: block;
    z-index: 1;
    font-size: 1.5rem;
    margin-bottom: 2rem;
  }

  @media only screen and (min-width: 768px) {
    .modal-btn-exit {
      cursor: pointer;
      width: 64px;
      height: 64px;
      border-radius: 32px;
    }

    .modal-btn-exit::before {
      width: 28px;
      height: 4px;
    }

    .modal-btn-exit::after {
      width: 28px;
      height: 4px;
    }

    .modal-btn-exit:hover {
      border-color: var(--red-1);
    }

    .modal-btn-exit:hover:before {
      background-color: var(--red-1);
    }

    .modal-btn-exit:hover:after {
      background-color: var(--red-1);
    }

    .modal-inner-wrapper {
      max-width: 800px;
      height: 60%;
      max-height: 800px;
    }
  }
</style>

<svelte:window on:keydown={handleEscape} />

{#if shown}
  <div class="modal-wrapper">
    <button class="modal-btn-exit" on:click={() => hide()} />
    <div class="modal-inner-wrapper">
      <span class="modal-kana">{@html kana}</span>
      <span class="modal-syll">{syll}</span>
    </div>
  </div>
{/if}
