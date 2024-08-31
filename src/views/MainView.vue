<template>
  <div class="grid grid-flow-col grid-cols-12 h-[90vh] w-screen">
    <div class="col-span-6 flex flex-col mt-36 pl-64 mb-24">
      <h1 class="text-center font-bold text-8xl mb-12">Password Generator.</h1>
      <h2 class="w-full text-center font-semibold text-xl px-28 align-middle">
        Create strong, secure passwords with ease. Customize your password
        settings and generate unbreakable codes in seconds.
      </h2>
    </div>
    <div class="col-span-6 flex flex-col mt-36 pr-64">
      <PasswordGenerator />
    </div>
  </div>
  <div className="h-px bg-gray-200 -mt-10" />
  <div class="flex w-full text-center align-middle justify-center">
    <WhyToUse />
  </div>
</template>

<script setup lang="ts">
import PasswordGenerator from "../components/PasswordGenerator.vue";
import WhyToUse from "../components/WhyToUse.vue";
</script>

<style scoped></style>
