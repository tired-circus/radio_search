<template>
  <v-app dark>
    <v-card color="grey lighten-4" flat tile>
      <v-toolbar dense>
        <v-toolbar-title>RadioSearch</v-toolbar-title>

        <v-spacer></v-spacer>
      </v-toolbar>
    </v-card>
    <nuxt></nuxt>
    <v-footer>
      <v-col class="text-center" cols="12">
        {{ new Date().getFullYear() }}
        <v-btn
          link
          nuxt
          text
          color="link"
          href="https://github.com/tired-circus/radio_search"
          ><strong>tired-circus</strong>
        </v-btn>
      </v-col>
    </v-footer>
  </v-app>
</template>
