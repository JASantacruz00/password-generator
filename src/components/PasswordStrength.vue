<template>
  <div class="w-full min-w-96 space-y-2">
    <div class="flex justify-between items-center">
      <span class="text-sm font-medium text-gray-700">Password Strength:</span>
      <span class="text-sm font-medium" :class="strengthTextColor">{{
        strengthLabel
      }}</span>
    </div>
    <div class="w-full bg-gray-200 rounded-full h-2.5">
      <div
        class="h-2.5 rounded-full transition-all duration-300 ease-in-out"
        :class="strengthBarColor"
        :style="{ width: `${strengthPercentage}%` }"
      ></div>
    </div>
  </div>
</template>

<script setup>
import { computed } from "vue";

const props = defineProps({
  password: {
    type: String,
    required: true,
  },
});

const calculatePasswordStrength = (password) => {
  let strength = 0;
  if (password.length >= 8) strength++;
  if (password.length >= 12) strength++;
  if (/[A-Z]/.test(password)) strength++;
  if (/[a-z]/.test(password)) strength++;
  if (/[0-9]/.test(password)) strength++;
  if (/[^A-Za-z0-9]/.test(password)) strength++;
  return strength;
};

const strength = computed(() => calculatePasswordStrength(props.password));

const strengthPercentage = computed(() => (strength.value / 6) * 100);

const strengthLabel = computed(() => {
  if (strength.value <= 2) return "Weak";
  if (strength.value <= 4) return "Moderate";
  return "Strong";
});

const strengthBarColor = computed(() => {
  if (strength.value <= 2) return "bg-red-500";
  if (strength.value <= 4) return "bg-yellow-500";
  return "bg-green-500";
});

const strengthTextColor = computed(() => {
  if (strength.value <= 2) return "text-red-500";
  if (strength.value <= 4) return "text-yellow-500";
  return "text-green-500";
});
</script>
