<script>
    import KanaCheckBox from "./KanaCheckBox.svelte";

    export let kana = [];
</script>

<style>
    table {
        display: block;
        width: 100%;
        overflow-y: scroll;
    }
</style>

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
                        <KanaCheckBox id={character.id} code={character.code} />
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
