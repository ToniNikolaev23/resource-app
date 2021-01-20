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
    <keep-alive>
    <component :is="selectedComponent"></component>
    </keep-alive>
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
        resources: this.storedResources,
        addResource: this.addResource,
        removeResource: this.removeResource
    }
},
  methods: {
    setComponent(tab) {
      this.selectedComponent = tab;
    },
    addResource(title,description,link){
        const newResource = {
            id: new Date().toISOString(),
            title: title,
            description: description,
            link: link
        }

        this.storedResources.unshift(newResource)

        this.selectedComponent = 'stored-resources'
    },
    removeResource(resId){
        const resIndex = this.storedResources.findIndex(res => res.id === resId)

        this.storedResources.splice(resIndex, 1)
    }
  },
};
</script>