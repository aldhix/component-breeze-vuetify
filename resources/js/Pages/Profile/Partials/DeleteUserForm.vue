<script setup>
import { useForm } from "@inertiajs/vue3";
import { nextTick, ref } from "vue";

const confirmingUserDeletion = ref(false);
const passwordInput = ref(null);

const form = useForm({
  password: "",
});

const confirmUserDeletion = () => {
  confirmingUserDeletion.value = true;

  nextTick(() => passwordInput.value.focus());
};

const deleteUser = () => {
  form.delete(route("profile.destroy"), {
    preserveScroll: true,
    onSuccess: () => closeModal(),
    onError: () => passwordInput.value.focus(),
    onFinish: () => form.reset(),
  });
};

const closeModal = () => {
  confirmingUserDeletion.value = false;

  form.reset();
};
</script>

<template>
  <v-card class="pa-4">
    <v-row>
      <v-col lg="6">
        <h6 class="text-h6 mb-2">Delete Account</h6>
        <p class="text-grey-darken-3 mb-7">
          Once your account is deleted, all of its resources and data will be
          permanently deleted. Before deleting your account, please download any
          data or information that you wish to retain.
        </p>
        <v-btn color="red" @click="confirmUserDeletion">Delete Account</v-btn>
      </v-col>
    </v-row>
  </v-card>

  <v-dialog v-model="confirmingUserDeletion" width="auto">
    <v-card
      max-width="600"
      text="Once your account is deleted, all of its resources and data will be permanently deleted. Please enter your password to confirm you would like to permanently delete your account."
      title="Are you sure you want to delete your account?"
    >
      <v-card-text>

        <v-text-field
          label="Password"
          v-model="form.password"
          ref="passwordInput"
          :error-messages="form.errors.password"
          type="password"
          @keyup.enter="deleteUser"
        />
        
      </v-card-text>

      <template v-slot:actions>

        <v-btn class="ms-auto" @click="closeModal">Cancel</v-btn>

        <v-btn
          color="red"
          @click="deleteUser"
          variant="tonal"
          :loading="form.processing"
          >Delete Account</v-btn
        >
      </template>
    </v-card>
  </v-dialog>
</template>
