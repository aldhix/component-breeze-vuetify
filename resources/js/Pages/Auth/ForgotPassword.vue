<script setup>
import GuestLayout from "@/Layouts/GuestLayout.vue";
import ApplicationLogo from "@/Components/ApplicationLogo.vue";
import { Head, useForm } from "@inertiajs/vue3";

defineProps({
  status: {
    type: String,
  },
});

const form = useForm({
  email: "",
});

const submit = () => {
  form.post(route("password.email"));
};
</script>

<template>
  <GuestLayout>

    <Head title="Forgot Password" />

    <v-container class="layout-login">

      <div class="text-center mb-5">
        <img src="/images/logo.png" alt="Logo" width="85">
      </div>

      <v-card class="pa-5">
        <p class="mb-5">
          Forgot your password? No problem. Just let us know your email address
          and we will email you a password reset link that will allow you to
          choose a new one.
        </p>

        <p class="mb-5 text-green text-center" v-if="status">
          {{ status }}
        </p>

        <form @submit.prevent="submit">
          <v-text-field label="Email" v-model="form.email" :error-messages="form.errors.email"
            prepend-inner-icon="mdi-email" class="mb-2" required autofocus autocomplete="username" />

          <div class="d-flex">
            <v-btn class="ms-auto" type="submit" color="black" :loading="form.processing">Email Password Reset
              Link</v-btn>
          </div>
        </form>
      </v-card>
    </v-container>


  </GuestLayout>
</template>
