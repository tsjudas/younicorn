<template>
  <div class="top">
    <postview :posts="posts"></postview>
    <infinite-loading duration="10" @infinite="onInfinite"></infinite-loading>
  </div>
</template>

<style scoped>

</style>

<script>
import axios from 'axios';
import postview from '~/components/Posts';
export default {
  data() {
    return {
      page: 0,
      posts: [],
    }
  },
  components: {
    postview
  },
  computed: {
    limit() {
      return 100;
    }
  },
  methods: {
    onInfinite($state) {
      setTimeout(() => {
        axios.get(`${process.env.apiUrl}?page=${this.page}&limit=${this.limit}`).then(res => {
          this.posts = this.posts.concat(res.data.results);
          this.page++;
          if (res.data.results.length === this.limit) {
            $state.loaded();
          } else {
            $state.complete();
          }
        })
      }, 1000);
    }
  }
}
</script>
