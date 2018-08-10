<template>
  <div class="app">
      <div class="wrapper">
        <HeroImage/>
        <Claim/>
        <search-input v-model="searchValue" @input="handleInput"/>
      </div>
  </div>
</template>

<script>
    import axios from 'axios';

    const API = 'https://images-api.nasa.gov/search';
    import debounce from 'lodash.debounce';
    import Claim from "@/components/Claim";
    import SearchInput from "@/components/SearchInput";
    import HeroImage from "@/components/HeroImage";

    export default {
        name: 'Search',
        components: {
            HeroImage,
            Claim,
            SearchInput
        },
        data() {
            return {
                searchValue: '',
                results: [],
            };
        },
        methods: {
            handleInput: debounce(function() {
                console.log(this.searchValue);
                const SELF = this;
                axios.get(`${API}?q=${this.searchValue}&media_type=image`)
                    .then(function(response) {
                        SELF.results = response.data.collection.items;
                    })
                    .catch((error) => {
                        console.log(error);
                    });
            }, 500),
        }
    };
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800');
  * {
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
  body {
    margin: 0;
    padding: 0;
    font-family: Montserrat, sans-serif;
  }

  .wrapper {
    display: flex;
    margin:0;
    width: 100%;
    min-height: 100vh;
    padding: 30px;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
</style>