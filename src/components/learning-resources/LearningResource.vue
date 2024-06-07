<template>
    <li>
        <div>
            <header>
                <h3>{{title}}</h3>
                <button>Delete Resource</button>
            </header>
            <p>{{ description }}</p>
            <nav>
                <a :href="link">View Resource</a>
            </nav>
        </div>
    </li>
</template>

<script>
export default {
    props: ["id", "title", "description", "link"]
}
</script>