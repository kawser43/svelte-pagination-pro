# svelte-pagination-pro

A simple **Svelte** component to show and handle pagination

![Gif](https://raw.githubusercontent.com/kawser43/svelte-pagination-pro/main/static/demo.gif)

## Install

```
$ npm install svelte-pagination-pro
```

## Usage

```
<script>
  import PaginationPro from "svelte-pagination-pro";

  let current_page = 1;
  let last_page = 20;
  let between_page = 3; // default is 3

  const changePage = event => {
    // fetch new data depending on page and update page
    current_page = event.detail.page
  };
</script>

<main>
<PaginationPro
    on:goToPage={changePage}
    {current_page}
    {last_page}
    {between_page}
  />
</main>

```
