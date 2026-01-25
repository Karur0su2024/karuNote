<script setup lang="ts">

import { useForm } from '@inertiajs/vue3';
import { ref } from 'vue';

import CreateNote from './createNote.vue';
// 1. Definujte props (co dostanete z Laravel)
defineProps<{
    // canRegister: boolean;
    // numberOfUsers: number`
    notes: Array<{
        id: number;
        title: string;
        content: string;
        created_at: string;
        updated_at: string;
    }>;

}>();

const selectedNote = ref<{
    id: number;
    title: string;
    content: string;
    created_at: string;
    updated_at: string;
} | null>(null);
const isModalOpen = ref(false);

const openModal = (note: any) => {
    selectedNote.value = note;
    isModalOpen.value = true;
};

const message = 'Vítejte na mé nové stránce!';

const isCreateNoteOpen = ref(false);

</script>

<template>
    <div class="p-5">
        <h1 class="text-3xl">karuNote</h1>
    </div>

    <button class="px-4 py-2 bg-blue-500 text-white rounded" @click="isCreateNoteOpen = true">
        Vytvořit novou poznámku
    </button>

    <div class="p-8 m-2 bg-gray-100 rounded shadow-sm">
        <p>{{ message }}</p>
    </div>

    <div class="p-5">
        <h2 class="text-2xl mb-4">Seznam poznámek</h2>
        <div v-for="note in notes" :key="note.id" class="mb-4 p-4 border rounded">
            <h3 class="text-xl font-bold">{{ note.title }}</h3>
            <p class="mt-2">{{ note.content }}</p>
            <p class="text-sm text-gray-500 mt-2">Vytvořeno: {{ new Date(note.created_at).toLocaleDateString() }}</p>
            <button @click="openModal(note)" class="mt-2 px-3 py-1 bg-red-500 text-white rounded">
                Otevřít poznámku
            </button>
        </div>
    </div>

    <div v-if="isModalOpen" class="fixed inset-0 bg-black/50 flex items-center justify-center">
        <div class="bg-white p-6 rounded shadow-lg w-1/2">
            <h2 class="text-2xl font-bold mb-4">{{ selectedNote!.title ?? 'Nadpis' }}</h2>
            <p class="mb-4">{{ selectedNote!.content ?? 'Obsah poznámky' }}</p>
            <button @click="isModalOpen = false" class="px-4 py-2 bg-gray-500 text-white rounded cursor-pointer">
                Zavřít
            </button>
        </div>
    </div>

    <CreateNote v-model:open="isCreateNoteOpen" />

</template>
