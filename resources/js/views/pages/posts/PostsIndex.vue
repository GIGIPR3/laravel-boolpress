<template>
    <div>
        <!-- Scrivere i dati dei posts -->
        <h1>Sono la pagina della lista dei posts</h1>
        <PostsList />
    </div>
</template>

<script>
import PostsList from "../../../components/posts/PostsList.vue"
export default {
    name: 'Posts',
    components: {
        PostsList
    },
    data() {
        return {
        }
    },
    methods: {
    }
}
</script>