<template>
  <div>
    
    <div style="width:80vw; margin: 0% 10% 0% 10%;">
      <div class="quick-about">
        <div class="flex flex-wrap">
          <div class="w-full md:w-1/2">
          <br>
          <br>
          <br>
            <!-- <img src="/pictures/Capture.png" width="80%" style="margin:17.5%"> -->
            <!-- <img src="https://assets-global.website-files.com/5d6ebfe6117b67440d16086f/61261fe24a57aa3847af57ce_fibra%20Copia%20de%20Ima%CC%81genes%20TechBlog.png" width="65%" style="margin:17.5%">
            <div id="orange-thing"></div> -->
          </div>
          <div class="w-full md:w-1/2">
             <!-- <nuxt-content :document="about" style="margin:10%;" class="font-body"></nuxt-content> -->
          </div>
        </div>
        <h1>Recomended Books</h1>
        <div class="flex flex-wrap" style="justify-content: center; margin-bottom:200px">
          <div @click="goToBook(book.ISBN)" class="w-56 m-6" style="cursor: pointer; background-color: rgb(150, 150, 150);" v-for="book in books" :key="book.id">

              <p>{{book.ISBN}}</p>
              <p>{{book.title}}</p>
              <img :src="book.img" alt="">
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  async asyncData({$content}){
      // let about = await $content('index/short-about').fetch()
      // let pages = await $content('postsmd').sortBy('nr', 'desc').without(['body']).fetch()
      // sortBy('id', 'desc').limit() 
      let db = require('../db_books.json');
      let books = []
      for(let i = 0; i<db["books"].length; i++) if(db["books"][i]["img"])books.push(db["books"][i])
      // console.log(books.length)
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




<style>
  .quick-about{
    width:100%;
  }
  #orange-thing{
    position: absolute; 
    width:20%; 
    height:70%; 
    background-color: #f0b541;
    top: 67.5%;
    left: 12%;
    z-index: -1;
  }
  .bloglist{
    width: 30%;
  }
</style>



