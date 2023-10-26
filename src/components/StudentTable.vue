<template>
  <div class="flex justify-center items-center h-screen">
    <div class="w-3/4">
      <table class="table-fixed w-full border border-collapse border-indigo-500 shadow-md rounded-md">
        <thead class="bg-indigo-500 text-white">
          <tr>
            <th class="px-4 py-2 border">Фото</th>
            <th class="px-4 py-2 border">ПІБ</th>
            <th class="px-4 py-2 border">Група</th>
            <th class="px-4 py-2 border">Оцінка</th>
            <th class="px-4 py-2 border">Практика</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="student in students" :key="student.id" class="bg-gray-100 hover:bg-gray-200 hover:text-black">
            <td class="px-4 py-2 border">
              <img v-if="isURL(student.photo)" :src="student.photo" alt="Student Photo">
              <span v-else>No Photo Available</span>
            </td>
            <td class="px-4 py-2 border">{{ student.name }}</td>
            <td class="px-4 py-2 border">{{ student.group }}</td>
            <td class="px-4 py-2 border">{{ student.mark }}</td>
            <td class="px-4 py-2 border">{{ student.isDonePr }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const students = ref([]);

const fetchStudents = async () => {
  try {
    const response = await axios.get('http://34.82.81.113:3000/students');
    students.value = response.data;
  } catch (error) {
    console.error('Error fetching students:', error);
  }
};

const isURL = (url) => {
  try {
    new URL(url);
    return true;
  } catch {
    return false;
  }
};

onMounted(() => {
  fetchStudents();
});
</script>
