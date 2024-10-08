<template>
  <div class="w-full max-w-md mx-auto">
    <label :for="id" class="text-xl font-semibold text-gray-700">
      {{ label }} {{ modelValue }}
    </label>
    <div class="flex items-center space-x-4">
      <div class="relative flex-grow pt-1">
        <input
          :id="id"
          type="range"
          :min="min"
          :max="max"
          :step="step"
          :value="modelValue"
          @input="updateValue"
          class="w-full h-2 bg-gray-300 rounded-lg appearance-none cursor-pointer"
        />
        <div
          class="absolute left-0 top-3.5 h-2 bg-blue-500 rounded-l-lg pointer-events-none border-right slider-track"
          :style="{ width: percentage }"
        ></div>
      </div>
    </div>
    <div class="flex justify-between text-xs text-gray-500">
      <span>{{ min }}</span>
      <span>{{ max }}</span>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from "vue";

const props = defineProps({
  modelValue: {
    type: Number,
    required: true,
  },
  min: {
    type: Number,
    default: 0,
  },
  max: {
    type: Number,
    default: 100,
  },
  step: {
    type: Number,
    default: 1,
  },
  label: {
    type: String,
    default: "Label",
  },
  id: {
    type: String,
    default: "range-input",
  },
});

const emit = defineEmits(["update:modelValue"]);

const thumbWidth = 20; // Ancho del thumb en píxeles
const trackWidth = 100; // Asumiendo que el track ocupa el 100% del ancho

const percentage = computed(() => {
  const rawPercentage =
    ((props.modelValue - props.min) / (props.max - props.min)) * 100;
  const thumbOffset = thumbWidth / 2;

  const correctedPercentage =
    (rawPercentage * (trackWidth - thumbOffset)) / trackWidth + thumbOffset;

  // return `calc(${correctedPercentage}% - ${thumbWidth}px)` ;
  return `calc(${rawPercentage}% - ${
    (rawPercentage / 100) * thumbWidth
  }px + 1px)`;
});

const updateValue = (event) => {
  const newValue = Number(event.target.value);
  emit("update:modelValue", newValue);
};
</script>

<style scoped>
input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 20px;
  height: 20px;
  /*background: #3b82f6; /* Tailwind blue-500 */
  background: white; /* Tailwind blue-500 */
  cursor: pointer;
  border-radius: 50%;
  border: 2px solid #3b82f6;
  /* border: 2px solid white; */
  box-shadow: 0 0 2px rgba(0, 0, 0, 0.2);
}

input[type="range"]::-moz-range-thumb {
  width: 20px;
  height: 20px;
  background: #3b82f6; /* Tailwind blue-500 */
  cursor: pointer;
  border-radius: 50%;
  border: 2px solid white;
  box-shadow: 0 0 2px rgba(0, 0, 0, 0.2);
}
</style>
