<script setup>
import UserInput from './components/UserInput.vue';
</script>

<template>
  <div id="header">
    <div id="header-content">
      <h1>Password App</h1>
      <h4>by Stefan Shapkarov</h4>
    </div>
  </div>
  
  <div id="user-input">
    <UserInput />
  </div>
</template>

<style scoped>
#header {
  display: flex;
  justify-content: center;
}

#header-content {
  border-radius: 10px;
  padding-inline: 100px;
  text-align: center;
}

#user-input {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 100px;
}
</style>