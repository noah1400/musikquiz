<template>
    <div class="flex justify-center p-6 bg-white rounded-lg shadow-xl">
        <div class="flex flex-row gap-6">
            <category-column v-for="category in categories" :key="category.id" :category="category"
                :difficulties="difficulties" @cell-clicked="handleCellClicked" />
        </div>
    </div>
</template>
  
<script>
import CategoryColumn from './CategoryColumn.vue';

export default {
    components: {
        CategoryColumn
    },
    props: {
        categories: Array,
        difficulties: Array
    },
    methods: {
        handleCellClicked(category, difficulty) {
            // Handle the logic when a cell is clicked
            console.log('Cell clicked:', category, difficulty);
            this.$emit('cell-clicked', category, difficulty);
        }
    }
};
</script>
  