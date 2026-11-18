<template>
    <div style="padding: 20px; text-align: center;">
        <h2>Вход</h2>
        <form @submit.prevent="login">
            <input v-model="password" type="password" placeholder="Пароль (1234)">
            <button type="submit">Войти</button>
        </form>
        <p v-if="error" style="color: red;">{{ error }}</p>
    </div>
</template>

<script setup>
import { ref } from "vue";
import { useRouter, useRoute } from "vue-router";

const password = ref("");
const error = ref("");
const router = useRouter();
const route = useRoute();

const login = () => {
    if (password.value === "1234") {
        localStorage.setItem("authToken", "demo");
        const redirect = route.query.redirect || "/dashboard";
        router.push(redirect);
    } else {
        error.value = "Неверный пароль";
    }
    };
</script>