<script>
  import fruits from "../data/fruits.json";
  import Card from "../components/Card.svelte";

  let fruitsToDisplay = fruits;

  const monthInPeriod = (period, month) => {
    if (period.start <= period.end) {
      return period.start <= month && period.end >= month;
    } else {
      return period.start <= month || period.end >= month;
    }
  };

  const handleSelectMonth = (month) => () => {
    if (month === null) {
      fruitsToDisplay = fruits;
    } else {
      fruitsToDisplay = fruits.filter((fruit) => {
        return fruit.periods.some((period) => monthInPeriod(period, month));
      });
    }
  };
</script>

<section class="my-2 text-center">
  <button class="btn" on:click={handleSelectMonth(null)}>全部</button>
  <button class="btn" on:click={handleSelectMonth(1)}>1月</button>
  <button class="btn" on:click={handleSelectMonth(2)}>2月</button>
  <button class="btn" on:click={handleSelectMonth(3)}>3月</button>
  <button class="btn" on:click={handleSelectMonth(4)}>4月</button>
  <button class="btn" on:click={handleSelectMonth(5)}>5月</button>
  <button class="btn" on:click={handleSelectMonth(6)}>6月</button>
  <button class="btn" on:click={handleSelectMonth(7)}>7月</button>
  <button class="btn" on:click={handleSelectMonth(8)}>8月</button>
  <button class="btn" on:click={handleSelectMonth(9)}>9月</button>
  <button class="btn" on:click={handleSelectMonth(10)}>10月</button>
  <button class="btn" on:click={handleSelectMonth(11)}>11月</button>
  <button class="btn" on:click={handleSelectMonth(12)}>12月</button>
</section>

<section class="grid grid-cols-2 gap-2">
  {#each fruitsToDisplay as fruit}
    <Card item={fruit} />
  {/each}
</section>

<style lang="postcss">
  .btn {
    @apply w-14 py-1 px-2 font-semibold rounded-md border-2 border-gray-300;
  }
</style>
