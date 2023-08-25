<script lang="ts">
  import Match from "./lib/match.svelte";
  import Playlist from "./lib/playlist.svelte";

  import {artists} from "./stores";

  artists.update((value) => value = ["Drake", "Mozart", "Daft Punk", "100 Gecs"]);
</script>

<main>
  <h1>Rankify</h1>

  <Match/>
</main>

<style>
</style>
