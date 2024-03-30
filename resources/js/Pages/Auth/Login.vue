<script setup>
import GuestLayout from "@/Layouts/GuestLayout.vue";
import { Head, Link, useForm } from "@inertiajs/vue3";
import { ref } from "vue";

defineProps({
  canResetPassword: {
    type: Boolean,
  },
  status: {
    type: String,
  },
});

const hidden = ref(true);

const form = useForm({
  email: "",
  password: "",
  remember: false,
});

const submit = () => {
  form.post(route("login"), {
    onFinish: () => form.reset("password"),
  });
};
</script>

<template>
  <GuestLayout>
    <Head title="Log in" />
    <v-card class="pa-5">

      <p class="text-center mb-5">Sign in to start your session</p>

      <p v-if="status" class="text-center mb-5">
        {{ status }}
      </p>

      <form @submit.prevent="submit">

        <v-text-field
          label="Email"
          v-model="form.email"
          :error-messages="form.errors.email"
          prepend-inner-icon="mdi-email"
          class="mb-3"
        />

        <v-text-field
          label="Password"
          v-model="form.password"
          :error-messages="form.errors.password"
          :type="hidden ? 'password' : 'text'"
          prepend-inner-icon="mdi-key"
          :append-inner-icon="hidden ? 'mdi-eye-off' : 'mdi-eye'"
          @click:append-inner="hidden = !hidden"
          class="mb-3"
        />

        <div class="d-flex">
          <v-checkbox-btn
            label="Remember"
            v-model="form.remember"
            class="pe-2"
          />
          <v-btn
            type="submit"
            color="black"
            :loading="form.processing"
            prepend-icon="mdi-login"
            >Log in</v-btn
          >
        </div>

      </form>
    </v-card>
  </GuestLayout>
</template>
