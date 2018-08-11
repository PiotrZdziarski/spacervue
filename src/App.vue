<template>
    <div :class="[{flexStart: step === 1}, 'wrapper']">
      <transition name="slide">
        <img src="./assets/logo.png" class="logo" v-if="step === 1">
      </transition>
      <transition name="fade">
        <HeroImage v-if="step === 0"/>
      </transition>
      <Claim v-if="step === 0"/>
      <search-input v-model="searchValue" @input="handleInput" :dark="step === 1"/>
      <div class="results" v-if="results && !loading && step === 1">
        <Item
            v-for="item in results"
            :item="item"
            :key="item.data[0].nasa_id"
            @click.native="handleModalOpen(item)"
        />
      </div>
      <div class="loading" v-if="step === 1 && loading"></div>
      <transition name="fade">
        <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false"/>
      </transition>
    </div>
</template>

<script>
    import axios from 'axios';

    const API = 'https://images-api.nasa.gov/search';
    import debounce from 'lodash.debounce';
    import Claim from "@/components/Claim";
    import SearchInput from "@/components/SearchInput";
    import HeroImage from "@/components/HeroImage";
    import Item from '@/components/Item';
    import Modal from '@/components/Modal'

    export default {
        name: 'Search',
        components: {
            HeroImage,
            Claim,
            SearchInput,
            Item,
            Modal,
        },
        data() {
            return {
                modalOpen: false,
                modalItem: null,
                loading: false,
                step: 0,
                searchValue: '',
                results: [],
            };
        },
        methods: {
            handleModalOpen(item) {
                this.modalOpen = true;
                this.modalItem = item;
            },
            handleInput: debounce(function() {
                this.loading = true;
                console.log(this.searchValue);
                const SELF = this;
                axios.get(`${API}?q=${this.searchValue}&media_type=image`)
                    .then(function(response) {
                        SELF.results = response.data.collection.items;
                        SELF.loading = false;
                        SELF.step = 1;
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

  .fade-enter-active, .fade-leave-active {
    transition: opacity .3s ease;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  .slide-enter-active, .slide-leave-active {
    transition: margin-top .3s ease;
  }
  .slide-enter, .slide-leave-to {
    margin-top: -50px;
  }

  .wrapper {
    display: flex;
    margin:0;
    width: 100%;
    position: relative;
    min-height: 100vh;
    padding: 30px;
    flex-direction: column;
    align-items: center;
    justify-content: center;

    &.flexStart {
      justify-content: flex-start;
    }

    .logo {
      width: 100px;
      position: absolute;
      top: 30px;
    }

    .results {
      display: grid;
      margin-top: 50px;
      grid-template-columns: 1fr 1fr;
      grid-gap: 20px;

      @media(min-width: 768px) {
        grid-template-columns: 1fr 1fr 1fr;
      }
    }
  }


  .loading {
    margin-top: 100px;
    display: inline-block;
    width: 64px;
    height: 64px;

    @media(min-width: 768px) {
      width: 90px;
      height: 90px;
    }
  }
  .loading:after {
    content: " ";
    display: block;
    width: 46px;
    height: 46px;
    margin: 1px;
    border-radius: 50%;
    border: 5px solid #1e3d4a;
    border-color: #1e3d4a transparent #1e3d4a transparent;
    animation: loading 1.2s linear infinite;
  }
  @keyframes loading {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }

</style>