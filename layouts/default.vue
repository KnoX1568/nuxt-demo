<template>
  <v-app>
    <v-app-bar>
      <v-app-bar-nav-icon variant="text" @click.stop="drawer = !drawer" />
      <v-toolbar-title :text="$t('app.title')" />
      <v-spacer />
      <v-btn @click="toggleTheme" :icon="(theme.global.current.value.dark) ? 'mdi-weather-sunny' : 'mdi-moon-waxing-crescent'" />
    </v-app-bar>

    <v-navigation-drawer
        v-model="drawer"
        :location="$vuetify.display.mobile ? 'top' : undefined"
    >
      <v-list>
        <v-list-item :title="$t('navigation.menu.label')" />
        <v-list-item-action>
          <v-select
              v-model="$i18n.locale"
              :label="$t('menu.language.select.label')"
              :items="$i18n.availableLocales"
          >
            <template v-slot:selection="{ item, props }">
              <v-list-item v-bind="props" :title="$t(`language.select.locale.${item.value}`)" />
            </template>
            <template v-slot:item="{ item, props }">
              <v-list-item v-bind="props" :title="$t(`language.select.locale.${item.value}`)" />
            </template>
          </v-select>
        </v-list-item-action>
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