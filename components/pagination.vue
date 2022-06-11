<script setup>
const props = defineProps({
    currentPage: Number,
    totalPages: Number,
    model: String,
})
</script>
<template>
    <ul dir="ltr" class="flex ltr:justify-end my-4 gap-2">
        <NuxtLink v-if="props.currentPage > 1" :to="'?page=' + (props.currentPage - 1)"
            class="px-3 py2 rounded-lg bg-gray-200 hover:bg-gray-600 hover:text-white">
            Previous
        </NuxtLink>

        <NuxtLink v-if="props.currentPage < props.totalPages" :to="'/?page=' + (props.currentPage + 1)"
            class="px-3 py2 rounded-lg bg-gray-200 hover:bg-gray-600 hover:text-white">
            Next
        </NuxtLink>
    </ul>
</template>