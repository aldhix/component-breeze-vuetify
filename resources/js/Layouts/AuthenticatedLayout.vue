<script setup>
import { ref } from "vue";
import { router } from "@inertiajs/vue3";

defineProps({
  title: {
    type: String,
    default: null,
  },
  icon: {
    type: String,
    default: null,
  },
});
const drawer = ref(true);
</script>

<template>
  <v-layout class="rounded rounded-md">
    <!-- Sidebar -->
    <v-navigation-drawer
      v-model="drawer"
      color="grey-darken-4"
      elevation="5"
      border="0"
    >
      <v-list-item
        class="py-3"
        prepend-avatar="/images/logo.png"
        :href="route('dashboard')"
        @click.prevent="router.get(route('dashboard'))"
      >
        <strong class="text-h5">{{ $appName }}</strong>
      </v-list-item>

      <v-divider />

      <v-list density="compact" nav>
        <v-list-item
          prepend-icon="mdi-view-dashboard"
          title="Dashboard"
          :href="route('dashboard')"
          @click.prevent="router.get(route('dashboard'))"
          :active="route().current('dashboard')"
        />
      </v-list>
    </v-navigation-drawer>

    <!-- Navbar -->
    <v-app-bar elevation="1">
      <template v-slot:prepend>
        <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
      </template>

      <v-toolbar-items>
        <v-btn id="menu-user" append-icon="mdi-menu-down">
          {{ $page.props.auth.user.name }}
        </v-btn>
        <v-menu activator="#menu-user">
          <v-list>
            <v-list-item
              title="Profile"
              prepend-icon="mdi-account"
              :href="route('profile.edit')"
              @click.prevent="router.get(route('profile.edit'))"
            />

            <v-list-item
              title="Log Out"
              prepend-icon="mdi-logout"
              :href="route('logout')"
              @click.prevent="router.post(route('logout'))"
            />
          </v-list>
        </v-menu>
      </v-toolbar-items>
    </v-app-bar>

    <!-- Main -->
    <v-main>
      <v-container style="min-height: calc(100vh - 129px)">
        <h1 class="text-h5 mb-5" v-if="title">
          <v-icon :icon="icon" class="me-2 mb-2" v-if="icon" />{{ title }}
        </h1>
        <slot />
      </v-container>
      <v-footer style="height: 65px" border>
        <strong class="text-grey">Copyright &copy; Aldhi Xar</strong>
      </v-footer>
    </v-main>
  </v-layout>
</template>