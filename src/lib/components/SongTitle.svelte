<script lang="ts">
  import type { SongEntry } from "$lib/types.js";
  export let song: SongEntry;
</script>

<div
  class="text-2xl tracking-tighter leading-6 border-b border-grey6 min-h-[calc(2rem-1px)] flex items-center i"
>
  <p>
    <span class="inline-block">{song.songname}</span>
    <span class="inline-block"><i>– {song.artistname}</i></span>
  </p>
</div>
