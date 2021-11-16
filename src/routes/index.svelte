<script>
  import fruits from "../data/fruits.json";
  import Card from "../components/Card.svelte";
</script>

<h1>Food in Season</h1>

<section class="grid grid-cols-2 gap-2">
  {#each fruits as fruit}
    <Card item={fruit} />
  {/each}
</section>

<style lang="postcss">
</style>
