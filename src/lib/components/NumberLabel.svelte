<script lang="ts">
  export let number: number;
</script>

<div class="numberLabel">
  {number}
</div>

<style lang="scss">
  .numberLabel {
    @apply rounded-[10rem] border-black border w-8 h-8 flex-shrink-0 flex justify-center items-center mx-2;
  }
</style>
