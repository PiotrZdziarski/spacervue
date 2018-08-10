<template>
   <div class="wrapper">
       <Claim/>
       <search-input/>
   </div>
</template>

<script>
import axios from 'axios';

const API = 'https://images-api.nasa.gov/search';
import debounce from 'lodash.debounce';
import Claim from "@/components/Claim";
import SearchInput from "@/components/SearchInput";

export default {
   name: 'Search',
    components: {
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
        height: 100vh;
        padding: 30px;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        background-image: url("../assets/background.jpg");
        background-repeat: no-repeat;
        background-size: cover;
    }
</style>
