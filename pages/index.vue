<template>
  <v-card-text>
    <v-text-field
      color="white"
      hide-no-data
      hide-selected
      item-text="Description"
      item-value="API"
      label="エンターキーで検索"
      placeholder="トーク内の単語を検索します"
      prepend-icon="mdi-database-search"
      return-object
      @click:append="search"
      @keydown.enter="search"
    >
    </v-text-field>
    <div v-if="hits.length > 0">
      <v-col v-for="(hit, i) in hits" :key="i" cols="12">
        <Results :item="hit" />
      </v-col>
    </div>
    <div v-else-if="query === ''">
      <v-card dark>
        <div class="d-flex flex-no-wrap justify-space-between">
          <div>
            <v-card-subtitle v-text="desc"></v-card-subtitle>
          </div>
        </div>
      </v-card>
    </div>
    <div v-else-if="loading">
      <v-card dark>
        <div class="d-flex flex-no-wrap justify-space-between">
          <div>
            <v-card-subtitle v-text="'検索中'"></v-card-subtitle>
          </div>
        </div>
      </v-card>
    </div>

    <div v-else>
      <v-card dark>
        <div class="d-flex flex-no-wrap justify-space-between">
          <div>
            <v-card-title class="headline" v-text="query"></v-card-title>

            <v-card-subtitle v-text="'該当なし'"></v-card-subtitle>
          </div>
        </div>
      </v-card>
    </div>
  </v-card-text>
</template>

<script>
import * as algoliasearch from 'algoliasearch'
import config from '~/algolia.config.js'
import Results from '~/components/results.vue'

const client = algoliasearch(config.appId, config.apiKey)
const index = client.initIndex('radio')

export default {
  components: {
    Results,
  },
  data() {
    return {
      hits: [],
      query: '',
      desc: 'そろそろやめたいラジオの配信の中身を検索できます。',
      loading: false,
    }
  },
  methods: {
    async search(event) {
      if (event.keyCode !== 13) return
      this.query = event.target.value
      if (this.query === '') return

      this.loading = true
      this.$nuxt.$loading.start()
      const searchResult = await index.search(this.query)
      console.log(searchResult)
      this.hits = searchResult.hits
      this.$nuxt.$loading.finish()
      this.loading = false
    },
  },
}
</script>
