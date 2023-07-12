<script>
  import fruitsSource from "../data/fruits.json";
  import vegetablesSource from "../data/vegetables.json";
  import Card from "../components/Card.svelte";
  import Button from "../components/Button.svelte";
  import SearchInput from "../components/SearchInput.svelte";

  const FRUIT = "fruit";
  const VEGETABLE = "vegetable";
  const ALL_TYPES = [FRUIT, VEGETABLE];

  const fruits = fruitsSource.map((it) => ({ ...it, type: FRUIT }));
  const vegetables = vegetablesSource.map((it) => ({
    ...it,
    type: VEGETABLE,
  }));

  let selectedTypes = ALL_TYPES;
  $: isAllTypeSelected =
    selectedTypes.includes(FRUIT) && selectedTypes.includes(VEGETABLE);
  let selectedMonth = new Date().getMonth() + 1;
  let searchedFood = null;

  $: foodsToSearch = [
    ...filterFoodsByMonth(fruits, selectedMonth),
    ...filterFoodsByMonth(vegetables, selectedMonth),
  ].filter((it) => selectedTypes.includes(it.type));
  $: foodsToDisplay = searchedFood ? [searchedFood] : foodsToSearch;

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

  const handleSelectType = (type) => () => {
    if (type === null) {
      if (isAllTypeSelected) {
        selectedTypes = [];
      } else {
        selectedTypes = ALL_TYPES;
      }
    }
    if (selectedTypes.includes(type)) {
      selectedTypes = selectedTypes.filter((it) => it !== type);
    } else {
      selectedTypes = [...selectedTypes, type];
    }
  };

  const handleSearch = (item) => {
    searchedFood = item;
  };
  const handleClear = () => {
    searchedFood = null;
  };
  const monthOptions = [null, ...Array(12).fill(1).map((_, i) => i + 1).values()].map((it => {
    return {
      value: it,
      label: it ? `${it}月` : "全部"
    }
  }))
</script>

<section class="my-2 text-center">
  <Button isSelected={isAllTypeSelected} on:click={handleSelectType(null)}>
    全部
  </Button>
  <Button
    isSelected={selectedTypes.includes(FRUIT)}
    on:click={handleSelectType(FRUIT)}
  >
    水果
  </Button>
  <Button
    isSelected={selectedTypes.includes(VEGETABLE)}
    on:click={handleSelectType(VEGETABLE)}
  >
    蔬菜
  </Button>
</section>

<section class="my-2 text-center flex gap-1 justify-center">
  {#each monthOptions as option}
    <Button isSelected={selectedMonth == option.value} on:click={handleSelectMonth(option.value)}>
      {option.label}
    </Button>
  {/each}
</section>

<section class="mb-2">
  <SearchInput
    class="md:w-1/2 mx-auto"
    items={foodsToSearch}
    onSearch={handleSearch}
    onClear={handleClear}
  />
</section>

{#if foodsToDisplay.length}
  <section class="grid md:grid-cols-2 gap-2">
    {#each foodsToDisplay as food}
      <Card item={food} />
    {/each}
  </section>
{:else}
  <section>
    <p class="text-gray-400 text-center">沒有任何項目可以顯示</p>
  </section>
{/if}
