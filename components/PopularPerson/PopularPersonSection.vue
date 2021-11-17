<template>
  <div class="px-5 py-5 mt h-full text-white">
    <div class="grid grid-cols-2">
      <p>Popular People</p>
      <div class="text-right">
        <font-awesome-icon :icon="['fas', 'chevron-right']" class="text-sm" />
      </div>
    </div>
      <div v-for="(item, index) in resources" :key="item.id" class="px-3 py-3 my-2 border rounded-lg border-gray-700">
        <div class="flex flex-row gap-x-5">
          <p class="text-sm text-white">{{index+1}}</p>
          <p class="text-sm text-white font-bold">{{item.name}}</p>
          <div class="flex flex-row content-center gap-x-2 mt-1">
            <font-awesome-icon :icon="['fas', 'star']" class="text-yellow-400 text-sm animate-bounce"/>
            <p class="text-xs">{{item.vote}}</p>
          </div>
        </div>
      </div>
  </div>
</template>
<script>
import axios from 'axios';

const url = 'https://api.themoviedb.org/3/person/popular?api_key=db876852a9e607e29209e2f8f6c977cf';

export default {
  name: 'PopularPerson',
  data() {
    return {
      isLoading: false,
      resources: '',
    };
  },
  mounted() {
    this.getTopRated();
  },
  methods: {
    async getTopRated() {
      try {
        this.isLoading = true;
        const response = await axios.get(url);

        const { results } = response.data;
        console.log(results);

        this.resources = results.map((item) => ({
          id: item.id,
          name: item.name,
          vote: item.popularity,
          type: 'person',
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
