<script setup>
import GuestLayout from "@/Layouts/GuestLayout.vue";
import { Head, Link } from "@inertiajs/vue3";
import { router } from "@inertiajs/vue3";

defineProps({
  canLogin: {
    type: Boolean,
  },
  canRegister: {
    type: Boolean,
  },
  laravelVersion: {
    type: String,
    required: true,
  },
  phpVersion: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <Head title="Welcome" />
  <GuestLayout>
    <v-card class="pa-5">
      <h3 class="mb-5">The PHP Framework for Web Artisans</h3>
      <p class="mb-5">
        Laravel is a web application framework with expressive, elegant syntax. We’ve already laid the foundation — freeing you to create without sweating the small things.
      </p>

      <p class="mb-5" v-if="canLogin">
        <v-btn
          v-if="$page.props.auth.user"
          color="black"
          :href="route('dashboard')"
          @click.prevent="router.get(route('dashboard'))"
          class="me-3"
        >
          Dashboard
        </v-btn>

        <template v-else>
          <v-btn
            color="black"
            :href="route('login')"
            @click.prevent="router.get(route('login'))"
            class="me-3"
          >
            Log In
          </v-btn>

          <v-btn
            color="black"
            :href="route('register')"
            @click.prevent="router.get(route('register'))"
            v-if="canRegister"
          >
            Register
          </v-btn>
        </template>
      </p>

      <p class="text-caption text-grey">Laravel v{{ laravelVersion }} (PHP v{{ phpVersion }})</p>
    </v-card>
  </GuestLayout>
</template>