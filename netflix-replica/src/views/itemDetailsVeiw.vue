<script setup>
import Topbar from '../components/Topbar.vue'
import itemDetails from '@/components/itemDetails.vue';
import Filter from '@/components/Filter.vue';
const sentId = ref(0)
function getDetails(id) {
    sentId.value = id
}
</script>

<template>
  <main>
    <Topbar />
    <itemDetails />
  </main>
</template>