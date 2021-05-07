<template>

    <div class="p-2">
        <div class="card h-100 shadow">

            <img 
                class="card-img-top mt-4 mb-2 px-3" 
                :src="productData.image" 
                :alt="productData.item"
            >

            <div class="card-body d-flex flex-column">
            
                <h5 class="card-title">
                    {{productData.title}}
                </h5>

                <p class="card-text">
                    {{productData.description.substr(0,100)}}...
                </p>

                <div class="flex-grow-1"></div>
                
                <h3 class='mb-3'>
                    {{productData.price.toFixed(2)}} $
                </h3>                
            
                <button 
                    class="btn btn-primary"
                    v-if='!inCart' 
                    @click="$emit('addToCart', productData)"
                >
                    <i class="fas fa-shopping-cart"></i>
                    Add to Cart
                </button>

                <button 
                    class="btn btn-outline-primary"
                    disabled 
                    v-else
                >
                    <i class="fas fa-shopping-cart"></i>
                    Already in Cart
                </button>

            </div>

        </div>
    </div>

</template>

<script>

    export default {
        
        props: [
            'productData', 
            'inCart'
        ],

        emits: [ 
            'addToCart' 
        ]
        
    }

</script>

<style scoped>

    .card img{
        height: 200px;
        object-fit:contain;
    }

</style>
