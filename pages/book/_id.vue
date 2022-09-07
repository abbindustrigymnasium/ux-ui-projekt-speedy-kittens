<template>
    <!-- <div style="margin-left:10%; margin-right:10%;">
        <nuxt-content :document="post"></nuxt-content>
        <br>
        <h5>Author: {{ post.author}}</h5>
        <p>Created: {{ post.created}}</p> 
        <p>Updated: {{ post.updated}}</p>
        <br>
    </div> -->
    <div>
        {{book.title}}
        <img :src="book.img" alt="">
        {{book.author}}
    </div>
</template>

<script>
export default {
    async asyncData({$content, params}){
        // let post = await $content('postsmd/'+params.id).fetch();
        let database = require('@/db_books.json');
        let book
        for(let i = 0; i<database["books"].length; i++) if(params.id == database["books"][i]["ISBN"]) book = database["books"][i]
        return {
            book
        }

    }
}

</script>




