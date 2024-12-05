<script setup>
import { ref, computed } from 'vue';
import { CompareTwoStrings } from '../Utils/CompareTwoStrings';
import PasswordRequirements from './PasswordRequirements.vue';

const commonPasswords = ['123456', 'password', 'admin', '12345678', 'qwerty', '111111', '123123', '1q2w3e4r', 'qwerty123', '000000'];

const password = ref('');
const username = ref('');

const isCommonPassword = computed(() => commonPasswords.includes(password.value.toLowerCase()));
const doesUsernameContainPassword = computed(() => {
    if (username.value !== '') {
        return CompareTwoStrings(username.value, password.value);
    }
    return false;
});
</script>

<template>
    <div id="input-container">
        <form>
            <label for="username">Username</label>
            <input type="text" placeholder="Enter username" v-model="username" id="username" />
            <label for="password">Password</label>
            <div id="password-container">
                <input type="password" placeholder="Enter password" v-model="password" id="password"
                    @input="$emit('update:password', $event.target.value)" />
                <div class="warning-container">
                    <p v-if="isCommonPassword" class="warning">Password is common, please choose a different one</p>
                    <p v-if="doesUsernameContainPassword" class="warning">Username shouldn't be part of the password</p>
                </div>
            </div>
            <button type="submit">Register</button>
        </form>
        <PasswordRequirements :password="password" />
    </div>
</template>

<style scoped>
#input-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
    border: 1px solid grey;
    border-radius: 10px;
    padding: 30px;
}

form {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
    border: 1px solid grey;
    border-radius: 10px;
    width: 400px;
    padding: 20px;
}

button {
    border-radius: 10px;
    padding-inline: 20px;
    padding-block: 5px;
}

input {
    border-radius: 10px;
    padding: 5px;
}

#password-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    position: relative;
}

.warning-container {
    min-height: 24px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 4px;
}

#password {
    margin-bottom: 10px;
}

.warning {
    font-size: 12px;
    color: yellow;
    margin: 0;
}
</style>