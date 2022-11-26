<template>
  <div class="search">
    <input type="text" v-model="query" @keypress.enter="handleSearch" placeholder="Please enter a word"/>
    <button @click="handleSearch">Search</button>
    <select v-model="limit" @change="handleSearch">
      <option value="1">1</option>
      <option value="10">10</option>
      <option value="20">20</option>
      <option value="30">30</option>
    </select>
  </div>
</template>

<script>
export default {
  name: 'Search',
  data() {
    return {
      query: 'trending',
      limit: 10,
    }
  },
  methods: {
    handleSearch() {
      this.$emit('SearchRequested', this.query, this.limit)
    }
  }
}
</script>

<style>
  .search {
    margin-top: 30px;
  }

  .search input {
    width: 800px;
    padding: 30px;
    font-size: 32px;
    border: 1px solid #959595;
    border-radius: 30px;
  }

  .search button {
    min-width: 100px;
    padding: 30px;
    font-size: 32px;
    font-weight: bold;
    border-radius: 30px;
    border: none;
    background-color: #850da3;
    color: white;
    cursor: pointer;
  }

  .search button:hover {
    background-color: #6b0a84;
  }

  select {
    min-width: 50px;
    padding: 30px;
    font-size: 32px;
    color: white;
    background-color: #850da3;
    border-radius: 30px;
  }


</style>
