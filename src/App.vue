<template>
  <div class="app">
    <header>
      <div class="title"><h1>Hyrule Jobs</h1></div>
      <div class="sort">
        <button @click="handleClick('title')">Order by Title</button>
        <button @click="handleClick('location')">Order by Location</button>
        <button @click="handleClick('salary')">Order by Salary</button>
      </div>
    </header>
    <div class="sort"></div>
    <JobList :jobs="jobs" :order="order" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import type Job from "./types/Job";
import JobList from "./components/JobList.vue";
import type OrderTerm from "./types/OrderTerm";

const initialJobs: Job[] = [
  {
    title: "farm worker",
    location: "lon-lon ranch",
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
    salary: 350000,
    id: "3",
  },
  {
    title: "fisherman",
    location: "lake hyla",
    salary: 21000,
    id: "4",
  },
  {
    title: "prison guard",
    location: "gerudo valley",
    salary: 32000,
    id: "5",
  },
];

export default defineComponent({
  components: {
    JobList,
  },
  setup() {
    const jobs = ref<Job[]>(initialJobs);

    const order = ref<OrderTerm>("title");
    const handleClick = (term: OrderTerm) => {
      order.value = term;
    };

    return {
      jobs,
      order,
      handleClick,
    };
  },
});
</script>

<style>
@import url("./assets/global.css");

.sort,
.title {
  @apply flex items-center w-full justify-center;
  @apply max-w-screen-lg m-auto my-10;
}

.title {
  @apply text-5xl mt-6;
}

.sort {
  @apply gap-4;
}
.sort button {
  @apply text-cerulean-500 py-2 px-4 rounded-lg w-48 h-11 bg-white;
  @apply cursor-pointer font-bold hover:opacity-75 border border-cerulean-500;
}
</style>
