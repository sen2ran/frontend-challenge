<template>
  <div class="flex max-w-sm rounded overflow-hidden shadow-lg bg-gray-200 my-2">
    <div class="w-10/12 p-3">
      <p lass="text-3xl">
        Moved "{{ action.post.title }}" from Index {{ action.old }} to Index
        {{ action.new }}
      </p>
    </div>
    <div class="w-2/12 flex flex-col">
      <button @click="timeTravelFn()">Time Travel</button>
    </div>
  </div>
</template>


<script>
export default {
  props: ["action", "index"],
  methods: {
    timeTravelFn() {
      this.$emit("time-travel", this.index);
    },
  },
};
</script>