<script>
  import KanaButton from "./KanaButton.svelte";

  export let kana = [];
</script>

<style>
  table {
    display: inline-block;
    width: 100%;
    max-width: 350px;
    overflow-x: scroll;
  }

  th {
    font-weight: normal;
    font-family: "Noto Sans Bold";
  }

  td {
    text-align: center;
    padding: 0.1rem;
  }

  span {
    display: block;
  }

  .last-row-item {
    font-family: "Noto Sans Bold";
  }

  .char-id {
    display: none;
  }

  @media only screen and (min-width: 768px) {
    table {
      max-width: 700px;
      overflow-x: unset;
    }

    td {
      padding: 0.25rem;
    }
  }

  @media only screen and (min-width: 768px) and (orientation: landscape) {
    table {
      overflow-y: scroll;
    }
  }

  @media only screen and (min-width: 1024px) {
    table {
      max-width: 900px;
      overflow-y: unset;
    }

    td {
      padding: 0.75rem;
    }
  }
</style>

<div class="wrapper">
  <table>
    <tr>
      <th>-</th>
      <th>k-</th>
      <th>s-</th>
      <th>t-</th>
      <th>n-</th>
      <th>h-</th>
      <th>m-</th>
      <th>y-</th>
      <th>r-</th>
      <th>w-</th>
      <th>n</th>
    </tr>
    {#each kana as row}
      <tr>
        {#each row as character}
          {#if character.code != "none"}
            <td>
              <KanaButton kana={character.code} syll={character.syll} />
              <span>{character.syll}</span>
              <span class="char-id">{character.id}</span>
            </td>
          {:else}
            <td>-</td>
          {/if}
          {#if character.isLastInRow}
            <td class="last-row-item">{row[0].syll.slice(-1)}</td>
          {/if}
        {/each}
      </tr>
    {/each}
  </table>
</div>
