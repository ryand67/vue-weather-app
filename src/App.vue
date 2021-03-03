<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input type="text" placeholder="Search..." class="search-bar">
      </div>
    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      api_key: 'a6957c1b49c6ff3ddbf191f7c07846ca'
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'montserrat', sans-serif;
}

#app {
  background-image: url('./assets/cold-bg.jpg');
}
</style>
