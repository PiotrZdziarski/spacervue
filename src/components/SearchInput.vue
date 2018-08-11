<template>
    <input
        id="search"
        name="search"
        :class="{ dark }"
        :value="value"
        @input="handleChange"
    />
</template>

<script>
    export default {
        name: "SearchInput",
        props: {
            value: {
                type: String,
                required: true,
            },
            dark: {
                type: Boolean,
                default: false,
            },
        },
        methods: {
            handleChange(e) {
                this.$emit('input', e.target.value);
            },
        },
    };
</script>

<style lang="scss" scoped>
    input {
        width: 250px;
        margin-top: 50px;
        display: flex;
        height: 30px;
        border: 0;
        background: none;
        text-align: center;
        font-weight: 300;
        font-family: 'Montserrat', sans-serif;
        font-size: 18px;
        color:white;
        border-bottom: 1px solid white;
        transition: box-shadow .3s ease-out;

        @media (min-width: 1024px) {
            font-weight: 400;
        }
    }

    input:focus {
        outline: none;
        box-shadow: 0 10px 20px -8px rgba(255,255,255, .5);
    }

    label {
        font-family: Montserrat, sans-serif;
    }
    .dark {
        color: #1e3d4a;
        border-bottom-color: #1e3d4a;
    }

    .dark:focus {
        box-shadow: 0 5px 10px -3px rgba(#1e3d4a, .5);
    }
</style>