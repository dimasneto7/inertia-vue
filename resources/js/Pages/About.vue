<script setup>
defineProps({
    user: String,
});
</script>

<template>
    <Head title=" | About" />
    <div class="text-3xl">
        <h1>About</h1>
        <p>{{ user }}</p>
    </div>
</template>
