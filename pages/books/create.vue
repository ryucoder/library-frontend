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

    <form @submit.prevent="handleSubmit()" method="post">
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

var DEFAULT_VALUE = {
    title: "",
    description: "",
    is_recommended: false,
}

var form = reactive(DEFAULT_VALUE)

async function handleSubmit() {


    // form level validation goes here 
    // field level validation goes here 

    var formData = false;
    var formError = false;

    try {
        const book = await $fetch(currentUrl, {
            method: 'POST',
            body: form
        }).then((data) => {
            formData = data;
        }).catch((error) => {
            formError = error;
        })

        if (formData) {
            // Form got submitted successfully
            
            // resets form here
            form.title = "";
            form.description = "";
            form.is_recommended = true;
        }

        if (formError) {
            // Form submission was unsuccessful
            // Shows book creation failed server side error alerts here
        }

    }
    catch (err) {
        // shows something failed alert here
    }

}

</script>