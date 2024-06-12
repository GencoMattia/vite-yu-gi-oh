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
        <section class="cards-wrapper">
            <article v-for="card in cardsList" :key="card.id">
                <div class="card" style="width: 18rem;">
                    <img :src="card.card_images.image_url" class="card-img-top" alt="...">
                    <div class="card-body">
                        <p class="card-text">
                            {{ card.desc }}
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
    }
</style>