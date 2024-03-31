<script setup>
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import { Head } from "@inertiajs/vue3";
</script>

<template>
  <Head title="Dashboard" />

  <AuthenticatedLayout title="Dashboard" icon="mdi-view-dashboard">
    <v-card class="pa-5"> You're logged in! </v-card>
  </AuthenticatedLayout>
</template>
