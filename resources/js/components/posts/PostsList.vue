<template>
    <div>
        <!-- Uso il loader -->
        <Loader v-if="isLoading" />

        <ul v-else-if="posts.length">
            <li v-for="elem in posts" :key="elem.id">
                <router-link :to="`/posts/${elem.id}`">
                    <p> Name: {{ elem.name }}</p>
                    <p> Date: {{ elem.date }}</p>
                    <p> Description: {{ elem.description }}</p>

                </router-link>

                <span v-if="elem.category">
                    <p>Category: {{ elem.category.name }}</p>

                </span>
                <ol>
                    <li v-for="tag in elem.tags" :key="tag.id">{{ tag.name }}</li>
                </ol>
            </li>
        </ul>
        <p v-else>Non ci sono post nel DB</p>

        <!-- Paginazione -->
        <Pagination @on-page-change="getPosts" :pagination="pagination" />
    </div>
</template>

<script>
import Loader from '../Loader.vue'
import Pagination from '../Pagination.vue'
export default {
    name: 'PostsList',
    components: {
        Loader,
        Pagination
    },
    data() {
        return {
            posts: [],
            isLoading: false,
            pagination: {}
        }
    },
    mounted() {
        this.getPosts();
    },
    methods: {
        getPosts(page = 1) {
            this.isLoading = true
            axios.get('http://localhost:8000/api/posts?page=' + page)
                .then((res) => {
                    console.log(res.data);
                    //this.posts = res.data.data
                    // const data = res.data.data;
                    // const current_page = res.data.current_page;
                    // const last_page = res.data.last_page;
                    //destrutturizzazione
                    const { data, current_page, last_page } = res.data;
                    this.posts = data;
                    this.pagination = {
                        lastPage: last_page,
                        currentPage: current_page
                    }
                }).catch(err => {
                    console.log(err)
                }).then(() => {
                    this.isLoading = false
                })
        }
    }
}
</script>

<style scoped lang="scss">

</style>