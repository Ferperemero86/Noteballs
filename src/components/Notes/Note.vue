<script setup>
import { defineProps, toRefs, computed } from 'vue'

const props = defineProps({
  note: {
    type: Object
  }
})

const { note } = toRefs(props)

const emit = defineEmits(['deleteClicked'])

const contentLength = computed(() => {
  let length = note.value.content.length
  let description = note.value.content.length > 1 ? 'characters' : 'character'
  return `${length} ${description}`
})

const handleDelete = () => {
  emit('deleteClicked', note.value.id)
}
</script>

<template>
  <div class="card mb-4">
    <div class="card-content">
      <div class="content">
        {{ note.content }}
      </div>
      <div class="has-text-right has-text-grey-light">
        <small>{{ contentLength }}</small>
      </div>
    </div>
    <footer class="card-footer">
      <a href="#" class="card-footer-item">Edit</a>
      <a href="#" class="card-footer-item" @click.prevent="handleDelete">Delete</a>
    </footer>
  </div>
</template>
