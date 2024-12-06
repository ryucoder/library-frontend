<template>
    <div>
        <NuxtLink to='/'>
            Go Back To Index Page
        </NuxtLink>
    </div>

    <div>
        <h1> Book List Page

            <NuxtLink to='/books/create' class="createLink">
                Add New Book
            </NuxtLink>
        </h1>
    </div>

    <div v-if="data == null">
        No data
    </div>

    <div v-else>

        <div v-for="book in data" class="book">
            <h2>Id: {{ book.id }}</h2>
            <h2>Title: {{ book.title }}</h2>
            <h2>Description: {{ book.description }}</h2>
            <h2>Recommended : {{ book.is_recommended }}</h2>
            <h2>Average Rating : {{ book.avg_rating }}</h2>

            <NuxtLink :to="'books' + '/' + book.id" target="_blank">
                View Details
            </NuxtLink>
        </div>

    </div>
</template>

<script setup>

// import { onMounted, onBeforeMount } from 'vue'

// // NOTE: Need to find a way to update the prop of component from the data of lifecycle hook

// var booksData = ref();

// onMounted(async () => {
//     console.log("onMounted");
//     console.log(`the component is now onMounted.`);
//     var  { data }  = await useFetch(currentUrl);
//     booksData.value = data.value;
// })

const runtimeConfig = useRuntimeConfig();
const currentUrl = runtimeConfig.public.apiBase + "books/";

// console.log(runtimeConfig.public.apiBase)
// console.log(currentUrl)

var { data } = await useFetch(currentUrl);

</script>

<style>
.book {
    border: 1px solid red;
    margin: 15px 0;
    padding: 5px;
}

.createLink {
    float: right;
}
</style>