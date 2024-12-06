<template>

    <div>
        <NuxtLink to='/books'>
            Book List Page
        </NuxtLink>
    </div>

    <div>
        <h1> Book Create Page</h1>
    </div>

    <div>
        <pre>
            {{ JSON.stringify(form, null, 2) }}
        </pre>
    </div>

    <form @submit.prevent="handleSubmit()">
        <div>
            <p>Title: </p>
            <input v-model="form.title" placeholder="Enter the title of the book" />
        </div>
        <div>
            <p>Description: </p>
            <textarea v-model="form.description"></textarea>
        </div>
        <div>
            <p>Recommended ? </p>
            <input type="checkbox" id="checkbox" v-model="form.is_recommended" />
            <label for="checkbox">{{ form.is_recommended }}</label>
        </div>

        <button type="submit">Add New Book</button>
    </form>
</template>


<script setup>
const runtimeConfig = useRuntimeConfig()
const currentUrl = runtimeConfig.public.apiBase + "books/"

const DEFAULT_VALUE = {
    title: "",
    description: "",
    is_recommended: false,
}

var form = ref(DEFAULT_VALUE)

async function handleSubmit() {
    console.log("\n");
    console.log("\n");
    console.log("LOGGED");
    console.log("form.value");
    console.log(form.value);

    const book = await $fetch(currentUrl, {
        method: 'POST',
        body: form.value
    })
    
    
    // .then((data) =>{
    //     form = ref(DEFAULT_VALUE)
    // }).catch((error) => {
    //     alert("FORM ERROR OCCURED");
    // })

    console.log("LOGGED");
    console.log("book");
    console.log(book);
    console.log(typeof(book));
    console.log("\n");
    console.log("\n");
}
</script>