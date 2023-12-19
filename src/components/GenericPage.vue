<template>
  <div>
    <template v-if="isTable">
      <v-data-table :title="content.title" :items="items" @row-click="handleRowClick" />
    </template>

    <template v-else-if="isTabs">
      <v-tabs v-model="tab_idx">
        <v-tab v-for="tab in content.tabs" :key="tab.title" :value="tab.title">{{ tab.title }}</v-tab>
      </v-tabs>
      <v-window v-model="tab_idx">
        <v-window-item v-for="tab in content.tabs" :key="tab.title" :value="tab.title">
          <GenericPage :content="tab" />
        </v-window-item>
      </v-window>
    </template>

    <template v-else-if="isCards">
      <v-card v-for="card in content.cards" :key="card.title">
        <v-card-title>{{ card.title }}</v-card-title>
        <v-card-text>
          <GenericPage :content="card" />
        </v-card-text>
      </v-card>
    </template>

    <template v-else>
      {{ content }}
    </template>
  </div>
</template>

<script>
export default {
  name: 'GenericPage',
  props: [
    'content'
  ],
  data() {
    return {
      tab_idx: 0,
      items: [],
      selectedItem: null,
    }
  },
  computed: {
    isTable: function() {
      return this.content && this.content.table
    },
    isTabs: function() {
      return this.content && this.content.tabs
    },
    isCards: function() {
      return this.content && this.content.cards
    },
  },
  mounted() {
    this.loadData()
  },
  methods: {
    loadData() {
      if (this.isTable) {
        const url = import.meta.env.VITE_API_BASE_URL + this.content.table.items
        fetch(url)
        .then(response => response.json())
        .then(json => {
          this.items = json
          console.log(this.items)
        }).catch(error => {
          console.error(error)
        })
      }
    },
    handleRowClick(e, type) {
      const param_content = this.contents.tabs
      if (type === 'page') {
        router.push({ name: 'GenericPage', params: { content: this.contents.onclick, item: e } })
      }
    },
  },
}
</script>
