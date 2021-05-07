<template>
   
    <section class='my-5 border p-5 shadow'>
        
        <i @click="closeCartMethod" style='cursor:pointer;' class="far fa-window-close fa-3x"></i>

        <h2>Shopping Cart</h2>

        <table class="table">

            <thead>
                <tr>
                    <th scope="col">#</th>
                    <th scope="col">Image</th>
                    <th scope="col">Title</th>
                    <th scope="col">Quantity</th>
                    <th scope="col">Price</th>
                    <th scope="col">Cost</th>
                    <th scope="col"></th>
                </tr>
            </thead>

            <tbody>
                <tr v-for='(cartItem, index) in cartList' :key='cartItem.product.id'>
                    <th scope="row">
                        {{index + 1}}
                    </th>
                    <td>
                        <img 
                            :src="cartItem.product.image" 
                            class='border p-1 item-image'
                        >
                    </td>
                    <td>
                        {{cartItem.product.title}}
                    </td>
                    <td>
                        <div class='d-flex justify-content-around align-items-center'>
                        
                            <button class='btn btn-outline-primary' @click='cartItem.quantity++'>
                                <i class="fas fa-plus"></i>
                            </button>
                            
                            {{cartItem.quantity}}
                            
                            <button class='btn btn-outline-primary' :disabled='cartItem.quantity < 2' @click='cartItem.quantity--'>
                                <i class="fas fa-minus"></i>
                            </button>
                       
                        </div>
                    </td>
                    <td>
                        {{cartItem.product.price}}$ 
                    </td>
                    <td>
                        {{ (cartItem.quantity * cartItem.product.price).toFixed(2) }}$
                    </td>
                    <td>  
                        <i 
                            title='Remove Item' 
                            @click='removeFromCartMethod(cartItem)' 
                            class="far fa-trash-alt fa-2x"
                        ></i>
                    </td>
                </tr>
            </tbody>

        </table>

        <h3>Total: {{itemsTotalCost}}$</h3>

        <button class='btn btn-success mt-3' disabled>Complete Order</button>
    </section>

</template>

<script>

    export default {

        props: [
            'cartList', 
            'removeFromCartMethod', 
            'itemsTotalCost', 
            'closeCartMethod'
        ]
        
    }

</script>

<style scoped>

    i.far {
        cursor: pointer;
    }

    section {
        position: relative;
    }

    section .fa-window-close{
        position: absolute;
        right: 15px;
        top: 10px;
        color: gray;
        
    }

    td, th {
        vertical-align:middle;
    }

    img.item-image {
        width:64px; 
        object-fit:contain;
    }
</style>