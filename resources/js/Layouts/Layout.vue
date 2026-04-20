<script setup></script>

<template>
    <div>
        <header>
            <nav>
                <div class="space-x-6">
                    <Link
                        :href="route('home')"
                        class="nav-link"
                        :class="{ 'bg-slate-700': $page.component === 'Home' }"
                        >Home</Link
                    >
                </div>
                <div v-if="$page.props.auth.user" class="space-x-6">
                    <Link
                        :href="route('dashboard')"
                        class="nav-link"
                        :class="{
                            'bg-slate-700': $page.component === 'Dashboard',
                        }"
                        >Dashboard</Link
                    >
                    <Link
                        :href="route('logout')"
                        method="post"
                        as="button"
                        type="button"
                        class="nav-link"
                        >Sair</Link
                    >
                </div>
                <div v-else class="space-x-6">
                    <Link
                        :href="route('register')"
                        class="nav-link"
                        :class="{
                            'bg-slate-700': $page.component === 'Auth/Register',
                        }"
                        >Cadastrar</Link
                    >
                    <Link
                        :href="route('login')"
                        class="nav-link"
                        :class="{
                            'bg-slate-700': $page.component === 'Auth/Login',
                        }"
                        >Entrar</Link
                    >
                </div>
            </nav>
        </header>
        <main class="p-4">
            <slot />
        </main>
    </div>
</template>
