<template>
  <div class="review-container">
    <h3>Reviews:</h3>
    <ul>
      <li v-for="(review, index) in reviews" :key="index">
        {{ review.name }} gives this {{ review.rating }} stars
        <br />
        "{{ review.review }}"
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  props: {
    reviews: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {};
  },
};
</script>
<style scoped></style>
