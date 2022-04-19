<template>
  <el-header>
    <el-row justify="space-between" align="middle">
      <h1>Персональный учет по SushiHouse</h1>
      <div>
        <h2>Попробовано: {{items.reduce((acc, item) => item.rating ? ++acc : acc, 0)}} / {{items.length}}</h2>
      </div>
    </el-row>
  </el-header>
  <el-divider />
  <el-main class="main">
    <SushiItem
      v-for="item in items"
      :key="item.name"
      :item="item"
      @edit="editItem"
    />
    <EditDialog v-model="dialog" :item="editData" @save="saveSushi" />
  </el-main>

</template>

<script setup>
import { computed, ref } from 'vue'
import SushiItem from '@/components/SushiItem'
import sushi from '@/data/sushi'
import EditDialog from '@/components/EditDialog'

const dialog = ref(false)

const editData = ref({
  name: '',
  rating: 0,
  feedback: ''
})

const ratings = ref(JSON.parse(localStorage.getItem('sushi') || '[]'))

const items = computed(() => sushi.map(item => {
  const rating = ratings.value.find(r => r.name === item.name)
  return {
    ...item,
    rating: rating ? rating.rating : 0,
    feedback: rating ? rating.feedback : ''
  }
}))

const editItem = (item) => {
  editData.value = {
    name: item.name,
    rating: item.rating,
    feedback: item.feedback
  }
  dialog.value = true
}

const saveSushi = (name, { rating, feedback }) => {
  const ratingItem = ratings.value.find(r => r.name === name)
  if (ratingItem) {
    ratingItem.rating = rating
    ratingItem.feedback = feedback
  } else {
    ratings.value.push({ name, rating, feedback })
  }
  localStorage.setItem('sushi', JSON.stringify(ratings.value))
  dialog.value = false
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
  justify-content: center;
  flex-wrap: wrap;
  row-gap: 40px;
  column-gap: 40px;
  padding: 40px !important;
}
</style>
