<template>
  <div>
    <ul v-if="gifs.length">
      <li v-for="gif in gifs" :key="gif.id">
        <img :src="gif.images.fixed_height.url" class="gifImage"/>
      </li>
    </ul>
    <p v-else-if="!isLoading" class="error">
      Something wrong!
    </p>
  </div>
</template>

<script>
export default {
  props: {
    gifs: {
      type: Array,
      default: null,
      required: false,
    },
    isLoading: {
      type: Boolean,
      default: true,
    }
  },
}
</script>

<style>
  ul {

  }

  li {
    list-style: none;
    float: left;
    margin: 10px;
  }

  .gifImage {
    border-radius: 30px;
    cursor: pointer;
  }

  p.error {
    display: flex;
    justify-content: center;
    font-size: 50px;
    margin-block: 50px;
    font-weight: bold;
    color: rgb(181, 3, 3);
  }
</style>
