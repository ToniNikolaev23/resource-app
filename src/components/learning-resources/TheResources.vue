<template>
  <div>
    <base-card>
      <base-button @click="setComponent('stored-resources')"
      :mode="setStoredStyleMode"
        >Stored Resources</base-button
      >
      <base-button @click="setComponent('add-resource')"
      :mode="setAddResourceStyleMode"
        >Add Resource</base-button
      >
    </base-card>

    <component :is="selectedComponent"></component>
  </div>
</template>


<script>
import AddResource from "./AddResource.vue";
import StoredResources from "./StoredResources.vue";
export default {
  components: {
    AddResource,
    StoredResources,
  },
  data() {
    return {
      selectedComponent: "stored-resources",
      storedResources: [
        {
          id: "official-guide",
          title: "Official guide",
          description: "The official VueJS documentation",
          link: "https://vuejs.org",
        },
        {
          id: "google",
          title: "Google",
          description: "Learn to google",
          link: "https://google.com",
        },
      ],
    };
  },
  computed:{
      setStoredStyleMode(){
          return this.selectedComponent === 'stored-resources' ? null : 'flat'
      },
      setAddResourceStyleMode(){
          return this.selectedComponent === 'add-resource' ? null : 'flat'
      }
  },
provide(){
    return{
        resources: this.storedResources
    }
},
  methods: {
    setComponent(tab) {
      this.selectedComponent = tab;
    },
  },
};
</script>