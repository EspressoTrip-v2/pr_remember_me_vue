<template>
  <li>
    <base-card>
      <header>
        <h3>{{ resource.title }}</h3>
        <base-button mode="flat" @click="deleteResource">Delete</base-button>
      </header>
      <p>{{ resource.description }}</p>
      <nav>
        <a :href="resource.link">View Resource</a>
      </nav>
    </base-card>
  </li>
</template>
<script>
import BaseButton from '@/components/ui/BaseButton.vue';

export default {
  components: { BaseButton },
  props: {
    resource: {
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
  },
  methods: {
    deleteResource() {
      console.log(this.resource.id);
      this.$emit('delete-resource', this.resource.id);
    },
  },
};
</script>

<style scoped>
li {
  margin: auto;
  max-width: 40rem;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h3 {
  font-size: 1.25rem;
  margin: 0.5rem 0;
}

p {
  margin: 0.5rem 0;
}

a {
  text-decoration: none;
  color: #ce5c00;
}

a:hover,
a:active {
  color: #c89300;
}
</style>
