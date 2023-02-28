<script>
  import Header from './components/Header.svelte';
  import ListOptions from './components/ListOptions.svelte';
</script>

<main>
  <div class="container">
    <Header />
    <ListOptions />
  </div>
</main>

<style>
  * {
    margin: 0;
    padding: 0;
    border: 0;
    outline: 0;
    text-decoration: none;
    list-style: none;
    box-sizing: border-box;
  }

  :root {
    /* COLOR ROOT */
    --color-white: #ffffff;
  }

  main {
    font-family: Helvetica, sans-serif;
    line-height: 1.7;
    width: 100%;
    margin: auto;
    display: flex;
    justify-content: center;
    height: 100vh;
    background-color: #64748b;
  }

  .container {
    padding: 20px;
  }
</style>
