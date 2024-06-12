<script>
export default {
    data() {
        return {
        
        };
    },

    props: {
        card: {
            type: Object,
            required: true,
        }
    }
};
</script>

<template>
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
</template>

<style scoped>

</style>