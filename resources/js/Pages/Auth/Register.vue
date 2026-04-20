<script setup>
import { useForm } from "@inertiajs/vue3";

const form = useForm({
    name: null,
    email: null,
    password: null,
    password_confirmation: null,
});
const submit = () => {
    form.post(route("register"), {
        onError: () => form.reset("password", "password_confirmation"),
    });
};
</script>

<template>
    <Head title=" | Register" />
    <h1 class="title">Registre uma nova conta</h1>
    <div class="w-2/4 mx-auto">
        <form @submit.prevent="submit">
            <div class="mb-6">
                <label>Nome</label>
                <input type="text" v-model="form.name" />
                <small>{{ form.errors.name }}</small>
            </div>
            <div class="mb-6">
                <label>Email</label>
                <input type="text" v-model="form.email" />
                <small>{{ form.errors.email }}</small>
            </div>
            <div class="mb-6">
                <label>Senha</label>
                <input type="password" v-model="form.password" />
                <small>{{ form.errors.password }}</small>
            </div>
            <div class="mb-6">
                <label>Confirmar Senha</label>
                <input type="password" v-model="form.password_confirmation" />
            </div>
            <div>
                <p class="text-slate-600 mb-2">
                    Já tem uma conta?
                    <a href="/login" class="text-link">Faça login</a>
                </p>
                <button class="primary-btn" :disabled="form.processing">
                    Registrar
                </button>
            </div>
        </form>
    </div>
</template>
