<template>
  <div class="min-h-screen bg-cover pt-24" style="background-image: url(https://static.vecteezy.com/system/resources/previews/003/421/363/original/abstract-modern-gradient-dark-blue-dynamic-stripes-background-free-vector.jpg);" >
    <div>
      <div class="quick-about">
        <div class="w-5/6 mx-auto bg-gray-800 mt-10 py-12 md:px-16 px-8 rounded-xl" style="box-shadow: 0 0 48px 0 rgba(0,10,20,0.4);">
          <h1 class="text-gray-300 text-center flex justify-center" style="top:0; font-weight: 600; ">Recommended Books</h1>
          <hr
              class="w-full mb-4"
              style="border: none; height: 2px; background: rgb(255, 136, 80); background: linear-gradient(90deg, rgba(255, 136, 80, 0) 0%, rgba(255, 136, 80, 0.7) 25%, rgba(255, 136, 80, 1) 50%, rgba(255, 136, 80, 0.7) 75%, rgba(255, 136, 80, 0) 100%);"
            />
          <div class="flex flex-wrap w-full" style="justify-content: center; top:0;">
            <div @click="goToBook(book.ISBN)" class="h-80 md:w-60 w-full md:my-6 md:mx-8 my-4 mx-5 bg-gray-600 bg-cover text-gray-200 rounded-lg" style="cursor: pointer; box-shadow: 0 12px 24px 0 rgba(0,10,20,0.3);" v-for="book in books" :key="book.id" :style="{
            backgroundImage: `url(${book.img})`,
            textShadow: '0 0 6px rgba(0, 0, 30, 1)'
            }">
                <!-- <img :src="book.img" alt="" class="w-full h-60 bg-cover">   -->
                <div class="w-full h-56"></div>
                <div class="bg-gray-700 bg-opacity-100 h-24 px-4 pb-2 rounded-b-lg">
                  <!-- <p>{{book.ISBN}}</p> -->
                  <hr
                    class="w-full mb-2 "
                    style="border: none; height: 2px; background: rgb(255, 136, 80); background: linear-gradient(90deg, rgba(255, 136, 80, 0) 0%, rgba(255, 136, 80, 0.7) 25%, rgba(255, 136, 80, 1) 50%, rgba(255, 136, 80, 0.7) 75%, rgba(255, 136, 80, 0) 100%);"
                  />
                  <p class="font-medium text-center">{{book.title}}</p>
                  <!-- <p>{{book.author}}</p> -->
                </div>
            </div>
          </div>
          <hr
              class="w-full mt-8"
              style="border: none; height: 2px; background: rgb(255, 136, 80); background: linear-gradient(90deg, rgba(255, 136, 80, 0) 0%, rgba(255, 136, 80, 0.7) 25%, rgba(255, 136, 80, 1) 50%, rgba(255, 136, 80, 0.7) 75%, rgba(255, 136, 80, 0) 100%);"
            />
        </div>
        <br>
        <br>
        <br>
      </div>
    </div>
  </div>
</template>

<script>


  // let stringChars = 20
  // let trimmedString = trimFunction(stringChars, bookTitle);
export default {
  name: 'IndexPage',
  async asyncData({}){
      // let about = await $content('index/short-about').fetch()
      // let pages = await $content('postsmd').sortBy('nr', 'desc').without(['body']).fetch()
      // sortBy('id', 'desc').limit()
      let db = require('../db_books.json');
      let books = []
      for(let i = 0; i<db["books"].length; i++) if(db["books"][i]["img"])books.push(db["books"][i])
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



