<template>
  <div>
    <h1 class="text-gray-300">Our staff</h1>
    <div class="flex flex-wrap bg-gray-700 py-12" style="justify-content: center; box-shadow: 0 0 48px 0 rgba(0,10,20,0.3);">
      <div class="h-60 w-80 m-6 p-6 bg-gray-600 bg-cover text-gray-200 font-medium" style="box-shadow: 0 12px 24px 0 rgba(0,10,20,0.3);" v-for="person in people" :key="person.id" :style="{
      textShadow: '0 0 6px rgba(0, 0, 30, 1)'
      }">
          <img :src="person.avatar" alt="" class="w-20 h-20 object-cover" style="border-radius: 50%;">

          <p>{{person.name}}</p>
          <p>{{person.role}}</p>
          <p>{{person.email}}</p>
          <p>{{person.phone}}</p>
          <p>{{person.dateOfBirth}}</p>

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
