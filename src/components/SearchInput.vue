<template>
    <div class="searchWrapper">
        <input
            id="search"
            v-model="searchValue"
            name="search"
            @input="handleInput"
        />
    </div>
</template>

<script>
    export default {
        name: "SearchInput"
    }
</script>

<style lang="scss" scoped>
    .searchWrapper {
        width: 250px;
        margin-top: 50px;
        display: flex;
        flex-direction: column;
    }

    input {
        height: 30px;
        border: 0;
        background: none;
        border-bottom: 1px solid black;
    }

    label {
        font-family: Montserrat, sans-serif;
    }
</style>