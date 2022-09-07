<template>
  <div>
    
    <h1>Categories</h1>
    <div class="flex flex-wrap" style="justify-content: center; margin-bottom:200px">
      <div @click="goToCategory(category[2])" class="w-56 m-6" style="cursor: pointer; background-color: rgb(150, 150, 150);" v-for="category in categories" :key="category.id">

          <p>{{category[0]}}</p>
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
