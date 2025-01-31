<template>
  <ul>
    <learning-resource
      :key="res.id"
      v-for="res in resource"
      :resource="res"
    ></learning-resource>
  </ul>
</template>

<script>
import LearningResource from '@/components/learning-resources/LearningResource.vue';

export default {
  components: {
    LearningResource,
  },
  props: {
    resource: [
      {
        id: {
          type: String,
          required: true,
        },
        title: {
          type: String,
          required: true,
        },
        description: {
          type: String,
          required: true,
        },
        link: {
          type: String,
          required: true,
        },
      },
    ],
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>
