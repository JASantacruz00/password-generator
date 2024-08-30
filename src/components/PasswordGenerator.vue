<template>
  <div class="card shadow-md">
    <div class="max-h-min">
      <div class="flex flex-col p-7 justify-center">
        <InputRange
          v-model="passwordLength"
          :min="8"
          :max="32"
          :step="1"
          id="password-length"
          label="Password Length: "
          @update:modelValue="onChangeLengthValue"
        />
        <div class="options">
          <div class="grid grid-cols-2 gap-16">
            <div class="flex items-center justify-end space-x-2">
              <input v-model="options.numbers" type="checkbox" class="w-4 h-4 form-checkbox" />
              <label>Numbers</label>
            </div>
            <div class="flex items-center space-x-2">
              <input v-model="options.symbols" type="checkbox" class="w-4 h-4 form-checkbox" />
              <label>Symbols</label>
            </div>
          </div>
        </div>
      </div>
      <input
        type="button"
        value="Generate"
        class="bg-blue-700 border border-solid px-3 py-2 mb-3 border-white rounded cursor-pointer"
        @click="generatePassword"
      />
      <input
        v-model="password"
        class="w-full text-black border border-black p-2 rounded"
        type="text"
        readonly
      ></input>
      <PasswordStrength 
        :password="password"
        class='mt-5'
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, type Ref, onMounted } from "vue";
import { IOptions } from "../shared/types/types";
import PasswordStrength from "./PasswordStrength.vue";
import InputRange from '../shared/components/InputRange.vue'

const password: Ref<string> = ref("");
const passwordLength: Ref<number> = ref(16);
const rows: Ref<number> = ref(1);
const charset: Ref<string> = ref("abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ");
const numbers: Ref<string> = ref("0123456789");
const symbols: Ref<string> = ref("!@#$%^&*()_+-=[]{}|;:,.<>?");


const options: Ref<IOptions> = ref({
  numbers: false,
  symbols: false,
});

const onChangeLengthValue = () => {
  if (passwordLength.value < 8) {
    passwordLength.value = 8;
  }
  if (passwordLength.value > 32) {
    passwordLength.value = 32;
  }
}

const generatePassword = () => {
  password.value = ""
  charset.value = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";

  if (options.value.numbers) {
    charset.value += numbers.value;
  }
  if (options.value.symbols) {
    charset.value += symbols.value;
  }

  for (let i = 0; i < passwordLength.value; i++) {
    password.value += charset.value.charAt(Math.floor(Math.random() * charset.value.length));
  }
  rows.value = Math.ceil(passwordLength.value / 20);
}

onMounted(() => {
  generatePassword();
});
</script>

<style scoped>
.card {
  background-color: #efefef;
  border-radius: 10px;
  padding: 20px;
  margin: 20px;
  border: 1px solid black;
  height: 45%;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

label {
  color: black;
}
</style>
