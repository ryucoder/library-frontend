<template>

    <div>
        <NuxtLink to='/books'>
            Book List Page
        </NuxtLink>
    </div>

    <div>
        <h1> Book Detail Page</h1>
        <h1> Book ID {{ book_id }}</h1>
    </div>

    <div v-if="book">
        <h2>Title: {{ book.title }}</h2>
        <h2>Description: {{ book.description }}</h2>
        <!-- <h2>Author : {{ book.author }}</h2> -->
        <h2>Recommended : {{ book.is_recommended }}</h2>
        <h2>Average Rating : {{ book.avg_rating }}</h2>
    </div>

</template>

<script setup>

const runtimeConfig = useRuntimeConfig()
const route = useRoute()
const book_id = route.params.id
const currentUrl = runtimeConfig.public.apiBase + "books/" + book_id

// console.log(runtimeConfig.public.apiBase)
// console.log(currentUrl)
let book = false;

const { data } = await useFetch(currentUrl)

book = data.value;

console.log(route.params.id)
console.log(data.value);

</script>