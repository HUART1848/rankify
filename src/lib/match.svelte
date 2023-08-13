<script lang="ts">
    import { artists } from "../stores";
    
    let currentArtists: String[];
    let currentRound: number;
    let currentMatches: number[][];

    let scores:number[];

    artists.subscribe((value) => {
        currentArtists = value;
        currentRound = 0;
        currentMatches = getMatches(value.length);

        scores = Array(value.length).fill(0);
    });

    function getMatches(n: number):number[][] {
        let idx = [...Array(n).keys()];
        return idx.flatMap((a, i) => idx.slice(i + 1).map( b => [a, b] ));;
    }

    function nextMatch(winner: number) {
        if (currentRound == currentArtists.length) {
            return
        }

        scores[currentMatches[currentRound][winner]] += 1;
        currentRound += 1;
    }
</script>

<match>
    <button on:click={() => nextMatch(0)}>A</button>
    <button on:click={() => nextMatch(1)}>B</button>

    {#each scores as s}
        <p>{s}</p>
    {/each}
</match>

<style>

</style>
