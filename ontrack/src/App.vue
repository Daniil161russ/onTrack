<script setup>
import { ref } from 'vue'
import TheHeader from './components/TheHeader.vue'
import TheNav from './components/TheNav.vue'
import TheActivities from './pages/TheActivities.vue'
import TheProgress from './pages/TheProgress.vue'
import TheTimeLine from './pages/TheTimeLine.vue'

import { PAGE_TIMELINE, PAGE_ACTIVITIES, PAGE_PROGRESS } from './constants'

const currentPage = ref(normalizePageHash())

function normalizePageHash() {
  const hash = window.location.hash.slice(1)

  if (Object.keys([PAGE_TIMELINE, PAGE_ACTIVITIES, PAGE_PROGRESS]).includes(hash)) {
    return hash
  }

  window.location.hash = PAGE_TIMELINE

  return PAGE_TIMELINE
}
</script>

<template>
  <TheHeader />

  <main class="flex flex-grow flex-col">
    <TheTimeLine v-show="currentPage === PAGE_TIMELINE" />
    <TheActivities v-show="currentPage === PAGE_ACTIVITIES" />
    <TheProgress v-show="currentPage === PAGE_PROGRESS" />
  </main>

  <TheNav :current-page="currentPage" @navigate="currentPage = $event" />
</template>
