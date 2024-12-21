<script setup>
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
  <v-app class="bg-transparent">
    <v-app-bar :title="$appName" app>
      <v-spacer></v-spacer>
      <template v-if="canLogin">
        <v-btn v-if="$page.props.auth.user" :href="route('dashboard')" @click.prevent="router.get(route('dashboard'))">
          Dashboard
        </v-btn>
        <template v-else>
          <v-btn :href="route('login')" @click.prevent="router.get(route('login'))">
            Login
          </v-btn>
          <v-btn v-if="canRegister" :href="route('register')" @click.prevent="router.get(route('register'))">
            Register
          </v-btn>
        </template>
      </template>
    </v-app-bar>
    <v-main class="d-flex fill-height align-center">
      <v-container class="bg-transparent">
        <v-row>
          <v-col lg="6" offset-lg="3">
            <div class="text-center mb-5">
              <img src="/images/logo.png" alt="Logo" width="85">
            </div>
            <v-row align="stretch">
              <v-col cols="12" md="6">
                <v-card append-icon="mdi-arrow-right-bold" href="https://laravel.com/" target="_blank"
                  class="fill-height" title="Laravel" subtitle="The PHP Framework for Web Artisans"
                  text="Laravel is a web application framework with expressive, elegant syntax. We’ve already laid the foundation — freeing you to create without sweating the small things.">
                </v-card>
              </v-col>
              <v-col cols="12" md="6">
                <v-card append-icon="mdi-arrow-right-bold" href="https://vuejs.org/" target="_blank"
                  class="fill-height" title="Vue" subtitle="The Progressive JavaScript Framework"
                  text="An approachable, performant and versatile framework for building web user interfaces.">
                </v-card>
              </v-col>
              <v-col cols="12" md="6">
                <v-card append-icon="mdi-arrow-right-bold" href="https://vuetifyjs.com/" target="_blank"
                  class="fill-height" title="Vuefity" subtitle="Vue Component Framework"
                  text="Vuetify is a no design skills required Open Source UI Library with beautifully handcrafted Vue Components.">
                </v-card>
              </v-col>
              <v-col cols="12" md="6">
                <v-card append-icon="mdi-arrow-right-bold" href="https://vite.dev/" target="_blank"
                  class="fill-height" title="Vite" subtitle="The Build Tool for the Web"
                  text="Vite is a blazing fast frontend build tool powering the next generation of web applications.">
                </v-card>
              </v-col>
            </v-row>
            <p class="text-center mt-16 text-grey">
              Laravel v{{ laravelVersion }} (PHP v{{ phpVersion }})
            </p>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>