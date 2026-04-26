<script setup>
import PagenationLinks from "./Components/PagenationLinks.vue";

defineProps({
    users: Object,
});

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

    <table>
        <thead>
            <tr class="bg-slate-300">
                <th>Avatar</th>
                <th>Nome</th>
                <th>Email</th>
                <th>Data de cadastro</th>
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
            </tr>
        </tbody>
    </table>

    <div>
        <PagenationLinks :paginator="users" />
    </div>
</template>
