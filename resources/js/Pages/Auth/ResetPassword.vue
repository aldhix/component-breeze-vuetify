<script setup>
import GuestLayout from "@/Layouts/GuestLayout.vue";
import ApplicationLogo from "@/Components/ApplicationLogo.vue";
import { Head, useForm } from "@inertiajs/vue3";
import { ref } from "vue";

const hidden = ref(true);

const props = defineProps({
  email: {
    type: String,
    required: true,
  },
  token: {
    type: String,
    required: true,
  },
});

const form = useForm({
  token: props.token,
  email: props.email,
  password: "",
  password_confirmation: "",
});

const submit = () => {
  form.post(route("password.store"), {
    onFinish: () => form.reset("password", "password_confirmation"),
  });
};
</script>

<template>
  <GuestLayout>

    <Head title="Reset Password" />
    <v-container class="layout-login">

      <div class="text-center mb-5">
        <img src="/images/logo.png" alt="Logo" width="85">
      </div>

      <v-card class="pa-5">
        <p class="mb-5">
          You are only one step a way from your new password, recover your password now.
        </p>

        <form @submit.prevent="submit">
          <v-text-field label="Email" v-model="form.email" :error-messages="form.errors.email"
            prepend-inner-icon="mdi-email" class="mb-2" required autofocus autocomplete="username" />

          <v-text-field label="Password" v-model="form.password" :error-messages="form.errors.password"
            :type="hidden ? 'password' : 'text'" prepend-inner-icon="mdi-key"
            :append-inner-icon="hidden ? 'mdi-eye-off' : 'mdi-eye'" @click:append-inner="hidden = !hidden" class="mb-2"
            autocomplete="new-password" />

          <v-text-field label="Confirmation Password" v-model="form.password_confirmation"
            :error-messages="form.errors.password_confirmation" :type="hidden ? 'password' : 'text'"
            prepend-inner-icon="mdi-key" class="mb-2" />

          <div class="d-flex">
            <v-btn class="ms-auto" type="submit" color="black" :loading="form.processing">Reset Password</v-btn>
          </div>
        </form>
      </v-card>
    </v-container>

  </GuestLayout>
</template>
