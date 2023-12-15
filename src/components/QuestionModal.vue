<template>
    <div v-if="show" class="fixed inset-0 bg-gray-800 bg-opacity-50 flex justify-center items-center px-4 py-6">
        <div class="bg-white w-full max-w-lg mx-auto rounded-lg shadow-lg overflow-hidden p-6">
            <h2 class="text-2xl font-semibold text-gray-800 mb-6">{{ question }}</h2>

            <!-- Answer Box (Visible or Invisible) -->
            <div class="mb-4">
                <div v-if="answerRevealed" class="bg-green-600 bg-opacity-75 text-white p-4 rounded">
                    <span class="font-medium">Answer:</span> {{ answer }}
                </div>

                <div v-else class="invisible p-4">
                    Placeholder for spacing
                </div>
            </div>

            <!-- Buttons -->
            <div class="flex justify-between">
                <!-- Reveal Answer Button -->
                <button v-if="!answerRevealed"
                    class="bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 px-4 rounded transition duration-200"
                    @click="revealAnswer">
                    Reveal Answer
                </button>
                <div v-else></div> <!-- Placeholder to keep layout -->

                <!-- Close Button -->
                <button
                    class="bg-red-600 hover:bg-red-700 text-white font-semibold py-2 px-4 rounded transition duration-200"
                    @click="closeModal">
                    Close
                </button>
            </div>
        </div>
    </div>
</template>
  
  
  
  
  
  
<script>
export default {
    props: {
        show: Boolean,
        question: String,
        answer: String
    },
    data() {
        return {
            answerRevealed: false
        };
    },
    methods: {
        closeModal() {
            this.answerRevealed = false; // Reset answer reveal state
            this.$emit('close');
        },
        revealAnswer() {
            this.answerRevealed = true;
        }
    }
};
</script>
  