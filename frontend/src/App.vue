<template>
  <div id="app">
    <searchbar v-model="searchQuery" @submit="onSubmit" />

    <b-container>
      <template v-if="searchResults.length > 0">
        <result-card
          v-for="(item, index) in searchResults"
          :key="`resultCard-${index}`"
          :number="index + 1"
          :content="item"
        />
      </template>

      <template v-else>
        <div class="text-secondary text-center">Keine Ergebnisse!</div>
      </template>
    </b-container>

  </div>
</template>

<script>
import resultCard from './components/ResultCard.vue';
import searchbar from './components/Searchbar.vue';
import axios from 'axios';

export default {
  name: 'App',

  components: {
    resultCard,
    searchbar
  },

  metaInfo: {
    title: 'Suchmaschinen template'
  },

  data() {
    return {
      searchQuery: '',
      searchResults: []
    }
  },

  methods: {
    onSubmit() {
      // TODO: Sprechen Sie hier Ihr eigenes Backend an

      axios.get(
        `https://jsonplaceholder.typicode.com/posts`,
        {
          params: {
            query: this.searchQuery
          },
        }
      )
        .then((response) => {
          if (response.data === null) {
            this.searchResults = [];
          } else {
            this.searchResults = response.data;
          }
        })
        .catch((error) => {
          console.log(error);
          this.searchResults = []
        })
    }
  }
}
</script>
