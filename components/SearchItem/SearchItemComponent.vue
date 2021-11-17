<template>
<div class="flex flex-row my-5 px-5 gap-x-5">
    <img :src="`https://image.tmdb.org/t/p/w500/${props.poster}`" alt="poster-image" class="w-20 rounded-xl" v-if="props.poster"/>
    <img :src="`https://www.edlinkeducation.com/global_assets/image/Event/default.jpg`" alt="poster-image" class="w-20 rounded-xl object-cover" v-else/>
    <div>
    <p class="font-bold text-lg text-white">{{props.title}}</p>
    <div>
      <p class="text-xs text-white text-opacity-50 truncate w-64">{{props.description}}</p>
    </div>
    <div class="flex flex-row content-center gap-x-2 mt-1 mb-5">
      <font-awesome-icon :icon="['fas', 'star']" class="text-yellow-400 text-sm"/>
      <p class="text-xs text-white">{{props.vote}}</p>
    </div>
    <button class="bg-gray-800 rounded-lg px-4 py-2 text-xs font-bold text-white hover:bg-gray-200 hover:text-gray-900">Watch Now</button>
  </div>
</div>
</template>
<script>
export default {
  props: {
    props: Object,
    default: () => {},
  },
};
</script>
