<template>
    <div class="min-h-screen bg-cover w-full" style="background-image: url(https://static.vecteezy.com/system/resources/previews/003/421/363/original/abstract-modern-gradient-dark-blue-dynamic-stripes-background-free-vector.jpg);">
      <h1 class="z-10 md:text-5xl text-xl text-gray-200 text-center mx-auto pt-24 md:w-6/12 w-3/4 justify-center "> {{book.title}} </h1>
      <div class="bg-gray-700 flex md:row col box-shadow md:w-7/12 w-5/6 rounded-xl mx-auto">
        <img :src="book.img" class="md:w-4/12 w-full bg-cover rounded-l-xl">
        <div class="p-4 md:8/12 w-1/2 p-4">
          <!-- <h1 class="flex text-white md:text-2xl text-md">{{book.title}}</h1> -->
          <h3 class="text-white md:text-xl text-sm">Author:&ensp; &emsp;    {{book.author}}</h3>
          <h3 class="text-white md:text-xl text-sm">Genre: &ensp; &emsp;    {{book.genre.toString()}}</h3>
          <h3 class="text-white md:text-xl text-sm">Language:&ensp;   {{book.lang}}</h3>
          <h3 class="text-white md:text-xl text-sm">Copies left: {{book.copies}}</h3>
          <button style="background: rgb(255,0,0);
            background: linear-gradient(130deg, rgba(255,0,0,1) 0%, rgba(254,132,3,1) 16%, rgba(217,224,32,1) 32%, rgba(33,223,32,1) 50%, rgba(52,144,252,1) 75%, rgba(252,69,202,1) 100%);" class="h-4/12 w-4/12 p-2 box-shadow rounded mt-32 ml-80">Buy
          </button>
        </div>
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




