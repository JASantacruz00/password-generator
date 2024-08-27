<template>
  <div class="flex">
    <div class="flex flex-col w-min text-center align-middle justify-center">
      <h1 class="text-center justify-center font-bold align-middle items-center h-max">
        Password Generator.
      </h1>
      <p class="font-semibold">
        Create strong, secure passwords with ease. Customize your password settings and
        generate unbreakable codes in seconds.
      </p>
    </div>
    <PasswordGenerator />
  </div>
</template>

<script setup lang="ts">
import PasswordGenerator from "../components/PasswordGenerator.vue";
</script>

<style scoped></style>
