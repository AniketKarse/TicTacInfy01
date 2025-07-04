<script setup>
// Just learning something Nuxt related!
const route = useRoute();
const nuxt = useNuxtApp();
console.log(route.params.id);
console.log(nuxt);
</script>

<template>
    <div>
        this is the event Id page
        
        event id: {{ $route.params.id }}
    </div>
</template>