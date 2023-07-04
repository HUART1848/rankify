<script lang="ts">
  import Match from "./lib/match.svelte";
  import Playlist from "./lib/playlist.svelte";

  import {artists} from "./stores";

  artists.update((value) => value = ["A", "B"]);
</script>

<main>
  <h1>Rankify</h1>

  <Match/>
</main>

<style>
</style>
