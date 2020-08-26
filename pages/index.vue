<template>
  <div class="container">
    <div>
      <logo />
      <h1 class="title">
        eslint-wakaranai
      </h1>
      <h2 class="subtitle">
        My sensational Nuxt.js project
      </h2>
      <div class="links">
        <a href="https://nuxtjs.org/" target="_blank" class="button--green">
          Documentation
        </a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          class="button--grey"
        >
          GitHub
        </a>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  methods: {
    downloadFile() {
      const openRequest = window.indexedDB.open('cache', 1)
      openRequest.onsuccess = (ev: Event) => {
        const db = (ev.target as IDBOpenDBRequest).result as IDBDatabase
        const tx = db
          .transaction('filecache', 'readwrite')
          .objectStore('filecache')
          .index('id')

        tx.get(1).onsuccess = (ev: Event) => {
          const cache = <any>(ev.target as IDBOpenDBRequest).result
          if (cache) {
            const link = document.createElement('a')
            link.href = URL.createObjectURL(cache.contents)
            link.setAttribute('download', cache.fileName)
            link.click()
          }
        }
      }
    }
  }
})
</script>
