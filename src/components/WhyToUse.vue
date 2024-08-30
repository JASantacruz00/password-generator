<template>
  <div class="flex flex-col max-w-6xl mx-auto p-6">
    <h1 class="text-center font-bold text-6xl mb-5">Why to use RandPass?</h1>
    <p class="font-semibold text-xl mb-4">
      A random password generator is essential for robust online security
      because:
    </p>
    <ul
      class="list-disc list-outside space-y-4 marker:text-primary marker:font-semibold text-xl pl-6"
    >
      <li
        v-for="(reason, index) in reasons"
        :key="index"
        class="font-semibold text-xl pl-2 text-start"
      >
        <span>{{ reason }}</span>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

const reasons = ref([
  "Strength: It creates complex passwords with a mix of uppercase and lowercase letters, numbers, and symbols, making them significantly harder to crack through brute-force attacks.",
  "Uniqueness: It ensures each password is unique, preventing a single breach from compromising multiple accounts.",
  "Convenience: It eliminates the need to remember complex passwords, as they can be stored securely in a password manager.",
  "Protection against phishing: Strong, unique passwords reduce the effectiveness of phishing attempts, where attackers try to trick users into revealing their login credentials.",
  "Compliance: Many organizations and industries require strong password practices to meet security standards and regulations.",
]);
</script>
