<script lang="ts" setup>
import { ref } from "vue";
import { useRouter } from "vue-router";
const router = useRouter();

const email = ref("");
const password = ref("");
const confirmPassword = ref("");

function register() {
  router.push({ name: "login" });
}
</script>
<template>
  <v-container style="height: 100%">
    <v-row align="center" no-gutters style="height: 100%">
      <v-sheet width="300" class="mx-auto">
        <h1 class="mb-5 text-center">Register</h1>
        <v-form fast-fail @submit.prevent="register">
          <v-text-field v-model="email" label="Email"> </v-text-field>
          <v-text-field v-model="password" label="Password" type="password">
          </v-text-field>
          <v-text-field
            v-model="confirmPassword"
            label="Confirm password"
            type="password"
          >
          </v-text-field>
          <v-btn type="submit" block class="mt-2">Submit</v-btn>
        </v-form>
      </v-sheet>
    </v-row>
  </v-container>
</template>
