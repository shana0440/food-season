<script>
  export let item;

  const formatInSeasonPeriods = (periods) => {
    if (periods[0].start === 1 && periods[0].end === 12) {
      return "全年";
    }
    return periods
      .map((it) => {
        if (it.start === it.end) {
          return `${it.start}月`;
        } else if (it.start > it.end) {
          return `${it.start}月到隔年${it.end}月`;
        }
        return `${it.start} - ${it.end}月`;
      })
      .join(", ");
  };
</script>

<div
  class="px-1 py-1 border-2 border-gray-300 rounded-md clear-both {item.type} {$$props.class}"
>
  <div class="flex mb-2">
    <h2 class="title">{item.name}</h2>
    {#if item.summary}
      <p class="summary">
        {item.summary}
      </p>
    {/if}
  </div>
  <div class="mb-2">盛產期：{formatInSeasonPeriods(item.periods)}</div>
  <div class="flex">
    {#if item.image}
      <img
        loading="lazy"
        src={item.image}
        alt={item.name}
        class="rounded-md h-40 w-40 mr-2 object-cover"
      />
    {/if}
    {#if item.description}
      <p>{item.description}</p>
    {/if}
  </div>
  {#if item.href}
    <a class="link" target="_blank" href={item.href}>看更多</a>
  {/if}
</div>

<style lang="postcss">
  .title {
    @apply font-semibold mr-2;
  }

  .summary {
    @apply px-2 font-semibold text-white rounded-md;
  }

  .link {
    @apply px-3 py-1 border-2 rounded-lg font-semibold float-right;
  }

  .fruit .title {
    @apply text-red-400;
  }
  .fruit .summary {
    @apply bg-red-400;
  }
  .fruit .link {
    @apply text-red-400 border-red-400;
  }

  .vegetable .title {
    @apply text-green-600;
  }
  .vegetable .summary {
    @apply bg-green-600;
  }
  .vegetable .link {
    @apply text-green-600 border-green-600;
  }
</style>
