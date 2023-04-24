<script lang="ts" setup>
import { emailRules, passwordRules } from "@/types/rules";
import { ref } from "vue";
import { useRouter } from "vue-router";
import type { VForm } from "vuetify/lib/components/index";

const email = ref("");
const password = ref("");
const router = useRouter();
const loginForm = ref<VForm | null>(null);

async function login() {
  const validated = await loginForm.value?.validate();

  if (validated?.valid) {
    router.push({ name: "chat" });
  }
}
</script>

<template>
  <v-container style="height: 100%">
    <v-row align="center" no-gutters style="height: 100%">
      <v-sheet width="300" class="mx-auto">
        <h1 class="mb-5 text-center">Login</h1>
        <v-form fast-fail @submit.prevent="login" ref="loginForm">
          <v-text-field :rules="emailRules" v-model="email" label="Email">
          </v-text-field>
          <v-text-field
            :rules="passwordRules"
            v-model="password"
            label="Password"
            type="password"
          >
          </v-text-field>
          <v-btn type="submit" block class="mt-2">Submit</v-btn>
        </v-form>
      </v-sheet>
    </v-row>
  </v-container>
</template>
