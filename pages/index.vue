<template>
  <div class="font-poppins bg-gray-900 max-w-screen-sm mx-auto h-full">
    <NavigationBar />
    <div class="grid grid-cols-2 px-5 my-5 gap-x-5">
      <button :disabled="isMovieSelected" type="button" @click="checkTabs()" :class="`w-full bg-white rounded-xl py-3 text-gray-700 font-bold transition ease-in-out  ${!isMovieSelected ? 'bg-opacity-50' : ''}`">Movie</button>
      <button :disabled="isTVShowSelected" type="button" @click="checkTabs()" :class="`w-full bg-white rounded-xl py-3 text-gray-700 font-bold transition ease-in-out ${!isTVShowSelected ? 'bg-opacity-50' : ''}`">TV Shows</button>
    </div>
    <div v-if="isMovieSelected">
      <top-rated-movie />
      <most-popular-movie />
    </div>
    <div v-else>
      <MostPopularTV />
      <TopRatedTV />
    </div>
    <PopularPerson />
    <div class="mb-20"></div>
    <BottomNavigationBar />
  </div>
</template>

<script>
import TopRatedMovie from '../components/TopRated/TopRatedSection.vue';
import MostPopularMovie from '../components/MostPopular/MostPopularSection.vue';
import MostPopularTV from '../components/MostPopularTV/MostPopularSection.vue';
import TopRatedTV from '../components/TopRatedTV/TopRatedSection.vue';
import PopularPerson from '../components/PopularPerson/PopularPersonSection.vue';
import BottomNavigationBar from '../components/BottomNavigationBar.vue';

export default {
  components: {
    TopRatedMovie, MostPopularMovie, MostPopularTV, TopRatedTV, PopularPerson, BottomNavigationBar,
  },
  data() {
    return {
      isMovieSelected: false,
      isTVShowSelected: false,
    };
  },
  mounted() {
    this.isMovieSelected = true;
  },
  methods: {
    checkTabs() {
      if (!this.isMovieSelected) {
        this.isMovieSelected = true;
        this.isTVShowSelected = false;
      } else {
        this.isMovieSelected = false;
        this.isTVShowSelected = true;
      }
    },
  },
};
</script>
