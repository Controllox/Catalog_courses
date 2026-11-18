<template>
    <div style="padding: 20px;">
        <h1>Каталог курсов</h1>
        <div style="margin-bottom: 20px;">
            <button @click="setFilter('all')" :disabled="filter == 'all'">
                Все
            </button>
            <button @click="setFilter('frontend')" :disabled="filter == 'frontend'">
                Frontend
            </button>
            <button @click="setFilter('backend')" :disabled="filter == 'backend'">
                Backend
            </button>
        </div>
        <div v-if="loading">
            <p>Загрузка...</p>
        </div>
        <ul v-else style="list-style: none; padding: 0;">
            <li v-for="course in filteredCourses" :key="course.id" 
            style="margin-bottom: 15px; 
            border: 1px solid #ccc; 
            padding: 10px;">
            <h3>
                {{ course.title }}
            </h3>
            <p>Категория: {{ course.category }}</p>
            <RouterLink :to="'/courses/' + course.id">
                Подробнее
            </RouterLink>
            </li>
        </ul>
        <p v-if="!loading && filteredCourses.length == 0">Нет курсов в этой категории.</p>
    </div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";
import { useRoute, useRouter } from "vue-router";
import { courses } from "../data/courses";

const route = useRoute();
const router = useRouter();

const filter = computed(() => route.query.category || "all");
const loading = ref(true);

const filteredCourses = computed(() => {
    if (filter.value === "all") return courses;
    return courses.filter(c => c.category === filter.value);
});
onMounted(() => {
    setTimeout(() => {
        loading.value = false;
    }, 1000);
});

const setFilter = (cat) => {
    router.push({ path: "/courses", query: { category: cat } });
};
</script>