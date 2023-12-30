<script>
    export default {
        props: {
            description: String
        }
    }
</script>

<template>
    <div class="product-description">
        <p class="font-product-description">{{ description }}</p>
    </div>
</template>

<style scoped>
    .product-description{
        padding-top: 20px;
        padding-bottom: 50px;
    }

    .font-product-description {
        color: var(--primary-dark);
        font-size: 20px;
    }

</style>