<!-- This component removes the code to display the iterated list of learning resources from App.vue to make code more modular and also scope the style to the list -->
<template>
    <ul>
        <!-- benefits of creating a separate list component are: to help modularize the code, keep file from getting to bulky/cumbersome, and make finding and editing code easier -->
        <learning-resource v-for="resource in resources" :key="resource.id" :title="resource.title" :description="resource.description" :link="resource.link"></learning-resource>
    </ul>
</template>

<script>
import LearningResource from "./LearningResource.vue";
export default {
    components: {
        LearningResource
    },
    props: ["resources"]
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>