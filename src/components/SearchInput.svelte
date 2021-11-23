<script>
  export let items;
  export let onSearch;
  export let onClear;

  let searching = "";
  let displaySearchList = false;
  $: itemsToDisplay = items.filter((it) => filterItems(it, searching));

  const filterItems = (item, keyword) => {
    return (
      item.name.includes(keyword) ||
      item.alias.some((it) => it.includes(keyword))
    );
  };

  const handleFocus = () => {
    searching = "";
    displaySearchList = true;
    onClear();
  };

  const handleInput = (e) => {
    searching = e.target.value;
  };

  const handleLoseFocus = (e) => {
    const isClickResultItem =
      e && e.relatedTarget && e.relatedTarget.classList.contains("result-item");
    if (!isClickResultItem) {
      displaySearchList = false;
    }
  };

  const handleClickResultItem = (item) => () => {
    searching = item.name;
    displaySearchList = false;
    onSearch(item);
  };
</script>

<div class="relative {$$props.class}">
  <div class="relative rounded-md shadow-sm">
    <input
      id="search"
      class="bg-gray-200 appearance-none border-2 border-gray-200 rounded-md w-full py-2 pl-2 pr-10 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-blue-400"
      autocomplete="off"
      type="text"
      placeholder="Search"
      value={searching}
      on:input={handleInput}
      on:focus={handleFocus}
      on:focusout={handleLoseFocus}
    />
    <div class="absolute inset-y-0 right-0 flex items-center pr-2">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-6 w-6 stroke-current text-gray-400"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M19 9l-7 7-7-7"
        />
      </svg>
    </div>
  </div>
  {#if displaySearchList}
    <div
      class="absolute rounded-md border-2 border-gray-200 divide-y divide-gray-200 py-1 px-2 mt-2 max-h-52 overflow-y-auto w-full bg-white"
    >
      {#each itemsToDisplay as item}
        <button on:click={handleClickResultItem(item)} class="result-item">
          {#if item.image}
            <img
              class="h-6 w-6 mr-2 rounded-sm"
              src={item.image}
              alt={item.name}
            />
          {/if}
          <p>{item.name}</p>
          {#if item.alias.length}
            <p class="text-gray-400">( {item.alias.join(", ")} )</p>
          {/if}
        </button>
      {/each}
    </div>
  {/if}
</div>

<style lang="postcss">
  .result-item {
    @apply px-2 py-1 flex items-center w-full;
  }
</style>
