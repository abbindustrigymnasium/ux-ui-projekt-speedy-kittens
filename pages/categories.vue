<template>
  <div class="min-h-screen bg-cover py-24" style="background-image: url(https://static.vecteezy.com/system/resources/previews/003/421/363/original/abstract-modern-gradient-dark-blue-dynamic-stripes-background-free-vector.jpg);">
    <div class="w-5/6 mx-auto bg-gray-800 mt-10 py-12 md:px-16 px-8 rounded-xl" style="box-shadow: 0 0 48px 0 rgba(0,10,20,0.4);">
      <h1 class="text-gray-300 text-center flex justify-center" style="top:0; font-weight: 600;">Categories</h1>
      <hr
              class="w-full mb-4"
              style="border: none; height: 2px; background: rgb(255, 136, 80); background: linear-gradient(90deg, rgba(255, 136, 80, 0) 0%, rgba(255, 136, 80, 0.7) 25%, rgba(255, 136, 80, 1) 50%, rgba(255, 136, 80, 0.7) 75%, rgba(255, 136, 80, 0) 100%);"
            />
      <div class="flex flex-wrap w-full" style="justify-content: center;">
        <div @click="goToCategory(category[2])" class="md:w-60 w-full md:my-6 md:mx-8 my-4 mx-5 bg-gray-700 text-center rounded-lg h-64" style="cursor: pointer; box-shadow: 0 12px 24px 0 rgba(0,10,20,0.3);" v-for="category in categories" :key="category.id" :style="{
            // backgroundImage: `url(${category.id})`,
            // textShadow: '0 0 6px rgba(0, 0, 30, 1)'
            }">

            <p class="text-center p-2 md:h-12 md:rounded-lg rounded-md text-white font-medium">{{category[0]}}</p>
            <img :src="category[3]" class="w-64 h-56 flex object-cover rounded-b-md">
        </div>
      </div>
      <hr
              class="w-full mt-8"
              style="border: none; height: 2px; background: rgb(255, 136, 80); background: linear-gradient(90deg, rgba(255, 136, 80, 0) 0%, rgba(255, 136, 80, 0.7) 25%, rgba(255, 136, 80, 1) 50%, rgba(255, 136, 80, 0.7) 75%, rgba(255, 136, 80, 0) 100%);"
            />
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
