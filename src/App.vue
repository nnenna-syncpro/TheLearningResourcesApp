<template>
    <the-header title="Learning Resources"></the-header>
    <stored-resources :resources="storedResources"> </stored-resources>
</template>

<script>
import StoredResources from "./components/learning-resources/StoredResources.vue";
import TheHeader from "./components/layouts/TheHeader.vue";

export default {
    components: {
        StoredResources,
        TheHeader
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

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

* {
  box-sizing: border-box;
}

html {
  font-family: 'Roboto', sans-serif;
}

body {
  margin: 0;
}
</style>