<script setup>
import { gameList } from '../assets/history'
import GameInfo from './GameInfo.vue'

// FIXME: get this from Meeting type directly
// See: https://github.com/vuejs/core/issues/4294
// See: https://github.com/wheatjs/vite-plugin-vue-type-imports
const props = defineProps({
  title: String,
  date: String,
  location: String,
  games: Array,
  alternate_side_games: Array
})
</script>

<template>
  <div class="item">
    <div class="details">
      <div class="when-and-where">
        <span class="date">{{ Intl.DateTimeFormat('default', {dateStyle: 'long'}).format(new Date(date)) }}</span>
        <span v-if="location" class="location">
          at {{ location }}
        </span>
    </div>
      <h3>{{ title }}</h3>
      <div v-for="game in games">
        <GameInfo v-bind="gameList[game]" />
      </div>
      <div v-if="alternate_side_games">
        Alternate side games:
        <li v-if="alternate_side_games" v-for="game in alternate_side_games">
          {{ gameList[game].name }}
        </li>
      </div>
    </div>
  </div>
</template>

<style scoped>
.when-and-where {
  color: #808080;
  font-size: 70%;
}
.item {
  margin-top: 2rem;
}
h3 {
  font-size: 1.2rem;
  font-weight: 500;
  margin-bottom: 0.4rem;
  color: var(--color-heading);
}
</style>
