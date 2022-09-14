<template>
  <div class="min-h-screen bg-cover py-24" style="background-image: url(https://static.vecteezy.com/system/resources/previews/003/421/363/original/abstract-modern-gradient-dark-blue-dynamic-stripes-background-free-vector.jpg);">
    <div class="w-5/6 mx-auto bg-gray-800 py-12 md:px-24 px-8 rounded-xl">
      <h1 class="text-gray-300 text-center">Categories</h1>
      <div class="flex flex-wrap w-full" style="justify-content: center; margin-bottom:200px">
        <div @click="goToCategory(category[2])" class="md:w-56 w-full md:m-6 my-4 mx-5 bg-gray-700 text-center" style="cursor: pointer; box-shadow: 0 12px 24px 0 rgba(0,10,20,0.3);" v-for="category in categories" :key="category.id" :style="{
            // backgroundImage: `url(${category.id})`,
            // textShadow: '0 0 6px rgba(0, 0, 30, 1)'
            }">

            <p class="text-center p-2 md:h-20 h-12 md:rounded-lg rounded-md">{{category[0]}}</p>
            <img :src="category[3]" alt="">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    async asyncData({$content}){
      let db = require('../db_books.json');
      let books = []
      let categories = []
      for(let i = 0; i<db["books"].length; i++) if(db["books"][i]["img"])books.push(db["books"][i])
      for(let i = 0; i<books.length; i++){
        for(let j = 0; j<books[i]["genre"].length; j++){
          let seen = false
          for(let gen = 0; gen<categories.length; gen++){
            if(books[i]["genre"][j] == categories[gen][0]){
              categories[gen][1]++
              seen = true
              break;
            }
          }
          if(!seen) {
            let identify = books[i]["genre"][j]
            for(let letter = 0; letter < books[i]["genre"][j].length; letter++) if(identify[letter] == ' ') identify = identify.substring(0,letter) + '-' + identify.substring(letter+1)
            // console.log(identify)
            categories.push([books[i]["genre"][j], 1, identify, books[i]["img"]])
          }
        }
      }
      console.log("amount of categories = ", categories.length)
      // for(let i = 0; i<categories.length; i++){
      //   console.log(categories[i][0], categories[i][1], categories[i][2])
      // }
      categories.sort()
      return {
          categories,
          books
      }
  }, 
  methods: {
    goToCategory(id) {
      this.$router.push('/category/'+id)
    },
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
</style>
