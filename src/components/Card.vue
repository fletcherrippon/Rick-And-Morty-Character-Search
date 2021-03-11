<template>
  <div class="card" :class="rank">
    <div>
        <span>Rank - {{rank}}</span>
    </div>
    <span>{{ name }} - {{ gender }} - {{ status }}</span>
    <div>
      <img :src="image" />
    </div>
    <div>
      {{location}}
    </div>
  </div>
</template>

<script>
export default {
  name: '',
  props: {
    name: String,
    image: String,
    gender: String,
    status: String,
    location: String,
    lengthOfEps: Number
  },
  computed: {
    // Create rank of character by number of epesides they have
    rank() {
      if (this.lengthOfEps > 20) return 'legendary'
      if (this.lengthOfEps > 10) return 'rare'
      if (this.lengthOfEps < 10 || !this.lengthOfEps) return 'common'
    }
  }
}
</script>

<style scoped>
  .card {
    padding: 10px;
    border-radius: 10px;
    border: 10px solid;
    margin:auto;
  }
  .card:hover {
    cursor: pointer;
  }
  .card.common {
    background: white;
    border-color: grey;
  }
  .card.legendary {
    background: orange;
    border-color: gold;
  }
  .card.rare {
    background: red;
    border-color: pink;
  }
  .card img {
    border-radius: 10px;
  }
</style>