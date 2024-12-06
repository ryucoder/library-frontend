<template>
    <div>
        <h1> Book List Page</h1>
    </div>

    <div v-if="data == null">
        No data
    </div>

    <div v-else>

        <div v-for="book in data" class="book">
            <h2>Title: {{ book.title }}</h2>
            <h2>Description: {{ book.description }}</h2>
            <!-- <h2>Author : {{ book.author }}</h2> -->
            <h2>Recommended : {{ book.is_recommended }}</h2>
            <h2>Average Rating : {{ book.avg_rating }}</h2>
            <!-- 
            <li><NuxtLink target="_blank" :to="{ name: 'books' + "/" + "",  params: { id: book.id } }">View Details</NuxtLink></li> -->

            <NuxtLink :to="'books' + '/' + book.id" target="_blank">
                View Details
            </NuxtLink>
        </div>

    </div>
</template>

<script setup>
const runtimeConfig = useRuntimeConfig()
const currentUrl = runtimeConfig.public.apiBase + "books/"

// console.log(runtimeConfig.public.apiBase)
// console.log(currentUrl)

const { data } = await useFetch(currentUrl)

// console.log(data.value);

</script>

<style>
.book {
    border: 1px solid red;
    margin: 15px 0;
    padding: 5px;
}
</style>