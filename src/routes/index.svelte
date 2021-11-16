<script>
  import fruitsSource from "../data/fruits.json";
  import vegetablesSource from "../data/vegetables.json";
  import Card from "../components/Card.svelte";
  import Button from "../components/Button.svelte";

  const fruits = fruitsSource.map((it) => ({ ...it, type: "fruit" }));
  const vegetables = vegetablesSource.map((it) => ({
    ...it,
    type: "vegetable",
  }));

  let selectedMonth = new Date().getMonth() + 1;
  $: foodsToDisplay = [
    ...filterFoodsByMonth(fruits, selectedMonth),
    ...filterFoodsByMonth(vegetables, selectedMonth),
  ];

  const monthInPeriod = (period, month) => {
    if (period.start <= period.end) {
      return period.start <= month && period.end >= month;
    } else {
      return period.start <= month || period.end >= month;
    }
  };

  const filterFoodsByMonth = (foods, month) => {
    if (month === null) {
      return foods;
    } else {
      return foods.filter((food) => {
        return food.periods.some((period) => monthInPeriod(period, month));
      });
    }
  };

  const handleSelectMonth = (month) => () => {
    selectedMonth = month;
  };
</script>

<section class="my-2 text-center">
  <Button isSelected={selectedMonth == null} on:click={handleSelectMonth(null)}>
    全部
  </Button>
  <Button isSelected={selectedMonth == 1} on:click={handleSelectMonth(1)}>
    1月
  </Button>
  <Button isSelected={selectedMonth == 2} on:click={handleSelectMonth(2)}>
    2月
  </Button>
  <Button isSelected={selectedMonth == 3} on:click={handleSelectMonth(3)}>
    3月
  </Button>
  <Button isSelected={selectedMonth == 4} on:click={handleSelectMonth(4)}>
    4月
  </Button>
  <Button isSelected={selectedMonth == 5} on:click={handleSelectMonth(5)}>
    5月
  </Button>
  <Button isSelected={selectedMonth == 6} on:click={handleSelectMonth(6)}>
    6月
  </Button>
  <Button isSelected={selectedMonth == 7} on:click={handleSelectMonth(7)}>
    7月
  </Button>
  <Button isSelected={selectedMonth == 8} on:click={handleSelectMonth(8)}>
    8月
  </Button>
  <Button isSelected={selectedMonth == 9} on:click={handleSelectMonth(9)}>
    9月
  </Button>
  <Button isSelected={selectedMonth == 10} on:click={handleSelectMonth(10)}>
    10月
  </Button>
  <Button isSelected={selectedMonth == 11} on:click={handleSelectMonth(11)}>
    11月
  </Button>
  <Button isSelected={selectedMonth == 12} on:click={handleSelectMonth(12)}>
    12月
  </Button>
</section>

<section class="grid grid-cols-2 gap-2">
  {#each foodsToDisplay as fruit}
    <Card item={fruit} />
  {/each}
</section>
