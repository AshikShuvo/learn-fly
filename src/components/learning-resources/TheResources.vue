<template>
  <base-card>
    <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMod">Stored Resoource</base-button>
    <base-button @click="setSelectedTab('add-resource')" :mode="addResButtonMod">Add Resource</base-button>
  </base-card>
  <keep-alive>
    <component :is="selectedTab" @delete-resource="deleteIt"></component>
  </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue'
export default {
    components:{
        StoredResources,
        AddResource
    },
    computed:{
        storedResButtonMod(){
            return this.selectedTab==='stored-resources'?null:'flat';
        },
         addResButtonMod(){
            return this.selectedTab==='add-resource'?null:'flat';
        }
    },
    data(){
        return {
            selectedTab:'stored-resources',
            storedResources:[
                {id:'official-guid', title:'Official Guid',description:'The official vue js resource',link:'https://vuejs.org'},
                 {id:'google-guid', title:'Google Search',description:'The official website of google to search',link:'https://google.com'},
            ],
        }
    },
    provide(){
        return {
            resources:this.storedResources,
            addResource:this.addResource,
            deleteResource:this.deleteIt
        }
    },
    methods:{
        setSelectedTab(tab){
            this.selectedTab=tab;
        },
        addResource(title,description,link){
            const newResource={
                id:new Date().toISOString(),
                title,
                description,
                link
                
            };
            this.storedResources.unshift(newResource);
            this.selectedTab='stored-resources';
        },
        deleteIt(id){
            const index=this.storedResources.findIndex(item=>item.id===id)
            this.storedResources.splice(index,1);
        }
    } 
      


}
</script>

<style>

</style>