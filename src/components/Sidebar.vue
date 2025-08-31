<script setup>
const props = defineProps(['active_note', 'notes']);
</script>

<template>
    <aside class="w-64 bg-gray-800 p-4">
        <div class="p-4">
            <button class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600" @click="$emit('new-note')">
                New Note
            </button>
        </div>
         <ul>
            <li v-for="note in props.notes" :key="note.id" @click="$emit('set-active-note', note.id)"
                class="mt-4 p-2 bg-gray-700 rounded hover:bg-gray-600 cursor-pointer flex justify-between items-center">
                <span>{{ note.title }}</span>
                <button class="text-red-500 hover:text-red-700" 
                @click="evt => $emit('delete-note', {id: note.id, evt})"> 
                Delete
            </button>
            </li>
        </ul>
<!--       <h2 class="text-xl font-bold mb-4">Sidebar</h2>
        <ul>
            <li class="mb-2"><a href="#" class="text-white hover:underline">Home</a></li>
            <li class="mb-2"><a href="#" class="text-white hover:underline">About</a></li>
            <li class="mb-2"><a href="#" class="text-white hover:underline">Contact</a></li>
        </ul>> -->
    </aside>
</template>