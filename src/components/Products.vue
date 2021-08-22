<template>
  <div>
    <div>
      <div class="cart">Cart ({{ cart.length }})</div>
      <h1>{{ msg }}</h1>
      <div class="productList">
        <Product
          v-for="item in products"
          :key="item.id"
          :detail="item"
          class="div1"
          v-on:addToCart="addProductToCart"
          v-on:changeProductColor="changeImage"
          @addReview="addUserReview"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Product from './Product.vue';
export default {
  name: 'Products',
  components: { Product },
  props: {
    msg: String,
  },
  data() {
    return {
      cart: [],
      products: [
        {
          id: 1,
          name: 'Socks',
          brand: 'Nike',
          prePrice: '$30',
          price: '$20',
          variantIndex: 1,
          contains: ['15% cotton', '30% wool', '20% polyester'],
          variants: [
            {
              id: 2234,
              color: 'green',
              image: require('../assets/images/green-socks.jpg'),
              quantity: 15,
            },
            {
              id: 2235,
              color: 'blue',
              image: require('../assets/images/blue-socks.jpg'),
              quantity: 10,
            },
          ],
          reviews: [],
        },
        {
          id: 2,
          name: 'Socks2',
          brand: 'Under Armour',
          price: '$22',
          variantIndex: 0,
          contains: ['15% cotton', '30% wool', '20% polyester'],
          variants: [
            {
              id: 2234,
              color: 'green',
              image: require('../assets/images/green-socks.jpg'),
              quantity: 0,
            },
            {
              id: 2235,
              color: 'blue',
              image: require('../assets/images/blue-socks.jpg'),
              quantity: 10,
            },
          ],
          reviews: [],
        },
      ],
    };
  },
  methods: {
    addProductToCart({ id, variantIndex }) {
      for (let data of this.products) {
        if (data.id === id) {
          // reduce the current added items by one
          data.variants[variantIndex].quantity -= 1;
          // //add current item on cart and variant should be only that user clicked(i.e. for color and size)
          this.cart.push({ ...data, variants: data.variants[variantIndex] });
          break;
        }
      }
    },

    changeImage({ id, variantIndex }) {
      for (let data of this.products) {
        if (data.id === id) {
          data.variantIndex = variantIndex;
        }
      }
    },
    addUserReview({ productID, review }) {
      for (let data of this.products) {
        if (data.id === productID) {
          data.reviews.push(review);
        }
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.cart {
  float: right;
  margin-right: 5%;
  width: 100px;
  padding: 10px;
  border: 1px solid green;
  font-size: 20px;
  font-weight: bolder;
}
</style>
