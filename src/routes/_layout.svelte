<script>
</script>

<svelte:head>
  <title>Food in Season</title>
</svelte:head>

<main class="container mx-auto app">
  <slot />
</main>

<style global lang="postcss">
  @tailwind base;
  @tailwind components;
  @tailwind utilities;

  @screen lg {
    .app {
      width: 960px;
    }
  }
</style>
