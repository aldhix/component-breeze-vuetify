<script setup>
import InputError from "@/Components/InputError.vue";
import InputLabel from "@/Components/InputLabel.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import TextInput from "@/Components/TextInput.vue";
import { useForm } from "@inertiajs/vue3";
import { ref } from "vue";

const passwordInput = ref(null);
const currentPasswordInput = ref(null);

const form = useForm({
  current_password: "",
  password: "",
  password_confirmation: "",
});

const updatePassword = () => {
  form.put(route("password.update"), {
    preserveScroll: true,
    onSuccess: () => form.reset(),
    onError: () => {
      if (form.errors.password) {
        form.reset("password", "password_confirmation");
        passwordInput.value.focus();
      }
      if (form.errors.current_password) {
        form.reset("current_password");
        currentPasswordInput.value.focus();
      }
    },
  });
};
</script>

<template>
  <v-card class="pa-4 mb-5">
    <v-row>
      <v-col lg="4">
        <h6 class="text-h6 mb-2">Update Password</h6>
        <p class="text-grey-darken-3 mb-7">
          Ensure your account is using a long, random password to stay secure.
        </p>

        <form @submit.prevent="updatePassword">
          <v-text-field
            label="Current Password"
            v-model="form.current_password"
            :error-messages="form.errors.current_password"
            type="password"
            class="mb-3"
          />

          <v-text-field
            label="Password"
            v-model="form.password"
            :error-messages="form.errors.password"
            type="password"
            class="mb-3"
          />

          <v-text-field
            label="Confirmation Password"
            v-model="form.password_confirmation"
            :error-messages="form.errors.password_confirmation"
            type="password"
            class="mb-3"
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
