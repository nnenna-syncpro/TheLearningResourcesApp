<template>
    <ul>
        <!-- benefits of creating a separate list component are: to help modularize the code, keep file from getting to bulky/cumbersome, and make finding and editing code easier -->
        <learning-resource v-for="resource in storedResources" :key="resource.id" :title="resource.title" :description="resource.description" :link="resource.link"></learning-resource>
    </ul>
</template>

<script>
import LearningResource from "./components/learning-resources/LearningResource.vue";
export default {
    components: {
        LearningResource
    },
    data () {
        return {
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
        }
    }
}
</script>