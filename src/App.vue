<template>
  <div class="flex h-screen bg p-20">
    <div class="w-1/2">
      <SortablePostList :posts="posts" @sorting-post="sortingPostFn" />
    </div>
    <div class="w-1/2">
      <TimeTravel :actions="actions" @time-travel="timeTravelFn" />
    </div>
  </div>
</template>

<script>
import SortablePostList from "./components/SortablePostList";
import TimeTravel from "./components/TimeTravel";

export default {
  name: "App",
  components: {
    SortablePostList,
    TimeTravel,
  },
  data() {
    return {
      posts: [
        {
          userId: 1,
          id: 1,
          title:
            "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
          body:
            "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto",
        },
        {
          userId: 1,
          id: 2,
          title: "qui est esse",
          body:
            "est rerum tempore vitae\nsequi sint nihil reprehenderit dolor beatae ea dolores neque\nfugiat blanditiis voluptate porro vel nihil molestiae ut reiciendis\nqui aperiam non debitis possimus qui neque nisi nulla",
        },
        {
          userId: 1,
          id: 3,
          title: "ea molestias quasi exercitationem repellat qui ipsa sit aut",
          body:
            "et iusto sed quo iure\nvoluptatem occaecati omnis eligendi aut ad\nvoluptatem doloribus vel accusantium quis pariatur\nmolestiae porro eius odio et labore et velit aut",
        },
        {
          userId: 1,
          id: 4,
          title: "eum et est occaecati",
          body:
            "ullam et saepe reiciendis voluptatem adipisci\nsit amet autem assumenda provident rerum culpa\nquis hic commodi nesciunt rem tenetur doloremque ipsam iure\nquis sunt voluptatem rerum illo velit",
        },
        {
          userId: 1,
          id: 5,
          title: "nesciunt quas odio",
          body:
            "repudiandae veniam quaerat sunt sed\nalias aut fugiat sit autem sed est\nvoluptatem omnis possimus esse voluptatibus quis\nest aut tenetur dolor neque",
        },
      ],
      actions: [],
    };
  },
  methods: {
    sortingPostFn(payload) {
      let posts = [...this.posts];

      [
        posts[payload.index],
        posts[payload.isUp ? payload.index - 1 : payload.index + 1],
      ] = [
        posts[payload.isUp ? payload.index - 1 : payload.index + 1],
        posts[payload.index],
      ];
      this.posts = posts;

      let timeTravelPayload = {
        old: payload.index,
        new: payload.isUp ? payload.index - 1 : payload.index + 1,
        post: posts[payload.index + 1],
      };

      this.actions.push(timeTravelPayload);
    },
    timeTravelFn(index) {
      let timeTravelArray = this.actions.slice(index).reverse();
      this.actions = [...this.actions.slice(0, index)]; // remaining actions

      let posts = [...this.posts];
      for (let i = 0; i < timeTravelArray.length; i++) {
        [posts[timeTravelArray[i].new], posts[timeTravelArray[i].old]] = [
          posts[timeTravelArray[i].old],
          posts[timeTravelArray[i].new],
        ];
      }
      this.posts = posts;
    },
  },
};
</script>

<style  scoped>
.bg {
  background: linear-gradient(169deg, #6457b1 28.6%, #efefef 28.9%);
}
</style>