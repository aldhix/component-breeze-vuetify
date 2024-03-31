<script setup>
import GuestLayout from "@/Layouts/GuestLayout.vue";
import { Head, Link, useForm, router } from "@inertiajs/vue3";
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

    <v-card class="pa-5">
      <p class="text-center mb-5">Register a new membership</p>

      <form @submit.prevent="submit">
        <v-text-field
          label="Name"
          v-model="form.name"
          :error-messages="form.errors.name"
          prepend-inner-icon="mdi-account"
          class="mb-2"
          required
          autofocus
          autocomplete="name"
        />

        <v-text-field
          label="Email"
          v-model="form.email"
          :error-messages="form.errors.email"
          prepend-inner-icon="mdi-email"
          class="mb-2"
          required
          autocomplete="username"
        />

        <v-text-field
          label="Password"
          v-model="form.password"
          :error-messages="form.errors.password"
          :type="hidden ? 'password' : 'text'"
          prepend-inner-icon="mdi-key"
          :append-inner-icon="hidden ? 'mdi-eye-off' : 'mdi-eye'"
          @click:append-inner="hidden = !hidden"
          class="mb-2"
          autocomplete="current-password"
        />

        <v-text-field
          label="Confirmation Password"
          v-model="form.password_confirmation"
          :error-messages="form.errors.password_confirmation"
          :type="hidden ? 'password' : 'text'"
          prepend-inner-icon="mdi-key"
          :append-inner-icon="hidden ? 'mdi-eye-off' : 'mdi-eye'"
          @click:append-inner="hidden = !hidden"
          class="mb-2"
          autocomplete="current-password"
        />

        <div class="d-flex">
          <v-btn
            class="text-none ms-auto me-3"
            color="blue"
            variant="text"
            :href="route('login')"
            @click.prevent="router.get(route('login'))"
            >Already registered?
          </v-btn>

          <v-btn
            type="submit"
            color="black"
            :loading="form.processing"
            prepend-icon="mdi-login"
            >Register</v-btn
          >
        </div>
      </form>
    </v-card>
  </GuestLayout>
</template>
