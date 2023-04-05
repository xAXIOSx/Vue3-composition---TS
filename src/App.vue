<template>
  <h1>{{ name }}</h1>
  <h3>{{ age }}</h3>
  <button @click="changeName(32)">Change Name!</button>
  <button @click="changeAge(true)">Change Age!</button>
</template>

<script lang="ts">
import {defineComponent} from "vue";

export default defineComponent({
  name: 'App',
  components: {},
  data() {
    return {
      name: 'Link',
      age: 23 as number | string
    }
  },
  methods: {
    changeName(newName: string) {
      this.name = newName
    },
    changeAge(newAge: number | string) {
      this.age = newAge
    }
  },
})

</script>


<style lang="scss">
@import "./assets/styles/style.scss";
</style>
