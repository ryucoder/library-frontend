<template>
    <div>
        <h1> Book Detail Page</h1>
        <h1> Book ID {{ id }}</h1>
    </div>
</template>

<script setup>
const route = useRoute()
const id = route.params.id
console.log(route.params.id)

</script>