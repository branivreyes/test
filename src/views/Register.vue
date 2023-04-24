<script lang="ts" setup>
import { emailRules, passwordRules } from "@/types/rules";
import { ref } from "vue";
import { useRouter } from "vue-router";
import type { VForm } from "vuetify/lib/components/index";
const router = useRouter();

const email = ref("");
const password = ref("");
const confirmPassword = ref("");
const registerForm = ref<VForm | null>(null);
const confirmPasswordRules = [
  ...passwordRules,
  (v: string) => v === password.value || "Passwords don't match",
];

async function register() {
  const validated = await registerForm.value?.validate();

  if (validated?.valid) {
    router.push({ name: "login" });
  }
}
</script>
<template>
  <v-container style="height: 100%">
    <v-row align="center" no-gutters style="height: 100%">
      <v-sheet width="300" class="mx-auto">
        <h1 class="mb-5 text-center">Register</h1>
        <v-form fast-fail @submit.prevent="register" ref="registerForm">
          <v-text-field v-model="email" :rules="emailRules" label="Email">
          </v-text-field>
          <v-text-field
            v-model="password"
            :rules="passwordRules"
            label="Password"
            type="password"
          >
          </v-text-field>
          <v-text-field
            v-model="confirmPassword"
            label="Confirm password"
            type="password"
            :rules="confirmPasswordRules"
          >
          </v-text-field>
          <v-btn type="submit" block class="mt-2">Submit</v-btn>
        </v-form>
      </v-sheet>
    </v-row>
  </v-container>
</template>
