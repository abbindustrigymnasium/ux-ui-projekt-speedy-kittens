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
        <h1>Recomended Books</h1>
        <div class="flex flex-wrap" style="justify-content: center; margin-bottom:200px">
            <div @click="goToBook(book.ISBN)" class="w-56 m-6" style="cursor: pointer; background-color: rgb(150, 150, 150);" v-for="book in books" :key="book.id">

                <p>{{book.ISBN}}</p>
                <p>{{book.title}}</p>
                <img :src="book.img" alt="">
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

    }, 
  methods: {
    goToBook(id) {
      this.$router.push('/book/'+id)
    }
  }
}

</script>




