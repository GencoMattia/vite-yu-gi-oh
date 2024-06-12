<script>
import axios from 'axios';

export default {
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
    <main>
        <section class="row cards-wrapper align-items-stretch">
            <article v-for="card in cardsList" :key="card.id" class="col-2 me-2">
                <div class="card" style="width: 100%; height: 100%;">
                    <img :src="card.card_images[0].image_url" :alt="card.name" class="card-img-top">
                    <div class="card-body p-2">
                        <h2 class="card-name text-center fs-6 fw-bold">
                            {{ card.name }}
                        </h2>
                        <p class="card-archetype text-center">
                            {{ card.archetype }}
                        </p>
                    </div>
                </div>
            </article>
        </section>
    </main>
</template>

<style scoped lang="scss">
@use "../styles/partials/variables" as *;

    main {
        background-color: $appOrange;
        height: calc(100vh - 100px);
        overflow: auto;
    }

    img {
        max-width: 100%;
        height: auto;
    }
</style>