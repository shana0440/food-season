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
  <h6 class="text-xs font-semibold mb-2">資料來源</h6>
  <div
    class="container grid grid-cols-2 divide-x divide-gray-200 divide-dashed"
  >
    <a
      class="link"
      target="_blank"
      href="https://ezgo.coa.gov.tw/Fruit/TW/Season_Fruits_All"
    >
      農業易遊網
    </a>
    <a
      class="link"
      target="_blank"
      href="https://4b1q.coa.gov.tw/upload/files/coa_4b1q_QA/8/%E5%90%84%E6%9C%88%E4%BB%BD%E5%8F%AF%E4%BE%9B%E6%87%89%E4%B9%8B%E5%9C%8B%E7%94%A2%E8%94%AC%E8%8F%9C%E3%80%81%E6%B0%B4%E6%9E%9C%E5%93%81%E9%A0%85%E5%8F%83%E8%80%83%E8%B3%87%E6%96%99.pdf"
    >
      各月份可供應之國產蔬菜、水果品項參考資料
    </a>
  </div>
</footer>

<style global lang="postcss">
  @tailwind base;
  @tailwind components;
  @tailwind utilities;

  .link {
    @apply text-xs text-blue-500 underline;
  }

  @screen lg {
    .app {
      width: 960px;
    }
  }
</style>
