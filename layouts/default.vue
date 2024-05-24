<template>
  <v-app>
    <v-app-bar>
      <v-app-bar-nav-icon variant="text" @click.stop="drawer = !drawer" />
      <v-toolbar-title text="Demo" />
      <v-spacer />
      <v-btn @click="toggleTheme" :icon="(theme.global.current.value.dark) ? 'mdi-weather-sunny' : 'mdi-moon-waxing-crescent'" />
    </v-app-bar>

    <v-navigation-drawer
        v-model="drawer"
        :location="$vuetify.display.mobile ? 'top' : undefined"
    >
      <v-list>
        <v-list-item title="Menu" />
      </v-list>
    </v-navigation-drawer>

    <v-main class="d-flex align-center justify-center" style="min-height: 300px">
      <slot />
    </v-main>
  </v-app>
</template>

<script setup lang="ts">
import { useTheme } from 'vuetify'

const theme = useTheme()

const drawer = ref<boolean>(false)

const toggleTheme = () => {
  theme.global.name.value = theme.global.current.value.dark ? 'light' : 'dark'
}
</script>