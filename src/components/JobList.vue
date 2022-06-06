<template>
  <div class="job-list">
    <p class="order">Order by {{ order }}</p>
    <transition-group name="list-container" tag="div">
      <div v-for="job in orderedJobs" :key="job.id" class="card">
        <h2>
          {{ job.title }} in {{ job.location }}
          <small>{{ job.salary }} rupees</small>
        </h2>

        <div class="description">
          <p>
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. Qui totam,
            corrupti et nisi explicabo eveniet placeat cum dicta eum vitae
            officia voluptas, voluptatem autem ipsam nemo at libero alias fuga!
          </p>
        </div>
      </div>
    </transition-group>
  </div>
</template>

<script lang="ts">
import type Job from "@/types/Job";
import { computed, defineComponent } from "vue";
import type { PropType } from "vue";
import type OrderTerm from "@/types/OrderTerm";

export default defineComponent({
  name: "JobList",
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
    const orderedJobs = computed(() => {
      return [...props.jobs].sort((a: Job, b: Job) => {
        return a[props.order] > b[props.order] ? 1 : -1;
      });
    });

    return {
      orderedJobs,
    };
  },
});
</script>

<style>
.job-list {
  @apply max-w-screen-lg my-10 m-auto;
}
.job-list .order {
  @apply text-cerulean-500 mb-2 capitalize;
}
.job-list ul {
  @apply p-0;
}
.job-list .card {
  @apply list-none bg-white p-4 my-0 mx-0 rounded-md;
  @apply mb-6 w-full;
}
.job-list h2 {
  @apply m-0 mb-2 capitalize font-bold text-2xl text-cerulean-500;
}
.job-list small {
  @apply text-cerulean-300 text-base font-bold my-3;
}
.list-container-move {
  transition: all 0.5s;
}
</style>
