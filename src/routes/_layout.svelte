<script>
</script>

<svelte:head>
  <title>Food in Season</title>
</svelte:head>

<main class="bg-gray-100">
  <slot />
</main>

<style global lang="postcss">
  @tailwind base;
  @tailwind components;
  @tailwind utilities;

  body {
    font-family: Roboto, -apple-system, BlinkMacSystemFont, Segoe UI, Oxygen,
      Ubuntu, Cantarell, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;
  }
</style>
