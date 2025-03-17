<script setup lang="ts">
import { ref, computed, onMounted } from 'vue';
import axios from 'axios';

const difficulties = {
    easy: { minLength: 50, maxLength: 100 },
    medium: { minLength: 100, maxLength: 200 },
    hard: { minLength: 200, maxLength: 300 }
};

const difficulty = ref<keyof typeof difficulties>('medium');
const text = ref('');
const userInput = ref('');
const startTime = ref<number | null>(null);
const endTime = ref<number | null>(null);
const isTestActive = ref(false);

const wpm = computed(() => {
    if (!startTime.value || !endTime.value) return 0;
    const timeInMinutes = (endTime.value - startTime.value) / 60000;
    const words = userInput.value.trim().split(/\s+/).length;
    return Math.round(words / timeInMinutes);
});

const accuracy = computed(() => {
    if (!text.value || !userInput.value) return 100;
    let correct = 0;
    const userInputChars = userInput.value.split('');
    const textChars = text.value.split('');

    userInputChars.forEach((char, i) => {
        if (char === textChars[i]) correct++;
    });

    return Math.round((correct / textChars.length) * 100);
});

async function fetchQuote() {
    const { minLength, maxLength } = difficulties[difficulty.value];
    try {
        const response = await axios.get('https://thequoteshub.com/api/');
        const quote = response.data.match(/Quote:\s*(.*?)\s*Author:/)[1];
        if (quote.length >= minLength && quote.length <= maxLength) {
            text.value = quote;
        } else {
            fetchQuote();
            return;
        }
        userInput.value = '';
        startTime.value = null;
        endTime.value = null;
        isTestActive.value = false;
    } catch (error) {
        console.error('Error fetching quote:', error);
        text.value = 'Error loading quote. Please try again.';
    }
}

function handleInput() {
    if (!startTime.value) {
        startTime.value = Date.now();
        isTestActive.value = true;
    }

    if (userInput.value.length >= text.value.length) {
        endTime.value = Date.now();
        isTestActive.value = false;
    }
}

onMounted(fetchQuote);
</script>

<template>
    <div class="min-h-screen bg-zinc-900 text-zinc-100 p-8 font-mono">
        <div class="max-w-4xl mx-auto">
            <h1 class="text-5xl font-bold mb-8 text-center tracking-tight">
                Type Master
            </h1>

            <div class="mb-6 flex justify-between items-center">
                <div class="space-x-4">
                    <button v-for="level in ['easy', 'medium', 'hard']" :key="level"
                        @click="difficulty = level as keyof typeof difficulties; fetchQuote()" :class="[
                            'px-6 py-3 border-2 transition-all duration-200 uppercase tracking-wider text-sm font-bold',
                            difficulty === level
                                ? 'bg-zinc-100 border-zinc-100 text-zinc-900'
                                : 'border-zinc-700 hover:border-zinc-500'
                        ]">
                        {{ level }}
                    </button>
                </div>

                <button @click="fetchQuote"
                    class="px-6 py-3 bg-zinc-800 hover:bg-zinc-700 transition-all duration-200 uppercase tracking-wider text-sm font-bold border-2 border-zinc-700 hover:border-zinc-600">
                    New Quote
                </button>
            </div>

            <div class="bg-zinc-800 p-8 mb-6 border-2 border-zinc-700 shadow-[0_0_15px_rgba(255,255,255,0.1)]">
                <p class="text-xl leading-relaxed font-light">{{ text }}</p>
            </div>

            <div class="relative">
                <textarea v-model="userInput" @input="handleInput"
                    :disabled="!isTestActive && userInput.length >= text.length"
                    class="w-full h-32 bg-zinc-800 text-zinc-100 p-6 resize-none border-2 border-zinc-700 focus:border-zinc-500 focus:outline-none transition-all duration-200 font-mono text-lg shadow-[0_0_15px_rgba(255,255,255,0.1)]"
                    :placeholder="isTestActive ? 'Keep typing...' : 'Start typing to begin the test...'"></textarea>
            </div>

            <div class="mt-6 grid grid-cols-2 gap-6">
                <div class="bg-zinc-800 p-6 border-2 border-zinc-700 shadow-[0_0_15px_rgba(255,255,255,0.1)]">
                    <p class="text-lg font-bold uppercase tracking-wider text-zinc-400">Speed</p>
                    <p class="text-4xl font-bold mt-2">{{ wpm }} <span class="text-2xl text-zinc-400">WPM</span></p>
                </div>
                <div class="bg-zinc-800 p-6 border-2 border-zinc-700 shadow-[0_0_15px_rgba(255,255,255,0.1)]">
                    <p class="text-lg font-bold uppercase tracking-wider text-zinc-400">Accuracy</p>
                    <p class="text-4xl font-bold mt-2">{{ accuracy }}<span class="text-2xl text-zinc-400">%</span></p>
                </div>
            </div>
        </div>
    </div>
</template>