<script setup lang="ts">
import { ref } from 'vue'
import { useForm } from '@inertiajs/vue3';


import {
    Dialog,
    DialogContent,
    DialogHeader,
    DialogTitle,
    DialogDescription
} from '@/components/ui/dialog';

const isOpen = defineModel<boolean>('open');

const form = useForm({
        title: '',
        content: '',
    });

const addNote = () => {
    form.post('/notes');
    isOpen.value = false;
    form.reset();
};

</script>
<template>
    <Dialog :open="isOpen">
        <DialogContent>
            <DialogHeader>
                <DialogTitle>Create Note</DialogTitle>
                <DialogDescription>
                    Here you can create a new note.
                </DialogDescription>
            </DialogHeader>
            <div>
                <form @submit.prevent="addNote">
                    <div class="mb-4">
                        <input v-model="form.title" type="text" placeholder="Nadpis" class="w-full p-2 border rounded" />
                    </div>
                    <div class="mb-4">
                        <textarea v-model="form.content" class="w-full p-2 border rounded">
                            Zde napište svou poznámku...
                        </textarea>
                    </div>
                    <button type="submit" class="px-4 py-2 bg-blue-500 text-white rounded">
                        Přidat poznámku
                    </button>
                </form>
            </div>
        </DialogContent>
    </Dialog>
</template>
