<template class="bg-gray-900">
  <div class="font-poppins max-w-screen-sm mx-auto h-100">
    <NavigationBar />
    <div class="flex flex-row my-5 justify-center px-5">
      <input v-model="search" type="text" class="bg-white border rounded-l-xl border-gray-300 border-r-0 w-full py-2 px-3" placeholder="Search Film Here">
      <button type="button" class="bg-gray-100 hover:bg-gray-200 transition rounded-r-xl py-2 px-3 text-gray-900">
        <div>
          <font-awesome-icon :icon="['fas', 'search']" class="text-center"  />
        </div>
      </button>
    </div>
    <div class="flex flex-row mt-48 mx-5" v-if="isEmpty">
      <div class="mx-auto">
        <div class="flex flex-row justify-center">
          <font-awesome-icon :icon="['fas', 'film']" class="text-6xl text-gray-500" />
        </div>
        <p class="text-sm text-bold text-gray-500">Search your movies here!</p>
      </div>
    </div>
    <div v-for="item in resources" :key="item.id">
      <SearchItem :props="item" v-if="!isLoading" />
      <Skeleton v-else />
    </div>
    <div class="mb-28"></div>
    <BottomNavigationBar />
  </div>
</template>
<script>
import axios from 'axios';
import NavigationBar from '../components/NavigationBar.vue';
import BottomNavigationBar from '../components/BottomNavigationBar.vue';
import SearchItem from '../components/SearchItem/SearchItemComponent.vue';
import Skeleton from '../components/SearchItem/SearchItem_skeleton.vue';

export default {
  name: 'SearchPage',
  components: {
    NavigationBar, BottomNavigationBar, SearchItem, Skeleton,
  },
  data() {
    return {
      isEmpty: true,
      isLoading: false,
      resources: {},
      search: '',
    };
  },
  watch: {
    search(value) {
      if (this.search.length > 2) {
        this.searchData(value);
        this.isEmpty = false;
      }
      if (this.search.length === 0) {
        this.resources = '';
        this.isEmpty = true;
      }
    },
  },
  methods: {
    async searchData(value) {
      try {
        this.isLoading = true;
        const response = await axios.get(`https://api.themoviedb.org/3/search/movie?api_key=db876852a9e607e29209e2f8f6c977cf&language=en-US&page=1&query=${value}&include_adult=false`);
        const { results } = response.data;
        this.resources = results.map((item) => ({
          id: item.id,
          title: item.original_title,
          poster: item.poster_path,
          vote: item.vote_average,
          description: item.overview,
          release_date: item.release_date,
        }));
        console.log(results);
      } catch (error) {
        console.log(error);
      } finally {
        this.isLoading = false;
      }
    },
  },
};
</script>
