<script lang="ts">
    export let artists: string[];
    export let scores: number[];
</script>

<results>
    <h2>Résultats:</h2>

    {#each artists as artist, i}
        <p>{artist} : {scores[i]}</p>
    {/each}
</results>

<style>

</style>
