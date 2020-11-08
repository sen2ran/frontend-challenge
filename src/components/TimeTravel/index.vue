<template>
  <div class="flex max-w-sm rounded overflow-hidden shadow-lg bg-gray-400 my-2">
    List of actions Commited
  </div>
  <div class="flex flex-col-reverse">
    <SingleTimeTravel
      v-for="(action, index) in actions"
      :key="index"
      :action="action"
      :index="index"
      @time-travel="timeTravelFn"
    />
  </div>
</template>

<script>
import SingleTimeTravel from "./SingleTimeTravel";
export default {
  props: ["actions"],
  components: {
    SingleTimeTravel,
  },
  methods: {
    timeTravelFn(index) {
      this.$emit("time-travel", index);
    },
  },
};
</script>