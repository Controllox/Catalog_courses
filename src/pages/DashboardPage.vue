<template>
    <div style="padding: 20px;">
        <h1>Личный кабинет</h1>
        <p>Вы авторизованы.</p>
        <button @click="logout">Выйти</button>
    </div>
</template>

<script setup>
import { useRouter } from "vue-router";
const router = useRouter();

const logout = () => {
    localStorage.removeItem("authToken");
    router.push("/login");
};
</script>