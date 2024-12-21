<script setup>
import GuestLayout from "@/Layouts/GuestLayout.vue";
import { Head, useForm } from "@inertiajs/vue3";
import { ref } from "vue";

const hidden = ref(true)

const form = useForm({
  password: "",
});

const submit = () => {
  form.post(route("password.confirm"), {
    onFinish: () => form.reset(),
  });
};
</script>

<template>
  <GuestLayout>

    <Head title="Confirm Password" />
    <v-container class="layout-login">

      <div class="text-center mb-5">
        <img src="/images/logo.png" alt="Logo" width="85">
      </div>

      <v-card class="pa-5">
        <p class="mb-5">
          This is a secure area of the application. Please confirm your password before continuing.
        </p>

        <form @submit.prevent="submit">

          <v-text-field label="Password" v-model="form.password" :error-messages="form.errors.password"
            :type="hidden ? 'password' : 'text'" prepend-inner-icon="mdi-key"
            :append-inner-icon="hidden ? 'mdi-eye-off' : 'mdi-eye'" @click:append-inner="hidden = !hidden" class="mb-2"
            required autofocus autocomplete="current-password" />

          <div class="d-flex">
            <v-btn class="ms-auto" type="submit" color="black" :loading="form.processing">Confirm</v-btn>
          </div>
        </form>
      </v-card>
    </v-container>

  </GuestLayout>
</template>
