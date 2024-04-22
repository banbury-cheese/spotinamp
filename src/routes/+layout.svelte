<script lang="ts">
  import Piano from "$lib/components/Piano.svelte";
  import SideConsole from "$lib/components/SideConsole.svelte";
  import "../app.css";
  export let data;
</script>

<body>
  <div class="piano">
    <Piano entries={data.entries} />
  </div>
  <div class="musicSheet">
    <slot />
  </div>
  <div class="playerBody">
    <SideConsole />
  </div>
</body>

<style lang="scss">
  .piano {
    @apply z-[1] flex-shrink-0 overflow-auto w-[300px] xl:flex-shrink xl:basis-1/4 xl:min-w-[300px];
  }

  body {
    @apply w-screen h-screen flex;
  }

  .musicSheet {
    @apply flex-grow basis-1/2 h-full overflow-auto;
  }

  .playerBody {
    @apply basis-1/4 border-black border;
  }
</style>
