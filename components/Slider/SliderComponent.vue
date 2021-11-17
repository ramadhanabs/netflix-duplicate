<template>
<div>
  <div class="inline-block px-2">
    <div class="text-white my-5 mx-auto">
      <img :src="imageURL" alt="poster-image" class="w-32 h-48 rounded-xl">
      <div class="w-32">
        <p class="text-normal font-semibold truncate mt-2">{{props.title}}</p>
      </div>
      <div class="flex flex-row content-center gap-x-2 mt-1">
          <font-awesome-icon :icon="['fas', 'star']" class="text-yellow-400 text-sm"/>
          <p class="text-xs">{{props.vote}}</p>
      </div>
    </div>
  </div>
</div>
</template>
<script>
export default {
  props: {
    props: {
      type: Object,
      default: () => {},
    },
  },
  computed: {
    imageURL() {
      if (this.props.type === 'person') {
        return `https://api.themoviedb.org/3/person/${this.props.id}/images?api_key=db876852a9e607e29209e2f8f6c977cf`;
      }
      return `https://image.tmdb.org/t/p/w500/${this.props.poster}`;
    },
  },
};
</script>
