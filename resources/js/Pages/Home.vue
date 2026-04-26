<script setup>
import { ref, watch } from "vue";
import PagenationLinks from "./Components/PagenationLinks.vue";
import { router } from "@inertiajs/vue3";
import { debounce } from "lodash";

const props = defineProps({
    users: Object,
    searchTerm: String,
    can: Object,
});

const search = ref(props.searchTerm);

watch(
    search,
    debounce(
        (q) => router.get("/", { search: q }, { preservState: true }),
        1000,
    ),
);

// Format date
const getDate = (date) =>
    new Date(date).toLocaleDateString("pt-br", {
        year: "numeric",
        month: "long",
        day: "numeric",
    });
</script>

<template>
    <Head :title="` | ${$page.component}`" />
    <h1 class="text-3xl font-bold">Home</h1>

    <div class="flex justify-end mb-4">
        <div class="w-1/4">
            <input type="search" placeholder="Procurar..." v-model="search" />
        </div>
    </div>

    <table>
        <thead>
            <tr class="bg-slate-300">
                <th>Avatar</th>
                <th>Nome</th>
                <th>Email</th>
                <th>Data de cadastro</th>
                <th v-if="can.delete_user">Deletar</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="user in users.data" :key="user.id">
                <td>
                    <img
                        :src="
                            user.avatar
                                ? 'storage/' + user.avatar
                                : 'storage/avatars/avatar.png'
                        "
                        class="avatar"
                        alt=""
                    />
                </td>
                <td>{{ user.name }}</td>
                <td>{{ user.email }}</td>
                <td>{{ getDate(user.created_at) }}</td>
                <td v-if="can.delete_user">
                    <button
                        @click="router.delete(`/users/${user.id}`)"
                        class="text-red-500"
                    >
                        Deletar
                    </button>
                </td>
            </tr>
        </tbody>
    </table>

    <div>
        <PagenationLinks :paginator="users" />
    </div>
</template>
