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
        }
        return `${it.start} - ${it.end}月`;
      })
      .join(", ");
  };
</script>

<div
  class="px-1 py-1 border-2 border-gray-300 rounded-md clear-both {$$props.class}"
>
  <div class="flex mb-2">
    <h2 class="font-semibold text-red-400 mr-2">{item.name}</h2>
    <p class="px-2 font-semibold bg-red-400 text-white rounded-md">
      {item.summary}
    </p>
  </div>
  <div class="mb-2">盛產期：{formatInSeasonPeriods(item.periods)}</div>
  <div class="flex">
    <img src={item.image} alt={item.name} class="rounded-md h-40 mr-2" />
    <p>{item.description}</p>
  </div>
  <a
    class="px-3 py-1 border-2 border-red-400 rounded-lg text-red-400 font-semibold float-right"
    target="_blank"
    href={item.href}
  >
    看更多
  </a>
</div>

<style lang="postcss"></style>
