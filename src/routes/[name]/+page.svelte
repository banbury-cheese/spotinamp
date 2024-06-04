<script lang="ts">
  import Page from "$lib/components/Page.svelte";
  import { currentEntry } from "$lib/stores";
  import { onMount } from "svelte";
  import type { Entry } from "$lib/types";
  import { page } from "$app/stores";
  export let data;
  $: entry = data.entries.find(
    (entry: Entry) => entry.slug === $page.params.name
  );

  $: currentEntry.set(entry);
  onMount(() => {});
</script>

{#if entry}
  {#key entry.slug}
    <Page></Page>
  {/key}
{/if}
