<script setup>
</script>

<template>
  <v-app>
    <v-main class="d-flex align-center justify-center bg-grey-lighten-3">
      <v-container>
        <v-row>
          <v-col md="4" offset-md="4">
            <h1 class="text-center text-h4 font-weight-reguler mb-5">
              {{ $appName }}<span class="font-weight-thin">Admin</span>
            </h1>
            <slot />
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>
