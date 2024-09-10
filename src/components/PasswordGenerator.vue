<template>
  <div class="card shadow-md">
    <div class="h-full">
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
              <input
                v-model="options.numbers"
                type="checkbox"
                class="w-4 h-4 form-checkbox"
              />
              <label class="text-black">Numbers</label>
            </div>
            <div class="flex items-center space-x-2">
              <input
                v-model="options.symbols"
                type="checkbox"
                class="w-4 h-4 form-checkbox"
              />
              <label class="text-black">Symbols</label>
            </div>
          </div>
        </div>
      </div>
      <div class="flex flex-col justify-center items-center">
        <input
          type="button"
          value="Generate"
          class="bg-blue-700 w-24 border border-solid px-3 py-2 mb-3 border-white rounded cursor-pointer"
          @click="generatePassword"
        />
        <div class="relative w-96">
          <input
            v-model="password"
            id="password"
            class="w-full text-black border border-black p-2 rounded"
            type="text"
            readonly
          />
          <button
            class="text-black absolute right-0 top-0 h-full px-3 group hover:scale-125"
            @click="onClickCopyToClipboard"
          >
            <i class="fa-regular fa-clipboard"></i>
            <div
              class="absolute bottom-full hidden group-hover:block w-max text-white text-xs rounded py-2 px-3"
              :class="
                passwordCopiedText == 'Copy to clipboard'
                  ? 'bg-gray-500'
                  : 'bg-green-500'
              "
            >
              {{ passwordCopiedText }}
            </div>
          </button>
        </div>
      </div>
      <PasswordStrength :password="password" class="mt-5 pb-8" />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, type Ref, onMounted } from "vue";
import { IOptions } from "../shared/types/types";
import PasswordStrength from "./PasswordStrength.vue";
import InputRange from "../shared/components/InputRange.vue";

const password: Ref<string> = ref("");
const passwordLength: Ref<number> = ref(16);
const rows: Ref<number> = ref(1);
const charset: Ref<string> = ref(
  "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ"
);
const numbers: Ref<string> = ref("0123456789");
const symbols: Ref<string> = ref("!@#$%^&*()_+-=[]{}|;:,.<>?");

const passwordCopiedText: Ref<string> = ref("Copy to clipboard");

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
};

const generatePassword = () => {
  password.value = "";
  passwordCopiedText.value = "Copy to clipboard";
  charset.value = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";

  if (options.value.numbers) {
    charset.value += numbers.value;
  }
  if (options.value.symbols) {
    charset.value += symbols.value;
  }

  for (let i = 0; i < passwordLength.value; i++) {
    password.value += charset.value.charAt(
      Math.floor(Math.random() * charset.value.length)
    );
  }
  rows.value = Math.ceil(passwordLength.value / 20);
};

const onClickCopyToClipboard = () => {
  navigator.clipboard.writeText(password.value);
  passwordCopiedText.value = "Password copied to clipboard!";
};

onMounted(() => {
  generatePassword();
});
</script>
