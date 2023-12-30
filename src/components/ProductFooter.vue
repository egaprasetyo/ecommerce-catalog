<script>
    export default {
        props: {
            price:Number,
            isMenClothing: {
                type: Boolean,
                required: true
            },
            isWomenClothing: {
                type: Boolean,
                required: true
            }
        }
    }
</script>

<template>
    <div class="product-footer mt-15">
        <h2 class="font-price" :class="{'primary-blue' : isMenClothing, 'primary-purple' : isWomenClothing}">${{ price }}</h2>
    </div>
</template>

<style scoped>
    .font-price {
        font-size: 28px;
        font-style: normal;
        font-weight: 600;
        line-height: normal;
    }

    @media screen and (max-width: 600px) {
        .product-footer{
            display: flex;
            align-items: center;
            justify-content: center;
        }
    }
</style>