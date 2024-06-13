<script>
import axios from 'axios';
import MainSingleCard from './MainSingleCard.vue';

export default {
    components: {
        MainSingleCard,
    },

    data() {
        return {
            cardsList: [

            ],
        };
    },

    methods: {
        getCards(){
            axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0')
            .then((response) => {
                // handle success
                console.log(response.data.data);
                this.cardsList = response.data.data;
            })
            .catch(function (error) {
                // handle error
                console.log(error);
            })
            .finally(function () {
                // always executed
            });
        }
    },

    created(){
        this.getCards();
    }
};
</script>

<template>
    <section class="row cards-wrapper align-items-stretch justify-content-center pt-4">
        <article v-for="card in cardsList" :key="card.id" class="col-2 me-1 mb-3">
            <MainSingleCard :card="card"/>
        </article>
    </section>
</template>

<style scoped lang="scss">
@use "../styles/partials/variables" as *;

    main {
        background-color: $appOrange;
        height: calc(100vh - 100px);
        overflow: auto;
    }
</style>