<template>
  <div class="min-h-screen bg-cover pt-24" style="background-image: url(https://static.vecteezy.com/system/resources/previews/003/421/363/original/abstract-modern-gradient-dark-blue-dynamic-stripes-background-free-vector.jpg);">
    <div class="w-5/6 mx-auto bg-gray-800 px-24 rounded-xl" style="box-shadow: 0 0 48px 0 rgba(0,10,20,0.4);">
      <h1 class="text-gray-300 mt-20 pt-8 text-center mb-0" style="top:0;">Our Staff</h1>
      <div class="flex flex-wrap mx-auto py-12" style="justify-content: center; top:0;">
        <div class="h-70 w-100 m-6 p-6 bg-gray-600 bg-cover text-gray-200 font-medium rounded-lg" style="min-width: 300px; box-shadow: 0 12px 24px 0 rgba(0,10,20,0.3);" v-for="person in people" :key="person.id" :style="{
          textShadow: '0 0 6px rgba(0, 0, 30, 1)'
          }">
              <img :src="person.avatar" alt="" class="w-20 h-20 object-cover mb-2" style="border-radius: 50%;">

              <p>{{person.name}}</p>
              <p>Role: {{person.role}}</p>
              <br>
              <p>Contact information</p>
              <p>Email: {{person.email}}</p>
              <p>Phone: {{person.phone}}</p>

        </div>
      </div>
    </div>
    <br>
    <br>
    <br>
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
