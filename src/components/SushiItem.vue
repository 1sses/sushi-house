<template>
  <el-card class="card">
    <template #header>
      <el-image :src="item.image" fit="contain" />
      <el-row justify="space-between" align="middle">
        <h2>{{item.name}}</h2>
      </el-row>
    </template>
    <p class="composition">{{item.composition}}</p>
    <el-rate :model-value="item.rating" :disabled="true" />
    <el-divider style="margin: 10px 0" />
    <el-col>
      <h3>Отзыв:</h3>
      <p v-if="item.feedback" class="feedback">{{item.feedback}}</p>
      <p v-else class="feedback">Нет отзыва</p>
    </el-col>
    <el-button class="edit-btn" plain circle :icon="Edit" @click="$emit('edit', item)" />
  </el-card>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'
import { Edit } from '@element-plus/icons'

defineProps({
  item: {
    type: Object,
    required: true
  }
})
defineEmits(['edit'])
</script>

<style scoped>
.card {
  position: relative;
  width: 300px;
}

.edit-btn {
  position: absolute;
  top: 5px;
  right: 5px;
}

h2 {
  font-size: 20px;
  font-weight: 500;
}

h3 {
  margin-top: 0;
  font-size: 16px;
}

.composition {
  font-size: 13px;
  height: 70px;
}

.feedback {
  height: 50px;
  font-size: 13px;
}
</style>
<style>
div.el-card__header {
  padding-bottom: 0;
}
</style>
