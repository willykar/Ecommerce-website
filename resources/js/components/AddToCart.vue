<template>
    <div>
     <hr>
      <button class="btn btn-warning text-center" 
       v-on:click.prevent="addProductToCart()">
          Add To Cart
      </button>
    </div>
    </template>
    
    <script>
    export default {
        data() {
            return {
                
            }
        },
    
        props:['productId', 'userId'],
        methods: {
    
            //checking if user is logged in.
            async addProductToCart() {
                if(this.userId == 0 ) {
                    this.$toastr.e('You Need to login, To add this product in cart')
                    return;
                }
                //if user is logged in
    
                let response = await axios.post('/cart', {
                    'product_id':this.productId
                });

                this.$root.$emit('changeInCart', response.data.items)
                
            }
        },
    
        mounted() {
            console.log('Component mounted.')
        }
    
    
    }
    </script>