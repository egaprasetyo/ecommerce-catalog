<script>
    export default {
        props: {
            title: String,
            category: String,
            rating: Object,
            isMenClothing: {
                type: Boolean,
                required: true
            },
            isWomenClothing: {
                type: Boolean,
                required: true
            }
        },
        computed: {
            roundedRating() {
                return this.rating && this.rating.rate ? Math.round(this.rating.rate) : 0;
            }
        }
    }
</script>

<template>
    <div class="product-header">
        <h1 :class="{'primary-blue': isMenClothing, 'primary-purple': isWomenClothing}">{{ title }}</h1>
        <div class="mt-25 flex flex-content-between flex-items-center">
            <p class="font-category-rating">{{ category }}</p>
            <div class="flex flex-content-between flex-items-center">
                <span v-if="rating && rating.rate" class="font-category-rating mr-10">{{rating.rate}}/5</span>
                <div class="flex flex-items-center gap-2">
                    <div v-for="index in 5" 
                         :key="index" 
                         class="rating-circle" 
                         :class="{ 
                            'bg-primary-blue': isMenClothing && index <= roundedRating, 
                            'bg-primary-purple': isWomenClothing && index <= roundedRating, 
                            'none-fill border-color-blue': isMenClothing && index > roundedRating,
                            'none-fill border-color-purple': isWomenClothing && index > roundedRating
                          }">
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .font-category-rating {
        color: var(--secondary-dark);
        font-size: 18px;
    }

    .rating-circle{
        width: 18px;
        height: 18px;
        border-radius: 50%;   
    }

    .none-fill{
        border: 1.5px solid;
    }
</style>