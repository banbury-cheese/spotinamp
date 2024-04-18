<script lang="ts">
  import type { Entry } from "$lib/types";
  export let entries: Entry[];
</script>

{#each entries as entry}
  <div class="key-container">
    <a href="/{entry.slug}">
      <div
        class="h-20 flex justify-start items-center pl-[calc(12.5vw+16px)] hover:bg-gray-300 rounded-r-md"
      >
        {entry.name}
      </div>
    </a>
    <div class="black-key"></div>
  </div>
{/each}

<style lang="scss">
  .key-container {
    @apply border-black border border-l-0 -mt-[1px] relative rounded-r-md;

    &:nth-child(7n + 4),
    &:nth-child(7n),
    &:last-child {
      .black-key {
        display: none;
      }
    }

    .black-key {
      @apply h-10 bg-black absolute top-[3.75rem] w-[12.5vw] z-10 rounded-r-md;
    }
  }
</style>
