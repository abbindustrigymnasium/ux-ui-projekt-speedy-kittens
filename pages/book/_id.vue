<template>
    <!-- <div style="margin-left:10%; margin-right:10%;">
        <nuxt-content :document="post"></nuxt-content>
        <br>
        <h5>Author: {{ post.author}}</h5>
        <p>Created: {{ post.created}}</p>
        <p>Updated: {{ post.updated}}</p>
        <br>     class="flex justify-start" style="margin-left:5%;"
    </div> -->
    <div class="bg-gray-800 min-h-screen">
      <h1 class="z-10 text-5xl justify-start text-white pt-24 w-6/12 justify-center " style="margin-left:20%;"> {{book.title}} skriven av {{book.author}} </h1>
      <div class="bg-gray-700 flex justify-start box-shadow w-7/12" style="margin-left:20%;">


        <img :src="book.img" class="w-4/12">
        <h1>det här är en bok</h1>



    </div>
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

<style>


</style>




