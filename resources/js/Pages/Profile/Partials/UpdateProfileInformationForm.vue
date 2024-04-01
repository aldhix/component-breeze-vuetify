<script setup>
import { useForm, usePage, router } from "@inertiajs/vue3";

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
          {{ mustVerifyEmail }} - {{ status }}
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

          <div
            class="mb-10"
            v-if="mustVerifyEmail && user.email_verified_at === null"
          >
            <p class="text-grey-darken-3 mb-3">
              Your email address is unverified.

              <v-btn
                color="blue"
                variant="tonal"
                class="text-none"
                :href="route('verification.send')"
                @click.prevent="router.post( route('verification.send') )"
              >
                Click here to re-send the verification email.
              </v-btn>
            </p>

            <p
              v-show="status === 'verification-link-sent'"
              class="text-green mt-3"
            >
              A new verification link has been sent to your email address.
            </p>
          </div>

          <div class="d-flex">
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
          </div>
        </form>
      </v-col>
    </v-row>
  </v-card>
</template>
