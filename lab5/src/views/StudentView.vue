<script setup lang="ts">
import StudentCard from '@/components/StudentCard.vue'
import type { StudentEvent } from '@/type'
import { ref, onMounted } from 'vue'
import StudentService from '@/services/StudentService'

const events = ref<StudentEvent[]>([])

onMounted(() => {
  StudentService.getStudents()
    .then((response) => {
      events.value = response.data
    })
    .catch((error) => {
      console.error('There was an error!', error)
    })
})
</script>

<template>
  <h1 class="text-2xl font-bold text-center my-4">Information For Student (need VPN)</h1>
  <div class="flex flex-col items-center">
    <StudentCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<style scoped>

</style>

