<template>
  <div class="grid grid-flow-col grid-cols-12 h-[90vh] w-screen">
    <div class="col-span-6 flex flex-col justify-center pl-64 mb-36">
      <h1 class="text-center font-bold text-8xl mb-12">Password Generator.</h1>
      <h2 class="font-semibold text-xl">
        Create strong, secure passwords with ease. Customize your password
        settings and generate unbreakable codes in seconds.
      </h2>
    </div>
    <div class="col-span-6 flex flex-col justify-center pr-64">
      <PasswordGenerator />
    </div>
  </div>
  </div>
</template>

<script setup lang="ts">
import PasswordGenerator from "../components/PasswordGenerator.vue";
</script>

<style scoped></style>
