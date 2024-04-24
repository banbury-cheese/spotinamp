<script lang="ts">
  export let number: number;
</script>

<div class="numberLabel">
  {number}
</div>

<style lang="scss">
  .numberLabel {
    @apply w-8 h-8 border-inherit border rounded-[8rem] -my-[1px] flex-shrink-0 flex justify-center items-center;
  }
</style>
