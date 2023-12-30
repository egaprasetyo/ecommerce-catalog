
<script>
    import ButtonCatalog from './buttons/ButtonCatalog.vue'

    export default {
        components: {
            ButtonCatalog
        },
        props: {
            image: String       
        },
        methods: {
            nextProduct() {
                this.$emit('next-product');
            }
        }
    }
</script>

<template>
    <div class="wrapper-page-not-found flex flex-content-center flex-items-center">
        <img class="page-404" :src="image" alt="404 Not Found" width="80%">
        <div class="centered flex flex-content-center flex-items-center flex-column">
            <p class="mb-15">This product is unavailable to show</p>
            <ButtonCatalog type="dark-outline" :isButtonLarge="true" @click="nextProduct">Next Product</ButtonCatalog>
        </div>
    </div>
</template>

<style scoped>

    .wrapper-page-not-found{
        min-width: 1000px;
        min-height: 400px;
        position: relative;
    }

    .page-404{
        opacity: 0.2;
    }

    .centered {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }

    @media screen and (max-width: 600px) {
        p{
            text-align: center;
        }
        .wrapper-page-not-found{
            min-width: 100%;
            min-height: 400px;
        }

    }
    
</style>