<template>
  <div class="job-list">
    <h3>Sorted by {{ order }}</h3>
    <TransitionGroup name="job-list" tag="ul">
      <li class="job" v-for="job in orderedJobs" :key="job.id">
        <h2>{{ job.title }} in {{ job.location }}</h2>
        <div class="salary">
          <img src="@/assets/img/rupee.svg" alt="">
          <p>{{ job.salary }} rupees</p>
        </div>
        <div class="description">
          <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Ullam porro
            dolorem reprehenderit ipsa magni optio rerum corporis maxime
            quibusdam quae tempore laudantium voluptas officia accusantium vero
            dolore, temporibus consectetur voluptate.
          </p>
        </div>
      </li>
    </TransitionGroup>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, PropType, watchEffect, computed } from "vue";
import Job from "@/types/Job";
import OrderTerm from "@/types/OrderTerm";

export default defineComponent({
  props: {
    jobs: {
      required: true,
      type: Array as PropType<Job[]>,
    },
    order: {
      required: true,
      type: String as PropType<OrderTerm>,
    },
  },
  setup(props) {
    let orderedJobs = computed(()=>{
      return [...props.jobs].sort((a: Job,b: Job)=>{
        return a[props.order] < b[props.order] ? -1 : 1
      })
    })

    return { orderedJobs }
      // if (props.order === "title") {
      //   jobsCopy.value.sort((a: Job, b: Job) => {
      //     return a.title < b.title ? -1 : a.title > b.title ? 1 : 0;
      //   });
      // } else if (props.order === "location") {
      //   jobsCopy.value.sort((a: Job, b: Job) => {
      //     return a.location < b.location ? -1 : a.location > b.location ? 1 : 0;
      //   });
      // } else {
      //   jobsCopy.value.sort((a: Job, b: Job) => {
      //     return a.salary - b.salary;
      //   });
      // }
  }
});

    // watchEffect(()=>{
    // if (props.order === "title") {
    //   props.jobs.sort((a: any, b: any) => {
    //     return a.title < b.title ? -1 : a.title > b.title ? 1 : 0;
    //   });
    // } else if (props.order === "location") {
    //   props.jobs.sort((a: any, b: any) => {
    //     return a.location < b.location ? -1 : a.location > b.location ? 1 : 0;
    //   });
    // } else {
    //   props.jobs.sort((a: any, b: any) => {
    //     return a.salary - b.salary;
    //   });
    // }
    // })
</script>

<style scoped lang="scss">
@import '../assets/styles/variables.scss';
.job-list {
  max-width: 1080px;
  margin: 40px auto;

  h3 {
    color: $mainColor;
  }

  ul {
    padding: 0;
  }

  li {
    list-style-type: none;
    background: white;
    padding: 16px;
    margin: 16px 0;
    border-radius: 4px;
  }

  h2 {
    margin: 0 0 10px;
    text-transform: capitalize;
  }

  &-move {
    transition: all 0.5s ease;
  }
}
.salary {
  display: flex;

  img {
    width: 30px;
  }

  p {
    color: $mainColor;
    font-weight: bold;
    margin: 10px 4px;
  }
}
.description {
  p {
    color: black;
  }
}
</style>
