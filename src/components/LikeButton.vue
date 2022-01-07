<template>
  <div class="h1 mb-0">
    <!-- Change button and liked value when button is clicked (includes animation) -->
    <b-icon
      :class="liked ? 'rounded bg-danger p-1' : 'rounded bg-success p-1'"
      @click="liked = !liked"
      :icon="liked ? 'heart-fill' : 'heart'"
      :animation="liked ? 'throb' : ''"
    ></b-icon>
  </div>
</template>

<script>
export default {
  name: "LikeButton",
  data() {
    return {
      // Check if button has been clicked
      liked: false,
    };
  },
};
</script>