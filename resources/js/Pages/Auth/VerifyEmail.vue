<script setup>
import { computed } from "vue";
import GuestLayout from "@/Layouts/GuestLayout.vue";
import ApplicationLogo from "@/Components/ApplicationLogo.vue";
import { Head, useForm, router } from "@inertiajs/vue3";

const props = defineProps({
  status: {
    type: String,
  },
});

const form = useForm({});

const submit = () => {
  form.post(route("verification.send"));
};

const verificationLinkSent = computed(
  () => props.status === "verification-link-sent"
);
</script>

<template>
  <GuestLayout>

    <Head title="Email Verification" />
    <v-container class="layout-login">

      <div class="text-center mb-5">
        <img src="/images/logo.png" alt="Logo" width="100">
      </div>

      <v-card class="pa-5">
        <p class="mb-5">
          Thanks for signing up! Before getting started, could you verify your
          email address by clicking on the link we just emailed to you? If you
          didn't receive the email, we will gladly send you another.
        </p>

        <p class="mb-5 text-green" v-if="verificationLinkSent">
          A new verification link has been sent to the email address you provided
          during registration.
        </p>

        <form @submit.prevent="submit">
          <div class="d-flex">
            <v-btn type="submit" color="black" :loading="form.processing">Resend Verification Email</v-btn>
            <v-btn class="ms-auto" color="blue" variant="tonal" :href="route('logout')"
              @click.prevent="router.post(route('logout'))">Log out</v-btn>
          </div>
        </form>
      </v-card>
    </v-container>

  </GuestLayout>
</template>
