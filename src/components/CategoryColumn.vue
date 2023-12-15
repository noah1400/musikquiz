<template>
    <div class="flex flex-col items-center bg-gray-200 p-4 rounded-lg">
        <div class="category-cell font-bold text-xl mb-4 bg-blue-500 text-white p-2 rounded">
            {{ category.name }}
        </div>
        <div class="difficulty-cells space-y-2">
            <difficulty-cell v-for="difficulty in difficulties" :key="category.id + '-' + difficulty" :category="category"
                :difficulty="difficulty" :question="category.questions[difficulty]"
                :is-answered="category.questions[difficulty].isAnswered" @click.native="cellClicked(difficulty)"
                class="h-12 flex items-center justify-center border rounded text-center cursor-pointer hover:bg-gray-200 mb-2" />
        </div>
    </div>
</template>
  
<script>
import DifficultyCell from './DifficultyCell.vue';

export default {
    components: {
        DifficultyCell
    },
    props: {
        category: Object,
        difficulties: Array
    },
    methods: {
        cellClicked(difficulty) {
            this.$emit('cell-clicked', this.category, difficulty);
        }
    }
};
</script>
  
<style>
/* Tailwind CSS styling */
</style>
  