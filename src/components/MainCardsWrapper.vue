<script>
import axios from 'axios';
import MainSingleCard from './MainSingleCard.vue';
import MainCardSelector from "./MainCardSelector.vue"

export default {
    components: {
        MainSingleCard,
        MainCardSelector,
    },

    data() {
        return {
            cardsList: [

            ],

            archetypeList: [

            ],

            selectedArchetype: "Tutti",

            filteredCards: [
                
            ],
        };
    },

    methods: {
        getCards(){
            axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=100&offset=0')
            .then((response) => {
                // handle success
                console.log(response.data.data);
                this.cardsList = response.data.data;
                this.filteredCards = this.cardsList;
            })
            .catch(function (error) {
                // handle error
                console.log(error);
            })
            .finally(function () {
                // always executed
            });
        },

        getArchetypes(){
            axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=100&offset=0')
            .then((response) => {
                // handle success
                const cards = response.data.data;
                const allArchetypes = [
                    "Tutti",
                ];

                cards.map(function(card) {
                    if (card.archetype !== undefined && !allArchetypes.includes(card.archetype)) {
                        allArchetypes.push(card.archetype);
                    }
                });
                
                this.archetypeList = allArchetypes;
            })
            .catch(function (error) {
                // handle error
                console.error('Errore durante il recupero degli archetipi:', error);
            })
            .finally(function () {
                // always executed
            });
        },

        filterCardsByArchetype(selectedArchetype) {
            this.selectedArchetype = selectedArchetype;

            if (selectedArchetype === 'Tutti') {
                this.filteredCards = this.cardsList;
            } else {
                this.filteredCards = this.cardsList.filter(card => card.archetype === selectedArchetype);
            }

            console.log( `Questo è l'archetipo selezionato ${selectedArchetype}`);
        },
    },

    created(){
        this.getCards();
        this.getArchetypes();
    }
};
</script>

<template>
    <section class="card-selector">
        <MainCardSelector @archetype-selected="filterCardsByArchetype" :archetypeList="archetypeList"/>
    </section>
    <section class="row align-items-stretch justify-content-center pt-4 cards-wrapper">
        <div class="col-12 text-bg-dark p-2 mb-2 text-center cards-counter">
            <h4>
                {{ filteredCards.length }} cards has been found
            </h4>
        </div>
        <article v-for="card in filteredCards" :key="card.id" class="col-2 me-2 mb-3">
            <MainSingleCard :card="card"/>
        </article>
    </section>
</template>

<style scoped lang="scss">
@use "../styles/partials/variables" as *;
    
    .card-selector {
        max-width: 1200px;
        margin: 1rem auto;

        div {
            max-width: 12rem;
        }
    }

    .cards-wrapper {
        max-width: 1200px;
        background-color: white;
        margin: 0 auto;
    }
</style>