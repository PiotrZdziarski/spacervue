<template>
    <div class="outerWrapper">
        <div class="innerWrapper">
            <div class="photo">
                <img class="image" :src="photo">
            </div>
            <div class="description">
                <h2 class="title">{{ title }}</h2>
                <p class="descriptionreal">
                    {{description}}
                </p>
            </div>
        </div>
        <div class="close" @click="$emit('closeModal')"></div>
    </div>
</template>

<script>
    export default {
        name: "Modal",
        props: {
            item: {
                type: Object,
                required: true,
            },
        },
        data() {
            return {
                photo: null,
                title: null,
                description: null,
            };
        },
        mounted() {
            this.photo =  this.item.links[0].href;
            this.title = this.item.data[0].title;
            this.description = this.item.data[0].description;
        }
    };
</script>

<style lang="scss" scoped>
    .outerWrapper {
        background: #f6f6f6;
        max-width: 100%;
        position: fixed;
        display: block;
        left: 0;

        @media(min-width: 1024px) {
            top: 50%;
            transform: translateY(-50%);
            max-width: 70%;
            left:0;
            right:0;
            margin: auto;
            box-shadow: 0 30px 30px - 10px rgba(0,0,0, .3);
        }

        @media(max-width: 1023.99px) {
            margin-top: -30px;
            width: 100%;
            height: 100%;
        }
    }

    .close {
        position: absolute;
        width: 30px;
        height: 30px;
        padding: 30px;
        right: 0;
        top: 0;
        cursor: pointer;

        &::before,
        &::after {
            position: absolute;
            top: 30px;
            right: 20px;
            content: '';
            width: 20px;
            height: 2px;
            background: black;
            display: block;
        }

        &::before {
            transform: rotate(45deg);
        }

        &::after {
            transform: rotate(-45deg);
        }
    }

    .innerWrapper {
        display: block;
        padding: 50px;
        justify-content: center;
        align-items: center;

        .description {
            min-width: 100%;
        }

        .photo {
            min-width: 100%;
            background: black;
        }
        @media(max-width: 1024px) {
            padding: 50px;
            .descriptionreal {
                overflow: hidden;
                display: -webkit-box;
                -webkit-line-clamp: 5;
                -webkit-box-orient: vertical;
            }
        }

        @media(min-width: 1024px) {
            display: flex;
            flex-direction: row;

            .photo {
                min-width: 60%;
                margin-right: 20px;
            }

            .description {
                min-width: 40%;
            }
        }
    }

    .descriptionreal {
        overflow: hidden;
        display: -webkit-box;
        -webkit-line-clamp: 19;
        -webkit-box-orient: vertical;
    }

    .image {
        width: 100%;
    }

    .title {
        color: #1e3d4a
    }
</style>