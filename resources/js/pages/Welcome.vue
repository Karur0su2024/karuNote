<script setup lang="ts">
// 1. Definujte props (co dostanete z Laravel)
defineProps<{
    canRegister: boolean;



}>();

const message = 'Vítejte na mé nové stránce!';


</script>

<template>
    <div class="p-5">
        <h1 class="text-3xl">karuNote</h1>
    </div>
    <div class="p-8 m-6 bg-white rounded-lg shadow-md">
        <p>{{ message }}</p>
    </div>
</template>
