<script>
export default {
    props: {
        image: String,
        title: String
    }
}
</script>
<template>
    <img class="" :src="image" :alt="title">
</template>

<style>
</style>