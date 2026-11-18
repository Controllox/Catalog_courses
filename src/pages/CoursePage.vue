<template>
    <div style="padding: 20px;">
        <div v-if="course">
            <h1>{{ course.title }}</h1>
            <p>Категория: {{ course.category }}</p>
            <div style="margin-bottom: 20px;">
                <RouterLink to="description" style="margin-right: 15px;">Описание</RouterLink>
                <RouterLink to="program" style="margin-right: 15px;">Программа</RouterLink>
                <RouterLink to="reviews">Отзывы</RouterLink>
            </div>
            <RouterView />
            <br><br>
            <RouterLink to="/courses">← Назад к списку</RouterLink>
        </div>
        <div v-else>
            <h2>Курс не найден</h2>
            <RouterLink to="/courses">← Назад к списку</RouterLink>
        </div>
    </div>
</template>

<script setup>
import { computed, provide } from "vue";
import { courses } from "../data/courses";

const props = defineProps({ id: [String, Number] });

const course = computed(() => courses.find(c => c.id == props.id));
provide("currentCourse", course);
</script>