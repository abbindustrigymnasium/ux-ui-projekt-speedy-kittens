<template>
  <div class="min-h-screen bg-cover mt-20 py-24" style="background-image: url(https://static.vecteezy.com/system/resources/previews/003/421/363/original/abstract-modern-gradient-dark-blue-dynamic-stripes-background-free-vector.jpg);">
    <div class="w-5/6 mx-auto bg-gray-800 py-12 px-24 rounded-xl">
      <h1 class="text-gray-300 text-center">Categories</h1>
      <div class="flex flex-wrap" style="justify-content: center; margin-bottom:200px">
        <div @click="goToCategory(category[2])" class="w-56 m-6" style="cursor: pointer; background-color: rgb(150, 150, 150);" v-for="category in categories" :key="category.id">

            <p class="text-center h-24">{{category[0]}}</p>
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
            categories.push([books[i]["genre"][j], 1, identify])
          }
        }
      }
      console.log("amount of categories = ", categories.length)
      // for(let i = 0; i<categories.length; i++){
      //   console.log(categories[i][0], categories[i][1], categories[i][2])
      // }
      return {
          categories
      }
  }, 
  methods: {
    goToCategory(id) {
      this.$router.push('/category/'+id)
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
