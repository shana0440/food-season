<script>
  export let isSelected;
</script>

<button class="btn {isSelected ? 'active' : ''}" on:click><slot /></button>

<style lang="postcss">
  .btn {
    @apply w-14 py-1 px-2 font-semibold rounded-md border-2 border-gray-300;
  }

  .active {
    @apply border-red-400;
  }
</style>
