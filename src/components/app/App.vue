<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo
        :allMoviescount="movies.length"
        :favouriteMoviesCounter="movies.filter((c) => c.favourite).length"
      />
      <div class="search-panel">
        <SearchPanel :updateTermHandler="updateTermHandler" />
        <AppFilter
          :updateFilterHandler="updateFilterHandler"
          :filterName="filter"
        />
      </div>
      <MovieList
        :movies="onFilterHandler(onSeachHandler(movies, term), filter)"
        @onToggle="onToggleHandler"
        @onDelete="onDelHandler"
      />
      <MovieAddForm @createMovie="createMovie" />
    </div>
  </div>
</template>

<script>
import AppInfo from "@/components/app-info/AppInfo.vue";
import SearchPanel from "../search-panel/SearchPanel.vue";
import AppFilter from "../app-filter/AppFilter.vue";
import MovieList from "../movie-list/MovieList.vue";
import MovieAddForm from "../movie-add-form/MovieAddForm.vue";
export default {
  components: {
    AppInfo,
    SearchPanel,
    AppFilter,
    MovieList,
    MovieAddForm,
  },
  data() {
    return {
      movies: [
        {
          name: "Omar",
          viewers: 8121,
          favourite: false,
          like: true,
          id: 1,
        },
        {
          name: "Yusuf",
          viewers: 1232,
          favourite: false,
          like: false,
          id: 2,
        },
        {
          name: "Muhammad",
          viewers: 1211,
          favourite: true,
          like: false,
          id: 3,
        },
      ],
      term: "",
      filter: "all",
    };
  },
  methods: {
    createMovie(item) {
      this.movies.push(item);
    },
    onToggleHandler({ id, prop }) {
      this.movies = this.movies.map((item) => {
        if (item.id == id) {
          return { ...item, [prop]: !item[prop] };
        }
        return item;
      });
    },
    onDelHandler(id) {
      this.movies = this.movies.filter((item) => item.id !== id);
    },
    onSeachHandler(arr, term) {
      if (term.length == 0) {
        return arr;
      }
      return arr.filter((c) => c.name.toLowerCase().indexOf(term) > -1);
    },
    updateTermHandler(term) {
      this.term = term.toLowerCase();
    },
    onFilterHandler(arr, filter) {
      switch (filter) {
        case "popular":
          return arr.filter((c) => c.like);
        case "mostViewers":
          return arr.filter((c) => c.viewers > 1300);
        default:
          return arr;
      }
    },
    updateFilterHandler(filter) {
      this.filter = filter;
    },
  },
};
</script>

<style>
.app {
  height: 100vh;
  color: black;
}
.content {
  width: 1000px;
  min-height: 700px;
  background-color: #fff;
  margin: 0 auto;
  padding: 5rem 0;
}
.search-panel {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
