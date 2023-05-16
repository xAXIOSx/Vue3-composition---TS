<template>
  <div class="app">
    <div class="title">
      <img src="./assets/img/heart.svg" alt="">
      <h1>Hyrule Jobs</h1>
    </div>
    <div class="order">
      <button @click="handleClick('title')">order by title</button>
      <button @click="handleClick('salary')">order by salary</button>
      <button @click="handleClick('location')">order by location</button>
    </div>
    <JobsList :jobs="jobs" :order="order"/>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, reactive, toRefs } from "vue";
import { Job, OrderTerm } from "@/types/allTypes";
import JobsList from "@/components/JobsList.vue";

export default defineComponent({
  name: "App",
  components: { JobsList },
  setup() {
    let jobs = ref<Job[]>([
      {
        title: "farm worker",
        location: "lon lon ranch",
        salary: 30000,
        id: "1",
      },
      {
        title: "quarryman",
        location: "death mountain",
        salary: 40000,
        id: "2",
      },
      {
        title: "flute player",
        location: "the lost woods",
        salary: 35000,
        id: "3",
      },
      { title: "fisherman", location: "lake hylia", salary: 21000, id: "4" },
      {
        title: "prison guard",
        location: "gerudo valley",
        salary: 32000,
        id: "5",
      },
    ]);

    let order = ref<OrderTerm>('title')

    const handleClick = (term: OrderTerm) => {
      order.value = term
    };

    return { jobs, handleClick, order };
  },
});
</script>

<style lang="scss">
@import './assets/styles/variables.scss';
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: sans-serif;
}
body {
  background-color: rgb(238, 238, 226);
}
.title {
  margin: 30px auto;
  display: flex;
  justify-content: center;
  img {
    width: 120px;
    margin-right: 20px;
    transform: translateY(-15px);
  }
  h1 {
    text-align: center;
    font-family: 'HyliaSerif';
    font-size: 80px;
    letter-spacing: 8px;
  }
}
.order {
  margin-top: 20px;
  display: flex;
  justify-content: center;
  button {
    margin: 0 10px;
    color: $mainColor;
    border: 2px solid $mainColor;
    background: lighten($color: $mainColor, $amount: 50%);
    padding: 18px 46px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
    font-size: 15px;
    text-transform: capitalize;
    transition: 0.2s;
    &:hover {
      background: lighten($color: $mainColor, $amount: 57%);
    }
  }
}
</style>
