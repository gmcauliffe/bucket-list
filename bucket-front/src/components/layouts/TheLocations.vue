<template lang="pug">
  .panel-container(
    fit-width="true",
    item-selector='.item',
    :origin-top="true",
    :horizontal-order="false",
  )
    location-card.item(
      v-for='(location, index) in locations',
      :key='index',
      :location='location',
      :post='posts[index]',
    )
</template>

<script>
import axios from 'axios';
import LocationCard from '../cards/LocationCard';

export default {
  components: {
    LocationCard
  },
  data() {
    return {
      locations: [],
      posts: [],
      errors: [],
    };
  },
  created() {
    axios.get('http://localhost:3000/locations')
      .then((response) => {
        const { locations,
          locationPosts,
        } = response.data;
        this.locations = locations;
        this.posts = locationPosts
      })
      .catch((e) => {
        this.errors.push(e);
      });
  },
};
</script>

<style scoped>

</style>
