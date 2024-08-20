<template>
  <div>
    <button
      v-for="btn in filterButtons"
      :key="btn.name"
      class="btn"
      @click="filterHandler(btn.name)"
      :class="[
        filterName === btn.name ? 'btn-warning' : 'btn-outline-secondary',
      ]"
    >
      {{ btn.title }}
    </button>
  </div>
</template>
<script>
export default {
  props: {
    updateFilterHandler: {
      type: Function,
      required: true,
    },
    filterName: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      filterButtons: [
        {
          title: "Barcha kinolar",
          name: "all",
        },
        {
          title: "Mashhur kinolar",
          name: "popular",
        },
        {
          title: "Eng ko'p ko'rilgan kinolar",
          name: "mostViewers",
        },
      ],
    };
  },
  methods: {
    filterHandler(filter) {
      this.filter = filter;
      this.updateFilterHandler(this.filter);
    },
  },
};
</script>
<style></style>
