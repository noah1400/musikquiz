<template>
    <div class="difficulty-cell flex justify-center items-center border border-gray-300 rounded-lg shadow hover:shadow-lg cursor-pointer transition duration-300 ease-in-out p-4 text-lg font-medium hover:bg-blue-400 hover:text-white"
        @click="cellClicked" :class="{ 'crossed-out': isAnswered, 'bg-green-200': !isAnswered }">
        {{ difficulty }}
    </div>
</template>
  
<script>
export default {
    props: {
        isAnswered: Boolean,
        category: Object,
        difficulty: Number,
        question: Object // Contains question and answer
    },
    methods: {
        cellClicked() {
            if (!this.isAnswered) {
                this.$emit('cell-clicked', this.category, this.difficulty, this.question);
                console.log('Cell clicked and answered: ', this.category, this.difficulty, this.question);
            }
        }
    }
};
</script>
  
<style>
.crossed-out {
    text-decoration: line-through;
    opacity: 0.5;
    cursor: not-allowed;
}
</style>
  