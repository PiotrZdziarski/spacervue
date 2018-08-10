<template>
    <div class="claimwrapper">
        <h1 class="claim">Spacer</h1>
        <p class="subclaim">
            Begin your journey through amazing galaxy,
            and discover places you never even heard of.
        </p>
        <p class="subclaim">
            Type anything space-related to start.
        </p>
    </div>
</template>

<script>
    export default {
        name: "Claim"
    }
</script>

<style lang="scss" scoped>
    .claimwrapper {
        display: flex;
        text-align: center;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    .claim {
        font-size: 50px;
        margin:0;
    }

    .subclaim {
        margin: 20px 0 0 0;
        font-size: 15px;
    }
</style>