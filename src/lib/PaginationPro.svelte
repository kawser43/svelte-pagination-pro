<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  import "./app.css";
  export /**
   * @type {number}
   */
  let current_page;
  export /**
   * @type {number}
   */
  let last_page;
  export let between_page = 3; // default is 3

  /**
   * @type {any[]}
   */
  let page_links = [];

  const customPageLinks = (
    /** @type {number} */ current_page,
    /** @type {number} */ last_page,
    /** @type {number} */ between_page
  ) => {
    let range = [];

    let to_before = 0;
    let available_before = current_page - 1;
    if (available_before > between_page) {
      to_before = between_page;
    } else {
      to_before = available_before;
    }

    if (to_before > 0) {
      let start = current_page - to_before;
      for (start; start < current_page; start++) {
        range.push(start);
      }
    }

    range.push(current_page);

    let to_after;
    let available_after = last_page - current_page; // 6 - 5 = 1
    if (available_after > between_page) {
      to_after = current_page + between_page;
    } else {
      to_after = current_page + available_after;
    }

    if (to_after > 0) {
      for (let i = current_page + 1; i < to_after + 1; i++) {
        range.push(i);
      }
    }

    page_links = range;
  };

  $: customPageLinks(current_page, last_page, between_page);

  const goToPage = (/** @type {number} */ page) => {
    dispatch("goToPage", { page });
  };
</script>

<ul class="text-center">
  <li
    on:click={() => goToPage(1)}
    class={`
          inline px-3 py-1 border-gray-200 rounded m-1 cursor-pointer 
           hover:bg-orange-500 hover:text-white transation duration-300
           bg-gray-100 border text-black
        `}
  >
    First
  </li>
  {#each page_links as link}
    <li
      on:click={() => goToPage(link)}
      class={`
          inline px-3 py-1 border-gray-200 rounded m-1 cursor-pointer 
           hover:bg-orange-500 hover:text-white transation duration-300
          ${
            current_page == link
              ? "bg-orange-600 border text-white"
              : "bg-gray-100 border text-black"
          }
        `}
    >
      {link}
    </li>
  {/each}
  <li
      on:click={() => goToPage(last_page)}
      class={`
          inline px-3 py-1 border-gray-200 rounded m-1 cursor-pointer 
           hover:bg-orange-500 hover:text-white transation duration-300
           bg-gray-100 border text-black
        `}
    >
      Last
    </li>
</ul>
