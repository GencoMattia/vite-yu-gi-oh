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

            archetypeList: [
                "Alien",
                "Dragon",
                "Fairy"
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
        <div class="col-12 text-bg-dark p-2 mb-2 text-center cards-counter">
            <h4>
                {{ cardsList.length }} cards has been found
            </h4>
        </div>
        <article v-for="card in cardsList" :key="card.id" class="col-2 me-2 mb-3">
            <MainSingleCard :card="card"/>
        </article>
    </section>
</template>

<style scoped lang="scss">
@use "../styles/partials/variables" as *;

    section {
        max-width: 1200px;
        background-color: white;
        margin: 0 auto;
    }
</style>