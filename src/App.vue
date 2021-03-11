<template>
  <header id="header">
    <Logo />
    <div class="header-search">
      <input type="text" placeholder="Search" autocomplete="false" v-model="search">
    </div>
  </header>
  <main class="background">
    <div class="grid">
      <Card v-for="(res, key) in filterSearch" 
        :name="res.name" 
        :image="res.image"
        :location="res.location.name"
        :gender="res.gender"
        :lengthOfEps="res.episode.length"
        @click="cardInfo = res"
        :key="key" 
      />
    </div>
    <div id="popup" v-if="Object.keys(cardInfo).length !== 0" @click="cardInfo = {}">
      <div class="popup-inside">
        <Card
          :name="cardInfo.name" 
          :image="cardInfo.image"
          :location="cardInfo.location.name"
          :gender="cardInfo.gender"
          :lengthOfEps="cardInfo.episode.length"
        />
      </div>
    </div>
  </main>
  <footer id="footer">
    <button v-if="info.prev" @click="getNewContent(info.prev)">pre</button>
    <button v-if="info.next" @click="getNewContent(info.next)">next</button>
  </footer>
</template>

<script>
import axios from 'axios'
import Logo from "./components/Logo.vue"
import Card from "./components/Card.vue"
import './App.css'

export default {
  components: {
    Logo,
    Card
  },
  data() {
    return {
      showCard: false,
      results: [],
      info: {},
      cardInfo: {},
      search: ''
    }
  },
  methods: {
    // Page next and back method
    getNewContent(url) {
      axios.get(url).then(({data}) => {
        this.results = data.results
        this.info = data.info
      })
    }
  },
  computed: {
    // Filter search results
    filterSearch() {
      return this.results.filter(char => char.name.toLowerCase().includes(this.search.toLowerCase()))
    }
  },
  // Get characters on load
  beforeMount() {
    axios.get('https://rickandmortyapi.com/api/character/').then(({ data }) => {
      this.results = data.results
      this.info = data.info
    })
  }
};
</script>

<style>
  #header {
    display: flex;
    flex-direction: row;
    padding: 1rem 2.5rem;
    justify-content: space-between;
    background-color: #353c42;
    box-shadow: 0 0 .8rem .8em #353c42;
    z-index: 1;
  }

  .header-search {
    display: flex;
    width: 50%;
  }

  .header-search input {
    width: 100%;
    padding: 0 0 0 10px;
  }

  .grid {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-gap: 3rem;
  }

  #popup {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 99999;
    width: 100vw;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: rgba(0,0,0,0.45);
  }

  .popup-inside {
    display: inline-block;
  }

  #footer {
    display: flex;
    background-color: #353c42;
    align-content: center;
    justify-content: center;
    padding: 10px 0;
    box-shadow: 0 0 .8rem .8em #353c42;
    z-index: 1;
  }
</style>
