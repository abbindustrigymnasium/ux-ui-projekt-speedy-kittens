<template>
  <div class="pt-24 bg-gray-800">
    
    <div style="width:80vw; margin: 0% 10% 0% 10%;">
      <div class="quick-about">
        <div class="flex flex-wrap">
          <div class="w-full md:w-1/2">
          <!-- <br>
          <br>
          <br> -->
            <!-- <img src="/pictures/Capture.png" width="80%" style="margin:17.5%"> -->
            <!-- <img src="https://assets-global.website-files.com/5d6ebfe6117b67440d16086f/61261fe24a57aa3847af57ce_fibra%20Copia%20de%20Ima%CC%81genes%20TechBlog.png" width="65%" style="margin:17.5%">
            <div id="orange-thing"></div> -->
          </div>
          <div class="w-full md:w-1/2">
             <!-- <nuxt-content :document="about" style="margin:10%;" class="font-body"></nuxt-content> -->
          </div>
        </div>
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
      let categorys = []
      for(let i = 0; i<db["books"].length; i++) if(db["books"][i]["img"])books.push(db["books"][i])
      console.log(books.length)
      for(let i = 0; i<books.length; i++){
        for(let j = 0; j<books[i]["genre"].length; j++){
          let seen = false
          for(let gen = 0; gen<categorys.length; gen++){
            if(books[i]["genre"][j] == categorys[gen][0]){
              categorys[gen][1]++
              seen = true
              break;
            }
          }
          if(!seen) categorys.push([books[i]["genre"][j], 1])
        }
      }
      console.log("**************")
      console.log(categorys.length)
      for(let i = 0; i<categorys.length; i++){
        console.log(categorys[i][0], categorys[i][1])
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




<style>

  * {
    font-family:
            'Source Sans Pro',
            -apple-system,
            BlinkMacSystemFont,
            'Segoe UI',
            Roboto,
            'Helvetica Neue',
            Arial,
            sans-serif;
        font-size: 16px;
        word-spacing: 1px;
        -ms-text-size-adjust: 100%;
        -webkit-text-size-adjust: 100%;
        -moz-osx-font-smoothing: grayscale;
        -webkit-font-smoothing: antialiased;
        box-sizing: border-box;
  }

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



