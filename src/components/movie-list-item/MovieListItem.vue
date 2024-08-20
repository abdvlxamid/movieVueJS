<template>
  <li
    class="list-group-item d-flex justify-content-between"
    :class="[{ like: movie.like }, { favourite: movie.favourite }]"
  >
    <span
      class="list-group-item-label"
      @click="$emit('onToggle', { id: movie.id, prop: 'like' })"
      >{{ movie.name }}</span
    >
    <input
      type="number"
      class="list-group-item-input"
      v-bind:value="movie.viewers"
    />
    <div class="d-flex justify-content-center align-items-center">
      <button
        type="button"
        class="btn btn-cookie btn-sm"
        @click="$emit('onToggle', { id: movie.id, prop: 'favourite' })"
      >
        <i class="fas fa-eye"></i>
      </button>
      <button type="button" class="btn btn-trash btn-sm" @click="onDelete">
        <i class="fas fa-trash"></i>
      </button>
      <i class="fas fa-moon"></i>
    </div>
  </li>
</template>
<script>
export default {
  props: {
    movie: {
      type: Object,
      required: true,
    },
  },
  methods: {
    onDelete() {
      this.$emit("onDelete", this.movie.id);
    },
  },
};
</script>
<style scoped>
.list-group-item {
  padding: 15px 20px;
  border-bottom: 1px solid #3d5a80;
}
.list-group-item:last-child {
  border-bottom: none;
}
.list-group-item span {
  line-height: 35px;
  font-size: 20px;
  cursor: pointer;
  width: 550px;
}
.list-group-item input {
  line-height: 20px;
  font-size: 20px;
  text-align: center;
  border: 0;
  outline: none;
}
.list-group-item button {
  width: 35px;
  height: 35px;
  margin: 3px;
  font-size: 17px;
  border: none;
  cursor: pointer;
}
.list-group-item .btn-cookie {
  color: #3d3d3c;
}
.list-group-item .btn-trash {
  color: #e5383b;
}
.list-group-item .fa-moon {
  width: 35px;
  height: 35px;
  text-align: center;
  line-height: 35px;
  font-size: 16px;
  color: #ffd700;
  transition: 0.3s all;
  transform: translateX(30px);
  opacity: 0;
}
.list-group-item.like .fa-moon {
  opacity: 1;
  transform: translateX(0);
}
.list-group-item.favourite .list-group-item-label,
.list-group-item.favourite .list-group-item-input {
  color: #e09f3e;
}
</style>
