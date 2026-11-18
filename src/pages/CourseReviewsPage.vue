<template>
    <div v-if="course">
        <h3>Отзывы</h3>
        <ul>
            <li v-for="(review, index) in course.reviews" :key="index">
                <strong>{{ review.author }}</strong> ({{ review.rating }}/5): {{ review.text }}
            </li>
        </ul>
    </div>
</template>

<script setup>
    import { inject } from "vue";
    const course = inject("currentCourse");
</script>