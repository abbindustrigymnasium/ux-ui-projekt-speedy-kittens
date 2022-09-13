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
        <h1 class="text-gray-300">Recomended Books</h1>
        <div class="flex flex-wrap bg-gray-700 py-12" style="justify-content: center; box-shadow: 0 0 48px 0 rgba(0,10,20,0.3);">
          <div @click="goToBook(book.ISBN)" class="h-80 w-60 m-6 bg-gray-600 bg-cover text-gray-200 font-medium" style="cursor: pointer; box-shadow: 0 12px 24px 0 rgba(0,10,20,0.3);" v-for="book in books" :key="book.id" :style="{
          backgroundImage: `url(${book.img})`,
          textShadow: '0 0 6px rgba(0, 0, 30, 1)'
          }">
              <!-- <img :src="book.img" alt="" class="w-full h-60 bg-cover">   -->
              <div class="w-full h-56"></div>
              <div class="bg-gray-500 bg-opacity-100 h-24 p-4">
                <!-- <p>{{book.ISBN}}</p> -->
                <p>{{book.title}}</p>
                <!-- <p>{{book.author}}</p> -->
              </div>
              
          </div>
        </div>
    </div>
</template>

<script>
export default {
    async asyncData({$content, params}){
        // let post = await $content('postsmd/'+params.id).fetch();
        let db = require('@/db_books.json');
        let allbooks = []
        let books = []
        console.log(params.id)
        for(let i = 0; i<db["books"].length; i++) if(db["books"][i]["img"])allbooks.push(db["books"][i])
        for(let i = 0; i<allbooks.length; i++){
            for(let j = 0; j<allbooks[i]["genre"].length; j++){
                let identify = allbooks[i]["genre"][j]
                for(let letter = 0; letter < allbooks[i]["genre"][j].length; letter++) if(identify[letter] == ' ') identify = identify.substring(0,letter) + '-' + identify.substring(letter+1)
                if(identify == params.id){
                    books.push(allbooks[i])
                    break;
                }
                
            }
        }
        return {
            books
        }

    }
}

</script>




