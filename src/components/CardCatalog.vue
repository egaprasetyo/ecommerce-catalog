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
                console.log('Next Product Clicked');
                this.currentProductId++
                if(this.currentProductId > 20){
                    this.currentProductId = 1
                }
                console.log('Fetching data for product ID:', this.currentProductId);
                this.fetchData(this.currentProductId);
                event.stopPropagation();
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
            <div v-if="isMenClothing || isWomenClothing" class="row">
                <div class="col-35">
                    <PreviewItem :image="data.image" :title="data.title"/>
                </div>
                <div class="col-65">
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

</style>
