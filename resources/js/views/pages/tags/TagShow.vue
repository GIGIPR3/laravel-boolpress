<template>
    <div>
        <h1>
            Pagina dettaglio dei tag: {{ this.$route.params.name }}
        </h1>
        <div>
            <TagCard />
        </div>
    </div>
</template>

<script>
import TagCard from '../../../components/tags/TagCard.vue'
export default {
    name: 'TagShow',
    components: {
        TagCard
    }
}
</script >