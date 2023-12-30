<script setup>
    import PreviewItem from './PreviewItem.vue';
    import ProductHeader from './ProductHeader.vue';
    import ProductDescription from './ProductDescription.vue';
    import ProductFooter from './ProductFooter.vue';
    import PageNotFound from './PageNotFound.vue';
    import ButtonCatalog from './buttons/ButtonCatalog.vue';
    import image404 from '../assets/img/page404.jpg';
</script>

<script>
    export default {
        components: {
            PreviewItem,
            ProductHeader,
            ProductDescription,
            ProductFooter,
            PageNotFound,
            ButtonCatalog
        },
        data(){
            return {
                data: null,
                currentProductId: 1,
                isLoading: false
            }
        },
        methods: {
            async fetchData(currentProductId){
                this.isLoading = true;
                try {
                    const response = await fetch(`https://fakestoreapi.com/products/${currentProductId}`);
                    this.data = await response.json();
                } catch (error) {
                    console.error("Error fetching data:", error);
                } finally {
                    this.isLoading = false;
                }
            },
            nextProduct(){
                this.currentProductId++
                if(this.currentProductId > 20){
                    this.currentProductId = 1
                }
                this.fetchData(this.currentProductId);
            }
        },
        mounted(){
            this.fetchData(this.currentProductId);
        },
        computed: {
            isMenClothing(){
                return this.data && this.data.category === `men's clothing`;
            },
            isWomenClothing(){
                return this.data && this.data.category === `women's clothing`;
            },
            isOtherCategory(){
                return this.data && !this.isMenClothing && !this.isWomenClothing;
            }
        },

    };

</script>

<template>
    <div class="wrapper flex flex-items-center flex-content-center" :class="{'bg-gradient-blue' : isMenClothing, 'bg-gradient-purple' : isWomenClothing, 'bg-gradient-gray': isOtherCategory}">
        <span v-if="isLoading" class="loader"></span>
        <main v-if="!isLoading && data">     
            <div v-if="isMenClothing || isWomenClothing" class="row flex flex-items-center flex-content-center flex-wrap">
                <div class="col-40">
                    <PreviewItem :image="data.image" :title="data.title"/>
                </div>
                <div class="col-60">
                    <ProductHeader :title="data.title" :category="data.category" :rating="data.rating" :isMenClothing="isMenClothing" :isWomenClothing="isWomenClothing"/>
                    <hr>
                    <ProductDescription :description="data.description"/>
                    <hr>
                    <ProductFooter :price="data.price" :isMenClothing="isMenClothing" :isWomenClothing="isWomenClothing"/>    
                    <div class="button-group">
                        <ButtonCatalog type="primary" class="mr-20" :isMenClothing="isMenClothing" :isWomenClothing="isWomenClothing">Buy Now</ButtonCatalog>
                        <ButtonCatalog type="primary-outline" :isMenClothing="isMenClothing" :isWomenClothing="isWomenClothing" @click="nextProduct">Next Product</ButtonCatalog>
                    </div>
                </div>
            </div>
            <PageNotFound v-else :image="image404" @next-product="nextProduct"/>
        </main>
    </div>
</template>

<style scoped>
    .wrapper {
        min-height: 100vh;
        padding: 50px;
    }

    main {
        max-width: 1000px;
        border-radius: 10px;
        background: var(--color-white);
        box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.25);
    }

    .button-group{
        margin-top: 15px;
        padding: 10px 0px;
        display: flex;
        flex-wrap: nowrap;
    }

    @media screen and (max-width: 600px) {
        .button-group{
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        .button-group .mr-20{
            margin-right: 0px;
            margin-bottom: 10px;
        }

    }

    @media only screen and (min-width: 601px) and (max-width: 900px) {
        main{
            min-width: 500px;
        }
        .wrapper{
            flex-wrap: wrap;
        }

        .button-group{
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        .button-group .mr-20{
            margin-right: 0px;
            margin-bottom: 10px;
        }
    }

</style>
