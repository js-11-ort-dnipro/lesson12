<template>

  <div class='container d-flex flex-column min-vh-100'>   
    
    <header>

      <div class="d-flex align-items-center justify-content-between">
            
        <h1>Shop-App</h1>

        <cart-widget  
          @click='showCart = !showCart' 
          :items-quantity='itemsQuantityInCart' 
          :items-total-cost='itemsTotalCostInCart'
        />

      </div>

    </header>

    <main class='flex-grow-1'>

      <cart-component 
        v-show='showCart'
        :cart-list='cart'
        :remove-from-cart-method='removeFromCart'
        :items-total-cost='itemsTotalCostInCart'
        :closeCartMethod='closeCart' 
      />

      <div v-show='!showCart' class="row row-cols-1 row-cols-md-2 row-cols-lg-4">
          
        <one-product 
          v-for='item in products' 
          :key='item.id'
          :product-data="item" 
          :in-cart="inCart(item)"
          @add-to-cart='addToCart'  
        />

      </div>
      
    </main>

    <footer class='text-center'>

      <h5 class='my-4 text-secondary'>Shop-App &copy; 2021</h5>
    
    </footer>

  </div>

</template>

<script>

  const URL = 'https://fakestoreapi.com/products';

  import OneProduct     from './components/OneProduct.vue';
  import CartWidget     from './components/CartWidget.vue';
  import CartComponent  from './components/CartComponent.vue';

  export default {

    components: {
      'one-product': OneProduct,
      'cart-widget': CartWidget,
      'cart-component': CartComponent
    },

    data(){

      return {
        products: [],
        cart: [],
        showCart: false
      }

    },

    methods: {

      addToCart(product){

        let checkIsExist = this.cart.filter(i => i.product.id === product.id);

        if(checkIsExist.length){
          
          checkIsExist[0].quantity++;

        }else{

          this.cart.push({
            product: product,
            quantity: 1
          });

        }
      },

      removeFromCart(cartItem){
        this.cart = this.cart.filter(i => i.product.id !== cartItem.product.id);
      },

      inCart(product){
        return this.cart.some(i => i.product.id === product.id);
      },

      closeCart(){
        this.showCart = false;
      }

    },

    computed: {

        itemsQuantityInCart(){
          return this.cart.reduce((acc, i) => acc + i.quantity, 0);
        },

        itemsTotalCostInCart(){
          return this.cart.reduce((acc, i) => acc + i.product.price * i.quantity, 0).toFixed(2);
        }   

    },

    async mounted(){
     
      let data = await fetch(URL);
      
      data = await data.json();

      this.products = data;

    }

  }

</script>

<style scoped>
  
</style>