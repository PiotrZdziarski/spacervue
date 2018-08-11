<template>
    <div :style="style" class="item"></div>
</template>

<script>
    export default {
        name: "Item",
        props: {
            item: {
                type: Object,
                required: true,
            },
        },
        data() {
            return {
                photo: this.item.links[0].href,
                title: this.item.data[0].title,
            }
        },
        computed: {
            style() {
                return `background-image: url("${this.photo}")`;
            },
        },
    };
</script>

<style lang="scss" scoped>
    .item {
        min-width: 40vw;
        height: 140px;
        background-size: cover;
        background-repeat: no-repeat;
        background-position: 50%;

        @media(min-width: 476px) {
            height: 220px;
        }

        @media(min-width: 768px) {
            height: 220px;
            min-width: 25vw;
        }

        @media(min-width: 1024px) {
            height: 320px;
        }
   }
</style>