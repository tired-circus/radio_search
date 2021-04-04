<template>
  <v-card dark :href="item.radiotalk_url">
    <div class="d-flex flex-no-wrap justify-space-between">
      <div>
        <v-card-title class="headline" v-text="item.title"></v-card-title>

        <v-card-subtitle
          v-html="item._snippetResult.talk.value"
        ></v-card-subtitle>
      </div>
    </div>
  </v-card>
</template>

<script>
export default {
  props: {
    item: Object,
  },
  data() {
    return this.item
  },
}
</script>
<style lang="scss">
em {
  color: yellowgreen;
}
</style>
