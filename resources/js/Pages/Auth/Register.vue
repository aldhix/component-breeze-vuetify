<script setup>
import GuestLayout from "@/Layouts/GuestLayout.vue";
import ApplicationLogo from "@/Components/ApplicationLogo.vue";
import { Head, useForm, router } from "@inertiajs/vue3";
import { ref } from "vue";

const hidden = ref(true);

const form = useForm({
  name: "",
  email: "",
  password: "",
  password_confirmation: "",
});

const submit = () => {
  form.post(route("register"), {
    onFinish: () => form.reset("password", "password_confirmation"),
  });
};
</script>

<template>
  <GuestLayout>

    <Head title="Register" />
    <v-container class="layout-login">

      <div class="text-center mb-5">
        <img src="/images/logo.png" alt="Logo" width="85">
      </div>
      

      <v-card class="pa-5">
        <form @submit.prevent="submit">
          <v-text-field label="Name" v-model="form.name" :error-messages="form.errors.name"
            prepend-inner-icon="mdi-account" class="mb-2" required autofocus autocomplete="name" />

          <v-text-field label="Email" v-model="form.email" :error-messages="form.errors.email"
            prepend-inner-icon="mdi-email" class="mb-2" required autocomplete="username" />

          <v-text-field label="Password" v-model="form.password" :error-messages="form.errors.password"
            :type="hidden ? 'password' : 'text'" prepend-inner-icon="mdi-key"
            :append-inner-icon="hidden ? 'mdi-eye-off' : 'mdi-eye'" @click:append-inner="hidden = !hidden" class="mb-2"
            autocomplete="current-password" />

          <v-text-field label="Confirmation Password" v-model="form.password_confirmation"
            :error-messages="form.errors.password_confirmation" :type="hidden ? 'password' : 'text'"
            prepend-inner-icon="mdi-key" class="mb-2" />

          <div class="d-flex">
            <v-btn class="text-none ms-auto me-3" color="blue" variant="text" :href="route('login')"
              @click.prevent="router.get(route('login'))">Already registered?
            </v-btn>

            <v-btn type="submit" color="black" :loading="form.processing">Register</v-btn>
          </div>
        </form>
      </v-card>
    </v-container>

  </GuestLayout>
</template>
