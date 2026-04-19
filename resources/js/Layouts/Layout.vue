<script setup></script>

<template>
    <div>
        <header class="bg-gray-800 text-white">
            <nav
                class="flex items-center justify-between p-4 max-w-screen-lg mx-auto"
            >
                <div class="space-x-6">
                    <Link href="/" class="mr-4">Home</Link>
                    <Link href="/about" class="mr-4">About</Link>
                </div>
            </nav>
        </header>
        <main class="p-4">
            <slot />
        </main>
    </div>
</template>
