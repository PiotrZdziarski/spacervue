<template>
   <div class="wrapper">
        <div class="search">
            <label for="search">Search</label>
            <input
               id="search"
               v-model="searchValue"
               name="search"
               @input="handleInput"
            />
            <ul>
                <li v-for="item in results" :key="item.data[0].nasa_id">
                    <p>{{ item.data[0].description}} </p>
                </li>
            </ul>
        </div>
   </div>
</template>

<script>
import axios from 'axios';

const API = 'https://images-api.nasa.gov/search';
import debounce from 'lodash.debounce';

export default {
   name: 'Search',
   data() {
       return {
           searchValue: '',
           results: [],
       };
   },
   methods: {
       handleInput: debounce(function() {
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
<style lang="scss" scoped>
    .wrapper {
        display: flex;
        margin:0;
        width: 100%;
        padding: 30px;
        flex-direction: column;
        align-items: center;
    }

    .search {
        width: 250px;
        display: flex;
        flex-direction: column;
    }

    input {
        height: 30px;
        border: 0;
        border-bottom: 1px solid black;
    }

    label {
        font-family: Montserrat, sans-serif;
    }
</style>
