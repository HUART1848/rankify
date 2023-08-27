<script lang="ts">
    import { artists } from "../stores";
    import Results from "./results.svelte";
    
    let currentArtists: string[];
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

    function roundArtists(round: number):String[] {
        let ret = currentMatches[round].map((i) => currentArtists[i]);
        return ret;
    }
</script>

<match>  
    {#if currentRound < currentMatches.length - 1}
        <button on:click={() => nextMatch(0)}>{roundArtists(currentRound)[0]}</button>
        <button on:click={() => nextMatch(1)}>{roundArtists(currentRound)[1]}</button>

        <p>Round {currentRound+1} of {currentMatches.length}</p>
        <p>Current match : {roundArtists(currentRound)}</p>
    {:else}
        <Results artists={currentArtists} scores={scores}></Results>
    {/if}
</match>

<style>

</style>
