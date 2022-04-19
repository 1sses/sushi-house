<template>
  <el-dialog
    v-model="dialog"
    width="400px"
  >
    <template #title>
      <h2 class="dialog-header">Редактировать<br> {{item.name}}</h2>
    </template>
    <h3>Отзыв:</h3>
    <el-input
      v-model="feedback"
      placeholder="Пиши тут"
    />
    <h3>Рейтинг:</h3>
    <el-rate
      v-model="rating"
      :max="5"
    />
    <template #footer>
            <span class="dialog-footer">
              <el-button @click="dialog = false">Отмена</el-button>
              <el-button type="primary" @click="saveItem">Сохранить</el-button>
            </span>
    </template>
  </el-dialog>
</template>

<script setup>
import { defineProps, defineEmits, computed, ref, watch } from 'vue'

const props = defineProps({
  item: {
    type: Object,
    required: true
  },
  modelValue: {
    type: Boolean,
    required: true
  }
})
const emit = defineEmits(['update:modelValue', 'save'])

const dialog = computed({
  get: () => props.modelValue,
  set: value => emit('update:modelValue', value)
})

const edited = ref({
  feedback: '',
  rating: 0
})

const feedback = computed({
  get: () => edited.value.feedback,
  set: value => {
    edited.value.feedback = value
  }
})
const rating = computed({
  get: () => edited.value.rating,
  set: value => {
    edited.value.rating = value
  }
})

watch(props, () => {
  edited.value = {
    feedback: props.item.feedback,
    rating: props.item.rating
  }
})

const saveItem = () => {
  emit('save', props.item.name, edited.value)
}
</script>

<style scoped>

</style>
