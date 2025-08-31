<script setup>
import { ref } from 'vue'
import Sidebar from './components/Sidebar.vue'

const notes = ref([]);
const active_note = ref(null);

const input_title = ref(''); 
const input_content = ref('');

function create_note() {
  const id = Math.random().toString(36).substring(2, 9);
  notes.value.push({
    id,
    title: 'Untitled',
    content: ''
  })
  set_active_note(id);
}

function set_active_note(id) {

  active_note.value = id;
  let note = notes.value.find(note => note.id === id);

  input_title.value = note.title;
  input_content.value = note.content; 

  setTimeout(() => {
    document.querySelector('input[type="text"]').focus();
  }, 0);
}

function update_note() {
  let note = notes.value.findIndex(note => note.id === active_note.value);
    notes.value[note].title = input_title.value;
    notes.value[note].content = input_content.value;
}

function delete_note({id, evt}) {
  evt.stopPropagation();
  let note = notes.value.findIndex(note => note.id === id);
  notes.value.splice(note, 1);
  active_note.value = null;
  input_title.value = '';
  input_content.value = '';
}

</script>

<template>
  <div class="bg-gray-700 text-white min-h-screen flex items-stretch justify-start">
    <Sidebar 
      :notes="notes" 
      :active_note="active_note"
      @new-note="create_note"
      @set-active-note="set_active_note"
      @delete-note="delete_note"
    />

    <main class="flex-1">
      <div v-if="active_note" class="p-6">
        <input v-model="input_title"
          @input="update_note"
        type="text" placeholder="Note Title" class="w-full p-2 mb-4 text-white rounded" />
        <textarea v-model="input_content"
          @input="update_note"
        placeholder="Write your note here..." class="w-full h-96 p-2 text-white rounded"></textarea>
      </div>
    </main>
  
  </div>
</template>
