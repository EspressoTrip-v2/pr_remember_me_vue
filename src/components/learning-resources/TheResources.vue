<template>
  <base-card>
    <base-button
      @click="selectTab('stored-resources')"
      :mode="storedResButtonMode"
      >Stored Resource</base-button
    >
    <base-button @click="selectTab('add-resource')" :mode="addResButtonMode"
      >Add Resource</base-button
    >
    <keep-alive>
      <component :is="selectedTab"></component>
    </keep-alive>
  </base-card>
</template>
<script>
import StoredResources from './StoredResources.vue';
import AddResource from '@/components/learning-resources/AddResource.vue';
export default {
  components: {
    StoredResources,
    AddResource,
  },
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The official Vue.js documentation',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Google search engine',
          link: 'https://google.com',
        },
      ],
    };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    },
  },
  methods: {
    selectTab(tab) {
      this.selectedTab = tab;
    },
    addNewResource(newResource) {
      this.storedResources.unshift(newResource);
      this.selectedTab = 'stored-resources';
    },
    deleteResource(id) {
      const index = this.storedResources.findIndex((res) => res.id === id);
      this.storedResources.splice(index, 1);
    },
  },
  provide() {
    return {
      resources: this.storedResources,
      addNewResource: this.addNewResource,
      deleteResource: this.deleteResource,
    };
  },
};
</script>

<style scoped></style>
