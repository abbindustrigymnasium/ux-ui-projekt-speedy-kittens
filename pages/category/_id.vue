<template>
    <!-- <div style="margin-left:10%; margin-right:10%;">
        <nuxt-content :document="post"></nuxt-content>
        <br>
        <h5>Author: {{ post.author}}</h5>
        <p>Created: {{ post.created}}</p> 
        <p>Updated: {{ post.updated}}</p>
        <br>
    </div> -->
    <div class="min-h-screen bg-cover" style="background-image: url(https://static.vecteezy.com/system/resources/previews/003/421/363/original/abstract-modern-gradient-dark-blue-dynamic-stripes-background-free-vector.jpg);" >
        <br>
        <br>
        <br>
        <div class="w-5/6 mx-auto bg-gray-800 px-24 rounded-xl" style="cursor: pointer; box-shadow: 0 0 48px 0 rgba(0,10,20,0.4);">
            <h1 class="text-gray-300 mt-20 pt-8 text-center mb-0" style="top:0;">{{categoryName}}</h1>
            <div class="flex flex-wrap mx-auto py-12" style="justify-content: center; top:0;">
            
            <div id="booksDiv" @click="goToBook(book.ISBN)" class="h-80 w-60 mx-10 mb-16 bg-gray-600 bg-cover text-gray-200 font-medium rounded-lg" style="cursor: pointer; box-shadow: 0 12px 24px 0 rgba(0,10,20,0.3);" v-for="book in books" :key="book.id" :style="{
            backgroundImage: `url(${book.img})`,
            textShadow: '0 0 6px rgba(0, 0, 30, 1)'
            }">
                <!-- <img :src="book.img" alt="" class="w-full h-60 bg-cover">   -->
                <div class="w-full h-56"></div>
                <div class="bg-gray-600 bg-opacity-100 h-24 p-4 rounded-b-lg">
                    <!-- <p>{{book.ISBN}}</p> -->
                    <p>{{book.title}}</p>
                    <!-- <p>{{book.author}}</p> -->
                </div>
                
            </div>
            </div>
        </div>
        <br>
        <br>
        <br>
    </div>
</template>

<script>
export default {
    async asyncData({$content, params}){
        // let post = await $content('postsmd/'+params.id).fetch();
        let db = require('@/db_books.json');
        let allbooks = []
        let books = []
        let categoryName = ""
        console.log(params.id)
        for(let i = 0; i<db["books"].length; i++) if(db["books"][i]["img"])allbooks.push(db["books"][i])
        for(let i = 0; i<allbooks.length; i++){
            for(let j = 0; j<allbooks[i]["genre"].length; j++){
                let identify = allbooks[i]["genre"][j]
                for(let letter = 0; letter < allbooks[i]["genre"][j].length; letter++) if(identify[letter] == ' ') identify = identify.substring(0,letter) + '-' + identify.substring(letter+1)
                if(identify == params.id){
                    categoryName = allbooks[i]["genre"][j]
                    books.push(allbooks[i])
                    break;
                }
                
            }
        }
        return {
            books, categoryName
        }

    }, 
  methods: {
    goToBook(id) {
      this.$router.push('/book/'+id)
    }
  }
}

</script>

<style>

    #booksDiv:hover {
    transform: scale(0.95);
    transition: 200ms;
  }
</style>




