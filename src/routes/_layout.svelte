<script>
</script>

<svelte:head>
  <title>Food in Season</title>
</svelte:head>

<main class="container mx-auto app">
  <slot />
</main>

<footer
  class="border-t-2 border-dashed border-gray-200 mt-4 text-center mx-4 py-2"
>
  <h6 class="text-xs font-semibold">資料來源</h6>
  <a
    class="text-xs text-blue-500 underline"
    target="_blank"
    href="https://ezgo.coa.gov.tw/Fruit/TW/Season_Fruits_All"
  >
    農業易遊網
  </a>
</footer>

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
