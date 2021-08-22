<template>
  <div class="container">
    <div class="div1">
      <div class="product">
        <div class="stock">
          <p v-if="productInStock > 10" class="inStock">In Stock</p>
          <p
            v-else-if="productInStock <= 10 && productInStock > 0"
            class="almostSold"
          >
            Almost Sold out
          </p>
          <p v-else class="outOfStock">out of stock</p>
          <p>InStock - {{ productInStock }}</p>
        </div>
        <div>
          <img v-bind:src="currentImage" />
        </div>
        <div class="img_detail">
          <strong>{{ productTitle }}</strong>
          <br />
          <span>
            <del :v-show="detail.prePrice">{{ detail.prePrice }}</del>
            &nbsp; <b>{{ detail.price }}</b></span
          >
        </div>
        <button
          class="button"
          :disabled="productInStock === 0"
          :class="{ disabledButton: productInStock === 0 }"
          @click="addToCart()"
        >
          Add To Cart
        </button>
      </div>
    </div>
    <div class="div1">
      <div class="details">
        <h1>Details</h1>
        <ul>
          <li v-for="info in detail.contains" :key="info.index">{{ info }}</li>
        </ul>
        <div
          v-for="(variant, index) in detail.variants"
          :key="variant.id"
          class="color-circle"
          :style="{ backgroundColor: variant.color }"
          @mouseover="updateImage(detail.id, index)"
        ></div>
      </div>
      <ReviewForm class="review" @review-submitted="addReview" />
    </div>
    <div class="div1" v-if="detail.reviews.length">
      <div class="reviewlist">
        <ReviewList :reviews="detail.reviews" />
      </div>
    </div>
  </div>
</template>
<script>
import ReviewForm from './ReviewForm.vue';
import ReviewList from './ReviewList.vue';
export default {
  props: {
    detail: {
      type: Object,
      required: true,
    },
  },
  components: {
    ReviewForm,
    ReviewList,
  },
  data() {
    ReviewForm;
    return {};
  },
  computed: {
    productTitle() {
      return this.detail.brand + ' ' + this.detail.name;
    },
    productInStock() {
      return this.detail.variants[this.detail.variantIndex].quantity;
    },
    currentImage() {
      return this.detail.variants[this.detail.variantIndex].image;
    },
  },
  methods: {
    addToCart() {
      this.$emit('addToCart', this.detail);
    },
    updateImage(id, variantIndex) {
      this.$emit('changeProductColor', { id, variantIndex });
    },
    addReview(review) {
      this.$emit('addReview', { productID: this.detail.id, review });
    },
  },
};
</script>
<style scoped>
img {
  width: 330px;
  height: 360px;
}

.product,
.details,
.review,
.reviewlist {
  padding: 5px;
  border: 1px solid rgb(221, 180, 180);
  max-width: 350px;
  cursor: pointer;
  margin: 10px;
  border-radius: 5%;
}

.review {
  background-color: #fff;
}

.details {
  color: red;
}

.img_detail {
  background-color: gray;
  padding: 5px 0;
  border-radius: 5%;
  color: wheat;
}

.inStock {
  background-color: green;
  color: white;
  padding: 5px 0;
}

.outOfStock {
  background-color: red;
  color: white;
  padding: 5px 0;
}

.almostSold {
  background-color: orange;
  color: white;
  padding: 5px 0;
}
.container {
  display: flex;
}
.div1 {
  flex: 1 1 auto;
}

.color-circle {
  width: 50px;
  height: 50px;
  margin-top: 8px;
  border: 2px solid #d8d8d8;
  border-radius: 50%;
}
</style>
