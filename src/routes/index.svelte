<script>
  import PaginationPro from "$lib/PaginationPro.svelte";

  let current_page = 1;
  let last_page = 20;
  /**
   * @type {number | undefined}
   */
  let between_page = 3;

  // @ts-ignore
  const changePage = event => {
    current_page = event.detail.page
  };
</script>

<div class="w-full mx-auto my-8">
  <h1 class="text-center text-lg font-semibold text-orange-600 my-4">
    Svelte Pagination Pro
  </h1>
  <PaginationPro
    on:goToPage={changePage}
    {current_page}
    {last_page}
    {between_page}
  />
</div>
