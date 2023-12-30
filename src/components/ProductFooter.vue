<script>
    export default {
        props: {
            price:Number,
            isMenClothing: {
                type: Boolean,
                required: true
            },
            isWomanClothing: {
                type: Boolean,
                required: true
            }
        }
    }
</script>

<template>
    <div class="product-footer mt-15">
        <h2 class="font-price" :class="{'primary-blue' : isMenClothing, 'primary-purple' : isWomanClothing}">${{ price }}</h2>
    </div>
</template>

<style>

</style>