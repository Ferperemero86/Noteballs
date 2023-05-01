<script setup>
import { ref } from 'vue'

import Note from '@/components/Notes/note.vue'

const newNote = ref('')
const newNoteRef = ref(null)
const notes = ref([])

const addNote = () => {
  let currentDate = new Date().getTime()
  let id = currentDate.toString()

  let note = {
    id,
    content: newNote.value
  }

  notes.value.unshift(note)
  newNote.value = ''
  newNoteRef.value.focus()
}

const deleteNote = (id) => {
  notes.value = notes.value.filter((note) => note.id !== id)
}
</script>

<template>
  <div class="notes">
    <div class="card has-background-success-dark p-4 mb-5">
      <div class="field">
        <div class="control">
          <textarea
            class="textarea"
            placeholder="Textarea"
            v-model="newNote"
            ref="newNoteRef"
          ></textarea>
        </div>
      </div>

      <div class="field is-grouped is-grouped-right">
        <div class="control">
          <button
            class="button is-link has-background-success"
            @click.prevent="addNote"
            :disabled="!newNote"
          >
            Add new note
          </button>
        </div>
      </div>

      <Note :note="note" v-for="note in notes" :key="note.id" @deleteClicked="deleteNote" />
    </div>
  </div>
</template>

<style></style>
