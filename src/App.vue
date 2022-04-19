<template>
  <el-header>
    <h1>Персональный учет по SushiHouse</h1>
    <el-divider />
  </el-header>
  <el-main class="main">
    <SushiItem
      v-for="item in items"
      :key="item.name"
      :item="item"
      @edit="editItem"
    />
    <EditDialog v-model="dialog" :item="editData" />
  </el-main>

</template>

<script setup>
import { ref } from 'vue'
import SushiItem from '@/components/SushiItem'
import items from '@/data/sushi'
import EditDialog from '@/components/EditDialog'

const dialog = ref(false)

const editData = ref({
  name: '',
  rating: 0,
  feedback: ''
})

const editItem = (item) => {
  editData.value = {
    name: item.name,
    rating: item.rating,
    feedback: item.feedback
  }
  dialog.value = true
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@100;200;300;400;500;600;700;800;900&display=swap');

body {
  font-family: 'Inter', sans-serif;
}
h1 {
  font-weight: 500;
}

main {
  display: flex !important;
  flex-wrap: wrap;
  column-gap: 40px;
}
</style>
