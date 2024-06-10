<template>
    <base-card>
        <base-button @click="setSelectedTab('stored-resources')" :mode="storedResourcesButtonSelected">Stored Resources</base-button>
        <base-button @click="setSelectedTab('add-resource')" :mode="addResourceButtonSelected">Add New Resource</base-button>
    </base-card>
    <component :is="selectedTab"></component>
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
            addNewResource: this.addNewResource
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