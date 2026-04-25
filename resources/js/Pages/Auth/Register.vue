<script setup>
import { useForm } from "@inertiajs/vue3";
import TextInput from "../Components/TextInput.vue";
import { Text } from "vue";

const form = useForm({
    name: null,
    email: null,
    password: null,
    password_confirmation: null,
    avatar: null,
    preview: null,
});
const submit = () => {
    form.post(route("register"), {
        onError: () => form.reset("password", "password_confirmation"),
    });
};

const change = (e) => {
    form.avatar = e.target.files[0];
    form.preview = URL.createObjectURL(e.target.files[0]);
};
</script>

<template>
    <Head title=" | Cadastrar" />
    <h1 class="title">Registre uma nova conta</h1>
    <div class="w-2/4 mx-auto">
        <form @submit.prevent="submit">
            <div class="grid place-items-center">
                <div
                    class="relative w-28 h-28 rounded-full overflow-hidden border border-slate-300"
                >
                    <label
                        for="avatar"
                        class="absolute inset-0 grid content-end cursor-pointer"
                        ><span class="bg-white/70 pb-2 text-center"
                            >Avatar</span
                        ></label
                    >
                    <input type="file" id="avatar" @input="change" hidden />
                    <img
                        class="object-cover w-28 h-28"
                        :src="form.preview ?? 'storage/avatars/avatar.png'"
                        alt="Avatar"
                    />
                </div>
                <p class="error mt-2">{{ form.errors.avatar }}</p>
            </div>
            <TextInput
                name="Nome"
                v-model="form.name"
                :message="form.errors.name"
            />

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
            <TextInput
                name="Confirmação de senha"
                type="password"
                v-model="form.password_confirmation"
            />
            <div>
                <p class="text-slate-600 mb-2">
                    Já tem uma conta?
                    <a :href="route('login')" class="text-link">Faça login</a>
                </p>
                <button class="primary-btn" :disabled="form.processing">
                    Registrar
                </button>
            </div>
        </form>
    </div>
</template>
