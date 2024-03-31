<script setup>
import { Link, useForm, usePage } from "@inertiajs/vue3";

defineProps({
  mustVerifyEmail: {
    type: Boolean,
  },
  status: {
    type: String,
  },
});

const user = usePage().props.auth.user;

const form = useForm({
  name: user.name,
  email: user.email,
});
</script>

<template>
  <v-card class="pa-4 mb-5">
    <v-row>
      <v-col lg="4">
        <h6 class="text-h6 mb-2">Profile Information</h6>
        <p class="text-grey-darken-3 mb-7">
          Update your account's profile information and email address.
        </p>
        <form @submit.prevent="form.patch(route('profile.update'))">
          <v-text-field
            label="Name"
            v-model="form.name"
            :error-messages="form.errors.name"
            class="mb-2"
          />

          <v-text-field
            label="Email"
            v-model="form.email"
            :error-messages="form.errors.email"
            type="email"
            class="mb-2"
          />

          <v-btn color="black" type="submit" :loading="form.processing">
            Save
          </v-btn>

          <Transition
            enter-active-class="transition ease-in-out"
            enter-from-class="opacity-0"
            leave-active-class="transition ease-in-out"
            leave-to-class="opacity-0"
          >
            <span
              v-if="form.recentlySuccessful"
              class="text-grey-darken-2 ms-1"
            >
              Saved.
            </span>
          </Transition>
        </form>
      </v-col>
    </v-row>
  </v-card>
</template>
