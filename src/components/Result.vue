<template>
  <div>
    <ul class="list">
      <li class="item" v-for="item of items" :key="item.trackId">
        <div class="item-inner">
          <div class="photo">
            <img :src="item.artworkUrl100" alt="item.trackName" class="photo-img" />
          </div>
        </div>
        <div class="content">
          <p>
            <a :href="item.trackViewUrl" target="_blank" class="track">{{ item.trackName }}</a>
          </p>
          <p>
            <a :href="item.artistViewUrl" target="_blank" class="artist">{{ item.artistName }}</a>
          </p>
          <div class="data">
            {{ getYear(item.releaseDate) }} / {{ item.primaryGenreName }} / ￥{{ item.trackPrice }}
          </div>
        </div>
      </li>
    </ul>
    <Loading class="loading" v-show="loadProgress" />
  </div>
</template>

<script>
import Loading from '@/components/Loading.vue';

export default {
  props: ['items', 'loadProgress'],
  components: { Loading },
  methods: {
    getYear(dateStr) {
      const date = new Date(dateStr);
      return date.getFullYear();
    },
  },
};
</script>

<style scoped>
.item {
  padding: 20px 0;
}

.item:nth-of-type(even) {
  background-color: #f5f5f5;
}

.item-inner {
  display: flex;
  width: 90%;
  max-width: 600px;
  margin: auto;
}

.photo {
  flex: 0 0 150px;
}

.photo-img {
  width: 100%;
  display: block;
}

.content {
  flex: 1 1;
  padding-left: 20px;
}

.track {
  color: #42b883;
  font-size: 2rem;
  font-weight: 700;
  text-decoration: none;
}

.artist {
  display: block;
  color: #42b883;
  font-size: 1.4rem;
  font-weight: 700;
  text-decoration: none;
}

.data {
  margin-top: 1.5em;
  text-align: right;
  font-size: 1.2rem;
}

.loading {
  position: fixed;
  top: 70px;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1;
  background: #35495e;
}
</style>
