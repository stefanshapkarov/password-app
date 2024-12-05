<script setup>
import { computed } from 'vue';
import PasswordScore from './PasswordScore.vue';

const { password } = defineProps(['password']);

const hasAtLeast8Characters = computed(() => password.length >= 8);
const hasLowercaseLetter = computed(() => /[a-z]/.test(password));
const hasUppercaseLetter = computed(() => /[A-Z]/.test(password));
const hasDigit = computed(() => /\d/.test(password));
const hasSpecialCharacter = computed(() => /[!@#$%^&*]/.test(password));

const totalRequirementsFulfilled = computed(() => {
    let count = 0;
    if (hasAtLeast8Characters.value) count++;
    if (hasLowercaseLetter.value) count++;
    if (hasUppercaseLetter.value) count++;
    if (hasDigit.value) count++;
    if (hasSpecialCharacter.value) count++;
    console.log(count);
    return count;
});
</script>

<template>
    <div id="requirements-container">
        <h4>Password requirements:</h4>
        <div class="requirement">
            <p>
                <span v-if="hasAtLeast8Characters" style="color: green">&#10004;</span>
                <span v-else style="color: red">&#10006;</span>
                Password should be at least 8 characters long
            </p>
        </div>
        <div class="requirement">
            <p>
                <span v-if="hasLowercaseLetter" style="color: green">&#10004;</span>
                <span v-else style="color: red">&#10006;</span>
                1 lowercase letter (a-z)
            </p>
        </div>
        <div class="requirement">
            <p>
                <span v-if="hasUppercaseLetter" style="color: green">&#10004;</span>
                <span v-else style="color: red">&#10006;</span>
                1 uppercase letter (A-Z)
            </p>
        </div>
        <div class="requirement">
            <p>
                <span v-if="hasDigit" style="color: green">&#10004;</span>
                <span v-else style="color: red">&#10006;</span>
                1 digit (0-9)
            </p>
        </div>
        <div class="requirement">
            <p>
                <span v-if="hasSpecialCharacter" style="color: green">&#10004;</span>
                <span v-else style="color: red">&#10006;</span>
                1 special character (e.g., !, @, #, $, etc.)
            </p>
        </div>
    </div>
    <PasswordScore :password="password" :fulfilledRequirements="totalRequirementsFulfilled" />
</template>

<style scoped>
#requirements-container {
    display: flex;
    flex-direction: column;
}

.requirement {
    margin-bottom: 8px;
}

.requirement p {
    display: flex;
    align-items: center;
    margin: 0;
}

.requirement span {
    margin-right: 8px;
}
</style>
