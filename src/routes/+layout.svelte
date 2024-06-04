<script lang="ts">
  import Piano from "$lib/components/Piano.svelte";
  import SideConsole from "$lib/components/SideConsole.svelte";
  import MainSection from '$lib/components/MainSection.svelte';
  import "../app.css";
  export let data;

  import { entries } from '$lib/stores';
	entries.set(data.entries);
</script>

<body>
  <div class="piano">
    <Piano/>
  </div>
  <MainSection>
    <slot />
  </MainSection>
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
