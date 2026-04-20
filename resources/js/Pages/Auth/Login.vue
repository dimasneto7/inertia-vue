<script setup>
import { useForm } from "@inertiajs/vue3";
import TextInput from "../Components/TextInput.vue";
import { Text } from "vue";

const form = useForm({
    email: null,
    password: null,
    remember: null,
});

const submit = () => {
    form.post(route("login"), {
        onError: () => form.reset("password", "remember"),
    });
};
</script>

<template>
    <Head title=" | Entrar" />
    <h1 class="title">Entrar na sua conta</h1>
    <div class="w-2/4 mx-auto">
        <form @submit.prevent="submit">
            <TextInput
                name="Email"
                type="email"
                v-model="form.email"
                :message="form.errors.email"
            />

            <TextInput
                name="Senha"
                type="password"
                v-model="form.password"
                :message="form.errors.password"
            />

            <div class="mb-4">
                <label for="remember">
                    <input
                        type="checkbox"
                        name="remember"
                        v-model="form.remember"
                        id="remember"
                        class="rounded border-gray-300 text-indigo-600 shadow-sm focus:ring-indigo-500"
                    />
                    Lembrar de mim
                </label>
            </div>

            <div>
                <p class="text-slate-600 mb-2">
                    Ainda não tem uma conta?
                    <a :href="route('register')" class="text-link"
                        >Crie uma conta</a
                    >
                </p>
                <button class="primary-btn" :disabled="form.processing">
                    Entrar
                </button>
            </div>
        </form>
    </div>
</template>
