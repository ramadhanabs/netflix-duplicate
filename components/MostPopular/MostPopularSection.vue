<template>
  <div class="px-5 py-5 mt h-full text-white">
    <div class="grid grid-cols-2">
      <p>Most Popular Movies</p>
      <div class="text-right">
        <font-awesome-icon :icon="['fas', 'chevron-right']" class="text-sm" />
      </div>
    </div>
    <div class="flex overflow-x-scroll hide-scroll-bar">
      <div v-for="(item) in resources" :key="item.id">
        <slider :props="item" v-if="!isLoading" />
        <skeleton v-else />
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios';
import Slider from '../Slider/SliderComponent.vue';
import Skeleton from '../Slider/Slider_skeleton.vue';

const url = 'https://api.themoviedb.org/3/movie/popular?api_key=db876852a9e607e29209e2f8f6c977cf';

export default {
  name: 'TopRated',
  components: { Slider, Skeleton },
  data() {
    return {
      isLoading: false,
      resources: '',
    };
  },
  mounted() {
    this.getMostPopular();
  },
  methods: {
    async getMostPopular() {
      try {
        this.isLoading = true;
        const response = await axios.get(url);

        const { results } = response.data;
        console.log(results);

        this.resources = results.map((item) => ({
          id: item.id,
          title: item.title,
          poster: item.poster_path,
          release_date: item.release_date,
          vote: item.vote_average,
        }));
      } catch (error) {
        console.log(error);
      } finally {
        this.isLoading = false;
      }
    },
  },
};
</script>
