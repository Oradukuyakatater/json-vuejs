<template>
  <v-row class="ma-0 pa-0">
    <v-col class="ma-0 pa-0">
      <v-textarea
        v-model="page"
      ></v-textarea>
    </v-col>
    <v-col class="ma-0 pa-0">
      <GenericPage :content="JSON.parse(page)" />
    </v-col>
  </v-row>
</template>

<script setup>
  import GenericPage from '@/components/GenericPage.vue'
  import { reactive, computed, ref } from 'vue'

  const page = ref(`{
    "tabs": [
      {
        "title": "Agency",
        "cards": [
          {
            "title": "General",
            "inputs": "{item}"
          },
          {
            "title": "Contacts",
            "table": {
              "items": "/posts",
              "actions": [
                "delete"
              ]
            }
          }
        ]
      },
      {
        "title": "Devices",
        "table": {
          "items": "/locations/{item.id}/devices"
        }
      },
      {
        "title": "Vlans",
        "table": {
          "items": "/locations/{item.id}/vlans",
          "actions": [
            "delete"
          ]
        }
      },
      {
        "title": "Telecom Links",
        "table": {
          "items": "/locations/{item.id}/telecom_links",
          "actions": [
            "delete"
          ]
        }
      }
    ]
  }`)
</script>
