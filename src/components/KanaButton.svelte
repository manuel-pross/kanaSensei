<script>
  import KanaDetail from "../components/KanaDetail.svelte";

  export let kana = "";
  export let syll = "";

  let modal;
</script>

<style>
  button {
    font-size: 1.5rem;
    background-color: var(--red-2);
    color: var(--white);
    border: none;
    margin: 0;
    width: 50px;
    height: 50px;
    transition: 0.25s ease-in-out;
    border-radius: 5px;
  }

  @media only screen and (min-width: 768px) {
    button {
      margin-bottom: 0.25rem;
    }

    button:hover {
      cursor: pointer;
      background-color: var(--red-1);
      text-decoration: none;
    }
  }

  @media only screen and (min-width: 1024px) {
  }
</style>

<button on:click={() => modal.show()}>{@html kana}</button>
<KanaDetail bind:this={modal} {kana} {syll} />
