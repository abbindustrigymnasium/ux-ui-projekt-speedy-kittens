<template>
  <div>
    <h1 class="text-gray-300">Our staff</h1>
    <div class="flex flex-wrap bg-gray-700 py-12" style="justify-content: center; box-shadow: 0 0 48px 0 rgba(0,10,20,0.3);">
      <div class="h-80 w-60 m-6 bg-gray-600 bg-cover text-gray-200 font-medium" style="cursor: pointer; box-shadow: 0 12px 24px 0 rgba(0,10,20,0.3);" v-for="person in people" :key="person.id" :style="{
      textShadow: '0 0 6px rgba(0, 0, 30, 1)'
      }">
          <img :src="person.avatar" alt="" class="w-full h-60 bg-cover">  
          <div class="w-full h-56"></div>
          <div class="bg-gray-500 bg-opacity-100 h-24 p-4">
            <p>{{person.name}}</p>
          </div>
          
      </div>
    </div>
  </div>
</template>

<script>
export default {
    async asyncData({$content}){
      let people = require('@/staff.json')["staff"];
      return {
          people
      }
  }, 
}
</script>
