<template>
  <div id="app">
    <div class="searchArea">
      <Search v-on:SearchRequested="handleSearch"></Search>
    </div>
    <p v-if="isLoading" class="loading">Loading...</p>
    <Preview v-bind:gifs="gifs" v-bind:isLoading="isLoading"></Preview>
  </div>
</template>

<script>
import Search from './components/Search'
import Preview from './components/Preview'

export default {
  name: 'app',
  components: { Search, Preview },
  methods: {
    doQuery(url) {
      setTimeout(()=> {
        fetch(url)
          .then((res) => { return res.json() })
          .then((res) => {
            this.gifs = res.data;
            this.isLoading= false;
          })
      }, 1000);
    },
    handleSearch(query, limit) {
      this.gifs = [];
      this.isLoading = true;
      const url = `http://api.giphy.com/v1/gifs/search?q=${query}&api_key=GcORRpQjPDrXpyaiJgBQXx28DeHMycDm&limit=${limit}`
      this.doQuery(url);
    }
  },
  created() {
    const url = `http://api.giphy.com/v1/gifs/trending?api_key=GcORRpQjPDrXpyaiJgBQXx28DeHMycDm&limit=10`
    this.doQuery(url);
  },
  data() {
    return {
      isLoading: true,
      gifs: [],
    }
  },
}
</script>

<style lang="scss">

body {
  background-color: rgb(187, 225, 61);
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.searchArea {
  display: flex;
  justify-content: center;
}

p.loading {
  display: flex;
  justify-content: center;
  font-size: 32px;
  font-family: 'Courier New', Courier, monospace;
  font-weight: bold;
}
</style>
