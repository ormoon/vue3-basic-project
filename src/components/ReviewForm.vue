<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <h3>Leave a review</h3>
    <div class="formInput">
      <label for="name">Name </label>
      <input
        type="text"
        name="name"
        id="name"
        v-model="name"
        ref="name"
        required
      />
    </div>
    <div class="formInput">
      <label for="review">Review </label>
      <input
        type="text"
        review="review"
        id="review"
        v-model="review"
        ref="review"
        required
      />
    </div>
    <div class="formInput">
      <label for="rating">Rating </label>
      <select
        name="rating"
        id="rating"
        v-model.number="rating"
        ref="rating"
        required
      >
        <option value="5">5</option>
        <option value="4">4</option>
        <option value="3">3</option>
        <option value="2">2</option>
        <option value="1">1</option>
      </select>
    </div>
    <button class="button" type="submit">Submit</button>
  </form>
</template>
<script>
export default {
  data() {
    return {
      name: '',
      review: '',
      rating: null,
    };
  },
  methods: {
    onSubmit() {
      let productReview = {
        name: this.name,
        review: this.review,
        rating: this.rating,
      };
      this.$emit('review-submitted', productReview);
      this.name = '';
      this.review = '';
      this.rating = null;
    },
  },
};
</script>
<style scoped>
.formInput {
  margin: 10px;
  text-align: left;
}

input,
select {
  font-size: 13px;
  padding: 3px;
}

select {
  width: 200px;
}
</style>
