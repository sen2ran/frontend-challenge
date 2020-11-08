<template>
  <p class="text-3xl text-white pb-5">Sortable Post List</p>
  <SinglePost
    v-for="(post, index) in posts"
    :post="post"
    :length="posts.length"
    :arrIndex="index"
    :key="post.id"
    @sorting-post="sortingPostFn"
  />
</template>

<script>
import SinglePost from "./SinglePost";
export default {
  components: {
    SinglePost,
  },
  props: ["posts"],
  methods: {
    sortingPostFn(payload) {
      this.$emit("sorting-post", payload);
    },
  },
};
</script>