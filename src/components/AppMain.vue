<script>
import axios from 'axios';
import MainCardsWrapper from './MainCardsWrapper.vue';

export default {
    components: {
        MainCardsWrapper,
    },

    data() {
        return {
            cardsList: [

            ],
        };
    },

    methods: {
        
    }
};
</script>

<template>
    <main>
        <MainCardsWrapper />
    </main>
</template>

<style scoped lang="scss">
@use "../styles/partials/variables" as *;

    main {
        background-color: $appOrange;
        height: calc(100vh - 100px);
        overflow: auto;
    }
</style>