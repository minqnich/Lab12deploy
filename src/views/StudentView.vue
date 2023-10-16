<template>
  <div class="student flex flex-col items-center">
    <StudentCard
      v-for="student in students"
      :key="student.id"
      :student="student"
      class="mb-4"
    ></StudentCard>
  </div>
</template>

  <script lang="ts" setup>
  import StudentCard from '../components/StudentCard.vue'
  import type { studentInfo } from '@/info'
  import { ref, type Ref } from 'vue'
  import StudentsInfoServices from '@/services/StudentsInfoServices'
  const students: Ref<Array<studentInfo>> = ref([])
  StudentsInfoServices.getStudent().then((response) => {
    students.value = response.data
  })
  </script>
  <!-- <style>
  /* .student {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  </style> */ -->