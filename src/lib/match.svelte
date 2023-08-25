<script lang="ts">
    import { artists } from "../stores";
    
    let currentArtists: String[];
    let currentRound: number;
    let currentMatches: number[][];

    let scores:number[];

    artists.subscribe((value) => {
        currentArtists = value;
        currentRound = 0;
        currentMatches = generateMatches(value.length);

        scores = Array(value.length).fill(0);
    });

    function generateMatches(n: number):number[][] {
        let idx = [...Array(n).keys()];
        return idx.flatMap((a, i) => idx.slice(i + 1).map( b => [a, b] ));;
    }

    function nextMatch(winner: number) {
        if (currentRound == currentMatches.length - 1) {
            return
        }

        scores[currentMatches[currentRound][winner]] += 1;
        currentRound += 1;
    }

    function getRoundArtists(round: number):String[] {
        let ret = currentMatches[round].map((i) => currentArtists[i]);
        return ret;
    }
</script>

<match>  
    {#if currentRound < currentMatches.length - 1}
        <button on:click={() => nextMatch(0)}>A</button>
        <button on:click={() => nextMatch(1)}>B</button>

        <p>Round {currentRound+1} of {currentMatches.length}</p>
        <p>Current match : {getRoundArtists(currentRound)}</p>
    {:else}
        <p>Résultat:</p>
    {/if}

    {#each scores as s, index}
        <p>{currentArtists[index]} : {s}</p>
    {/each}
</match>

<style>

</style>
