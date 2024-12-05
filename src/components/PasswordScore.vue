<script setup>
import zxcvbn from 'zxcvbn';
import { computed } from 'vue';

const { password, fulfilledRequirements } = defineProps(['password', 'fulfilledRequirements']);

const passwordStrength = computed(() => {
    let score = '';
    let strength = 'Weak';

    if (fulfilledRequirements === 5) {
        const zxcvbnResult = zxcvbn(password);
        if (zxcvbnResult.score === 4) {
            score = 10;
            strength = 'Strong';
        } else if (zxcvbnResult.score === 1) {
            score = 1;
            strength = 'Weak';
        } else if (zxcvbnResult.score < 5 && zxcvbnResult.score > 2) {
            score = fulfilledRequirements + zxcvbnResult.score;
            strength = 'Strong';
        } else if (zxcvbnResult.score < 3) {
            score = fulfilledRequirements + zxcvbnResult.score;
            strength = 'Medium';
        }
    } else {
        score = fulfilledRequirements;
        strength = 'Weak';
    }

    return { score, strength };
});
</script>

<template>
    <div id="score-container">
        <p>Password strength: <span :class="passwordStrength.strength === 'Weak' ? 'red' : passwordStrength.strength === 'Medium' ? 'yellow' : 'green'">{{ passwordStrength.strength }}</span></p>
        <p>Password score: <span :class="passwordStrength.strength === 'Weak' ? 'red' : passwordStrength.strength === 'Medium' ? 'yellow' : 'green'">{{ passwordStrength.score }}/10</span></p>
    </div>
</template>

<style scoped>
#score-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    border-top: 1px solid grey;
    border-bottom: 1px solid grey;
    padding: 10px;
    margin-top: 30px;
}

.red {
    color: red;
}

.green {
    color: green;
}

.yellow {
    color: yellow;
}
</style>