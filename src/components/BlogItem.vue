<script>
    export default {
        props: ['blog'],

        data(){
            return {

            }
        },
    };
</script>

<template>
    <button @click="$emit('show-blog',blog.id)">
        <img :src="blog.image" :alt="blog.title" class="img-fluid rounded shadow">
        <abbr :title="blog.title">
            <h6 v-text="blog.title.substring(0,8) + '...'"></h6>
        </abbr>
    </button>

</template>
