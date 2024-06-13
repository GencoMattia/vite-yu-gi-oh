<script>
export default {
    data() {
        return {
        
        };
    },

    props: {
        archetypeList: {
            type: Array,
            required: true,
        }
    },

    methods: {
        emitSelectedArchetype(event) {
            this.$emit('archetype-selected', event.target.value); 
        }
    }
};
</script>

<template>
    <div class="form-floating">
        <select @change="emitSelectedArchetype" class="form-select" aria-label="Floating label select example" name="archetype-selector" id="archetype-selector">
            <option v-for="(archetype, index) in archetypeList" key="index" :value="archetype">
                {{ archetype }}
            </option>
            </select>
        <label for="archetype-selector">Choose an archetype:</label>
    </div>
</template>

<style scoped>

</style>