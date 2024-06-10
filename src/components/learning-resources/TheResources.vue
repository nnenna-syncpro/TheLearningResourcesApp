<template>
    <base-card>
        <base-button @click="setSelectedTab('stored-resources')" :mode="storedResourcesButtonSelected">Stored Resources</base-button>
        <base-button @click="setSelectedTab('add-resource')" :mode="addResourceButtonSelected">Add New Resource</base-button>
    </base-card>
    <keep-alive>
        <component :is="selectedTab">
            <!-- Because were using dynmaic component, the problem is that there is no place to listen fro the custom event deleteResource -->
        </component>
    </keep-alive>
</template>
<!-- moving StoredResources from App to TheResources made it unavailable to be displayed on App -->
<!-- add props to dynamic component or provide and inject. hence move StoredRecources array from App to TheResources -->
<script>
import StoredResources from "./StoredResources.vue";
import AddResource from "./AddResource.vue"
export default {
    components: {
        StoredResources,
        AddResource
    },
    data () {
        return {
            selectedTab: "stored-resources",
            storedResources: [
                {
                    id: "vue-guide",
                    title: "Vue Guide",
                    description: "Resource guide for vue",
                    link: "https://vuejs.org/guide/quick-start.html"
                },
                {
                    id: "google",
                    title: "Google",
                    description: "Resource guide for google",
                    link: "https://google.com"
                }
            ]
        };
    },
    provide () {
        return {
            resources: this.storedResources,
            addNewResource: this.addNewResource,
            deleteResource: this.deleteResource
        };
    },
    methods: {
        setSelectedTab(tab){
            this.selectedTab = tab;
        },
        addNewResource(title, description, urlLink) {
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                description: description,
                urlLink: urlLink

            }
            this.storedResources.push(newResource);
            //switch tab after adding a new resource
            this.selectedTab = "stored-resources";
        },
        deleteResource (resourceId) {
            //.push() changes the same array that was provided, however, .filter() creates a brand new array that is different from what was previously provided and hence the array created by .filter() is not re-provided
            // this.storedResources = this.storedResources.filter(resource => resource.id !== resourceId);
            // console.log(this.storedResources.length)

            //Soln
            //get index of resource to be deleted
            const resourceIndex = this.storedResources.findIndex(resource => resource.id === resourceId);
            //remove resource at index
            this.storedResources.splice(resourceIndex, 1);
        }
    },
    computed: {
        storedResourcesButtonSelected () {
            //give different styling to button not selected
            return this.selectedTab === "stored-resources" ? null : "flat";
        },
        addResourceButtonSelected () {
            return this.selectedTab === "add-resource" ? null : "flat";
        }
    }
}
</script>